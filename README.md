# DotNet.Mono.Profiler.Android

Support for the Mono profiler in .NET 6 Android applications

## MSBuild Properties

* `$(AndroidMonoProfilers)`: list of Mono profilers to run. Defaults
  to `calls,alloc,nocounters`.

* `$(AndroidMonoProfilerOutput)`: location to save `profile.mlpd` on
  the Android device or emulator. Defaults to
  `/sdcard/Download/profile.mlpd`.

* `$(AndroidMonoProfilerEnvironmentFile)`: location of the generated
  `@(AndroidEnvironment)` file. Defaults to
  `$(IntermediateOutputPath)DotNet.Mono.Profiler.Android.env`.
