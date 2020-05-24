# Rename APK

In our Android development career, we all came across the scenario where we are generating the APK and before sharing it with others we are manually renaming it.

We all felt that this process should be automatic and it should produce the name as per the need of the developer.

If you search on the internet, you will find many answers to do so but those are confusing as each answer is associated with some specific gradle version.

Here, I am sharing the updated code which works for both debug and release builds.

---
Put following gradle function in _application level_ `build.gradle` file.

``` groovy
android.applicationVariants.all { variant ->
    def appName
    // if applicationName property is set in gradle.properties
    if (project.hasProperty("applicationName")) {
        appName = applicationName
    } else {
    // if not use the name of the parent project
        appName = parent.name
    }

    appName = appName.replaceAll(" ", "_")
    def formattedDate = new Date().format('yyyy_MM_dd_HH_mm_ss')

    variant.outputs.all { output ->
        outputFileName = "${appName}_${output.baseName}_${variant.versionCode}" +
                "(${variant.versionName})_${formattedDate}.apk"
        println("outputFileName: " + outputFileName)
    }
}
```
&nbsp;
Generated APK name: `SampleApp_debug_1(1.0)_2020_05_24_12_58_21.apk`