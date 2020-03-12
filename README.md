# Coatlus
Coatlus is a Gradle plugin allowing to make your let download needed dependencies on startup.

**This is a project idea and the plugin will be created later**

## Why download libraries on startup ?
Download dependencies on startup make your jar lighter and allow users to update only old dependencies without re-downloading all libraries. You can choose libraries you want to download on startup allowing you to do other operations for each library like shading it.

## Installation
To add this plugin to your build script, use:
```gradle
plugins {
  id 'fr.il_totore:coatlus:version'
}
```

## Configuration
Coatlus provides multiples tasks to improve configuration ease.

### Generate libraries file
To keep in memory download-required dependencies, Coatlus add into your jar a `libraries.json` file (can be renamed) using the `generateLibrariesFile` task.
```gradle
generateLibrariesFile {
  named 'libraries.json'
}
