Repro for cc_toolchain_suite uses gets incorrect paths when toolchains are in a different repository from the cc_toolchain_suite

In the `consumer` directory:

With Bazel at commit a8f0cf032a545f3c1a7a71ffa6fde6768756d63e (before the breaking change):
```console
% bazel build :gr
Extracting Bazel installation...
Starting local Bazel server and connecting to it...
INFO: Invocation ID: aedda700-8441-4469-9454-d4223c710ac8
INFO: Analyzed target //:gr (38 packages loaded, 153 targets configured).
INFO: Found 1 target...
Target //:gr up-to-date:
  bazel-bin/out
INFO: Elapsed time: 15.136s, Critical Path: 0.08s
INFO: 2 processes: 1 internal, 1 darwin-sandbox.
INFO: Build completed successfully, 2 total actions
```

With Bazel at commit d30fcf2f09021aa624a7954acfe563a9c8c622a2 (the breaking change):
```console
% bazel build :gr
INFO: Invocation ID: bbb3fa4c-7606-4a54-830c-e91e1b71463d
INFO: Analyzed target //:gr (1 packages loaded, 3 targets configured).
INFO: Found 1 target...
ERROR: /Volumes/Source/github.com/illicitonion/repro-bazel-cc-toolchain-starlark-paths/consumer/BUILD.bazel:1:8: Executing genrule //:gr failed: (Exit 1): bash failed: error executing command (from target //:gr) /bin/bash -c ... (remaining 1 argument skipped)

Use --sandbox_debug to see verbose messages from the sandbox and retain the sandbox build root for debugging
Wrong path to clang: bin/clang
Target //:gr failed to build
Use --verbose_failures to see the command lines of failed build steps.
INFO: Elapsed time: 0.117s, Critical Path: 0.02s
INFO: 2 processes: 2 internal.
ERROR: Build did NOT complete successfully
```
