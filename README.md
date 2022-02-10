# Mono.Profiler.Android

Support for the Mono profiler in .NET 6 Android applications

## Usage of the Mono Profiler

```dotnetcli
> dotnet new android
> dotnet add package Mono.Profiler.Android --prerelease
> dotnet build -c Release -t:StartProfiling
# Wait until app launches, or you navigate to a screen
> dotnet build -c Release -t:StopProfiling
```
_NOTE: you can also use `dotnet new maui`, build with `-f net6.0-android`._

This should produce `profile.mlpd` in the project's directory.

See [Profiling Managed Code][profiling] for more info.

[profiling]: https://github.com/xamarin/xamarin-android/blob/98d61e54736fda9e79fda62d49d20d9e7bc26ce7/Documentation/guides/profiling.md#profiling-managed-code

## Usage of the AOT Profiler

Use a Debug build, or set `-p:AndroidEnableAotProfiler=true`:

```dotnetcli
> dotnet add package Mono.AotProfiler.Android --prerelease
> dotnet build -t:BuildAndStartAotProfiling
# Wait until app launches, or you navigate to a screen
> dotnet build -t:FinishAotProfiling
```

This will produce a `custom.aprof` in your project directory.

To use `custom.aprof` going forward, you can do:

```xml
<PropertyGroup>
  <AndroidUseDefaultAotProfile>false</AndroidUseDefaultAotProfile>
</PropertyGroup>
<ItemGroup>
  <AndroidAotProfile Include="custom.aprof" />
</ItemGroup>
```

`-p:RunAOTCompilation=true` and `-p:AndroidEnableProfiledAot=true` are
required to enable Profiled AOT. This should be enabled by default
for `Release` builds.

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
