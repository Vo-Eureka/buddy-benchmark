# Audio Processing Benchmark

## Operation Level Benchmark

The table below lists the benchmark cases at the operation level.

| Name  | Build Target | Introduction |
| -------------- | ------------- | ------------- |
| Biquad Op  | `ninja dap-op-biquad-benchmark`  | This benchmark compares Buddy's `dap.biquad` operation with KFR library. Check the benchmark in [this file](./Operations/BiquadOp/Main.cpp). |
| FFT Op | `ninja dap-op-fft-benchmark`  | Task in TODO list. Check the benchmark in [this file](./Operations/FFTOp/Main.cpp). |
| FIR Op | `ninja dap-op-fir-benchmark`  | Task in TODO list. Check the benchmark in [this file](./Operations/FIROp/Main.cpp). |
| IIR Op | `ninja dap-op-iir-benchmark`  | This benchmark compares scalar and vectorized version `dap.iir` operation with KFR library. Check the benchmark in [this file](./Operations/IIROp/Main.cpp). |

### Local Hardware Platform.

1. Set KFR library path:

The audio processing benchmark currently includes the following frameworks and libraries:

- KFR ([link](https://github.com/kfrlib/kfr))


2. Build benchmark for local platform:

```bash
$ cd buddy-benchmark
$ mkdir build && cd build
$ cmake -G Ninja .. \
    -DCMAKE_BUILD_TYPE=RELEASE \
    -DAUDIO_PROCESSING_BENCHMARKS=ON \
    -DCMAKE_CXX_COMPILER=clang++ \
    -DKFR_DIR=/PATH/TO/KFR/SOURCE/CODE \
    -DBUDDY_MLIR_BUILD_DIR=/PATH/TO/BUDDY-MLIR/BUILD/
$ ninja <target benchmark>
// For example: 
$ ninja dap-op-iir-benchmark
```

3. Run the benchmark on your local platform:

```bash
// For example:
$ cd bin
$ ./dap-op-iir-benchmark
```

### audio-plot tool

1. Install required packages:

To help visualize the results of audio processing, we provide a tool for figure plotting. To use this tool, ensure that you are running `Python3` and have the necessary packages installed: `numpy`, `matplotlib` and `scipy`. You can install them using the following command:

```bash
$ pip install matplotlib scipy
```

2. Build benchmark for local platform:

You can customize the `python3` path during the build process by 
adding the option `-DPYTHON_BINARY_DIR=/PATH/TO/PYTHON/BIN` as follows:

```bash
$ cd build
$ cmake -G Ninja .. \
    -DAUDIO_PROCESSING_BENCHMARKS=ON \
    -DCMAKE_CXX_COMPILER=clang++ \
    -DKFR_DIR=/PATH/TO/KFR/SOURCE/CODE \
    -DBUDDY_MLIR_BUILD_DIR=/PATH/TO/BUDDY-MLIR/BUILD \
    -DPYTHON_BINARY_DIR=/PATH/TO/PYTHON/BIN/
$ ninja audio-plot
```

3. Run `audio-plot` on your local platform:

Once the processing is complete, you can use this tool to plot a comparision figure:

```bash
$ cd bin
$ ./audio-plot ../../benchmarks/AudioProcessing/Audios/NASA_Mars.wav ResultKFRIir.wav
```

The result is saved in `bin/res.png`. For additional usage details, run `audio-plot -h` to view the help information.