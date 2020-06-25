# Tensorflow-Lite-Select-TF-Ops-AAR
This repo contains the tensorflow-lite.aar and tensorflow-lite-select-tf-ops.aar (version 2.3).

The SSE4.1 and SSE4.2 are disabled to avoid the following error when running on android emulator which does not support them:
```
cpu_feature_guard.cc:36 The TensorFlow library was compiled to use SSE instructions, but these aren't available on your machine.
A/libc: Fatal signal 11 (SIGSEGV), code 1 (SEGV_MAPERR), fault addr 0xfffffff4 in tid xxx (xxx), pid xxx (xxx)
```

The budding command:
```
android update sdk --no-ui -a --filter tools,platform-tools,android-29,build-tools-29.0.2
bazel build -c opt --copt=-mno-sse4.1 --copt=-mno-sse4.2 --fat_apk_cpu=x86,x86_64,arm64-v8a,armeabi-v7a \
  --host_crosstool_top=@bazel_tools//tools/cpp:toolchain \
  //tensorflow/lite/java:tensorflow-lite[-select-tf-ops]
```
