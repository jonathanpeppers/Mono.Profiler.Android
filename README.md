# Mono.Profiler.Android

Support for the Mono profiler in .NET 6 Android applications

## Usage

```dotnetcli
> dotnet new android
> dotnet add package Mono.Profiler.Android
> dotnet build -c Release -t:StartProfiling
# Wait until app launches, or you navigate to a screen
> dotnet build -c Release -t:StopProfiling
```
_NOTE: you can also use `dotnet new maui`, build with `-f net6.0-android`._

This should produce `profile.mlpd` in the project's directory.

See [Profiling Managed Code][profiling] for more info.

[profiling]: https://github.com/xamarin/xamarin-android/blob/98d61e54736fda9e79fda62d49d20d9e7bc26ce7/Documentation/guides/profiling.md#profiling-managed-code

## MSBuild Properties

* `$(AndroidMonoProfilers)`: list of Mono profilers to run. Defaults
  to `calls,alloc,nocounters`.

* `$(AndroidMonoProfilerOutput)`: temporary location to save
  `profile.mlpd` on the Android device or emulator. Defaults to
  `/sdcard/Download/profile.mlpd`.

* `$(AndroidMonoProfilerEnvironmentFile)`: location of the generated
  `@(AndroidEnvironment)` file. Defaults to
  `$(IntermediateOutputPath)Mono.Profiler.Android.env`.

## To Build & Test this Repository

```dotnetcli
> dotnet build -c Release
> dotnet build -c Release samples/hellomaui/hellomaui.csproj -t:StartProfiling
> dotnet build -c Release samples/hellomaui/hellomaui.csproj -t:StopProfiling
```
