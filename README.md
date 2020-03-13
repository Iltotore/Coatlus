# Coatlus
Coatlus is a Gradle plugin allowing to make your let download needed dependencies on startup.

**This is a project idea and the plugin and the library will be created later. Note that the behavior can change**

## Why download libraries on startup ?
Download dependencies on startup make your jar lighter and allow users to update only old dependencies without re-downloading all libraries. You can choose libraries you want to download on startup allowing you to do other operations for each library like shading it.

## Installation
To add this plugin to your build script, use:
```gradle
plugins {
  id 'fr.il_totore:coatlus-plugin:version'
}
```
Then add to your dependencies the coatlus library:
```gradle
repositories {
  jcenter()
}

dependencies {
  implementation 'fr.il_totore:coatlus-lib:version'
}
```

## Build Configuration
Coatlus provides multiples tasks to improve configuration ease.

### Generate libraries file
To keep in memory download-required dependencies, Coatlus add into your jar a `libraries.json` file (can be renamed) using the `generateLibsFile` task.
```gradle
generateLibsFile {
  named 'coatlusLibs.json' //Default: libraries.json
  save project.configurations.example, project.configurations.anotherConfig
}
```

## Library Usage
The Coatlus library is used by the Coatlus Gradle Plugin. It provides tools to check for, download and load dependencies at runtime.

### Load libraries informations
Before installing and using libraries, you need to load their informations.

```java
LibRegistry libs = LibRegistry.fromJson(jsonObject); //Coatlus only support natively com.google.gson.JsonObject
```

### Download libraries
Now, you can download and updates libraries using LibRegistry#downloadLatest.
```java
PreparedDownload dl = libs.prepareDownload(libsDir)
  .useSSL(true)
  .filter(predicate)
  .updateExisting(true)
  .forceUpdate(false); //Only libsDir is required. Others parameters are optionals.
  
dl.execute()
```
