**Warning: this feature is not yet stable and currently under actively development; APIs may change until stablization**

This is a brief document about developing Xposed Modules using modern Xposed API. Documentation refinement is always welcome. Please submit a Feature Reuest issue with the refinement documentation for contribution.

### API Changes
Compared to the legacy XposedBridge APIs, the modern API has the following differences:
1. Java entry now uses `META-INF/xposed/java_init.list` instead of `assets/xposed_init`; native entry now uses `META-INF/xposed/native_init.list`. Create a file in `src/main/resources/META-INF`, and Gradle will automatically package files into your APK. You should now be able to obfuscate your entry classes with R8 with proguard rules `adaptresourcefilenames`.
1. Modern API does not use metadata anymore as well. Module name uses the `android:label` resource; module description uses the `android:description` resource; scope list uses `META-INF/xposed/scope.list` (one line for one package name); module configuration uses `META-INF/xposed/module.prop` (in format of [Java properties](https://docs.oracle.com/javase/7/docs/api/java/util/Properties.html)). 
1. Java entry should now implement `io.github.libxposed.api.XposedModule`. Each entry is a limited `android.content.Context`, providing a more familiar way for developers to handle. Most interfaces are not implemented by the `XposedModule` context, but will open more in the future. You can submit feature request with proper reason for a specific method.
1. Hook APIs are new but intentionally kept simple. We no longer provide interfaces like `XposedHelpers` in the framework anymore. But we will offer official libraries for a more friendly development kit. See [libxposed/helper](https://github.com/libxposed/helper) for this developing library.
1. You can now deoptmize a specific method to bypass method inline (especially when hooking System Framework)
1. Resource hooks are removed. Since we provide `XposedModule` context now, you can easily get the resource of your module. You can choice a better hook point to inject/modify the host resource.
1. You can communicate to the Xposed framework now. With the help of this feature, you can **dynamically request scope**, **share SharedPreference or blob file** across your module and hooked app, **check framework's name and version**, and more... To achieve this, you should declare a Xposed service in your module, and once your module is launched, the xposed framework will send you a service to communicate with the framework. See [libxposed/service](https://github.com/libxposed/service) for more details.
1. You can now analyze a dex by using `DexParser` API, which helps you to deobfuscate an Application and find the hook point, and to find caller of hooked methods for deoptimization to bypass method inline.

Module configuration uses entries as following:
|Name|Format|Optional|Meaning|
|:-|:-|:-|:-|
|minApiVersion|int|No|Indicates the minimal Xposed API version required by the module|
|targetApiVersion|int|No|Indicates the target Xposed API version required by the module|
|staticScope|boolean|Yes|Indicates whether users should not apply the module on any other app out of scope|


### Early Access
Note that most things are unstable, untested. APIs are likely to change in the feature. But you can still try them in your module if you need some of the new features. Please don't release a stable release until the new APIs are stable.
The current development status of all components are listed below.

|Componment|Usage|Repository|Status|
|:-|:-|:-|:-|
|LSPosed|Implement API and service; you don't need to declaring any dependency for it.|https://github.com/LSPosed/LSPosed|Done|
|API|User interface for hooks; you should declare it as dependency as `compileOnly`; don't use it together with the legacy `XposedBridge`|https://github.com/libxposed/api|Done; undocumented and may change|
|Service|Service to communicate with the Xposed Framework; you should depend on it by `implementation`|https://github.com/libxposed/service|PoC; likely to change in the feature, but you can use the raw binder API, which should be less likely to change|
|Helper|Utils to find classes fields, methods and kotlinize APIs; it should be depended by `implementation`|https://github.com/libxposed/helper|Developing; DSL APIs are designed but not yet implemented|

Aforementioned libraries will be published to maven central repository  when stabilized, but **not now**! They offer an CI version in Github Action. Download the artifacts, and merge it with your local maven repository (see more about [mavenLocal](https://docs.gradle.org/current/userguide/declaring_repositories.html#sec:case-for-maven-local)) or use the raw aar.

### Donation or Contribution
LSPosed and libxposed are open source projects, and we only work on them for interests. We are not dedicated into these projects and can only work on them in our spare time. That's why the new API takes some long for its first prototype. If you want the new API to grow faster, submit codes to help us, or [buy us a cup of coffee](https://github.com/sponsors/LSPosed).