---
layout: post
title:  "Gradle: Dump all tasks properties"
categories: android
tags: [gradle, android, tasks]
---

1. Add following script in your module's `build.gradle`

    ```groovy
    task('dumpTasks', dependsOn: 'preBuild') << {
        def p = rootProject.projectDir.parentFile.path
        def f = new File(buildDir, 'outputs/tasks.json')
        def pw = f.newPrintWriter()
        pw.println "{"
        def ts = tasks.findAll{ it.name.contains('Release') }
        def tn = ts.size()
        ts.eachWithIndex { t, ti ->
            pw.println "  \"${t.name}\": {"
            def strings = [:]
            def files = [:]
            def atoms = [:]
            t.properties.each { k, v ->
                if (k == 'path' || k == 'name' || k == 'temporaryDir') return
                if ((v instanceof String)) {
                    strings.put(k, v)
                } else if ((v instanceof File)) {
                    files.put(k, v)
                } else if ((v instanceof Boolean) || (v instanceof Integer)) {
                    atoms.put(k, v)
                }
            }
            strings.each { k, v ->
                pw.println  "    \"$k\": \"$v\","
            }
            files.each { k, File v ->
                String s = v.path
                if (s.startsWith(p)) {
                    s = '**' + s.substring(p.length())
                }
                pw.println  "    \"$k\": \"$s\","
            }
            def ai = 0
            def an = atoms.size()
            atoms.each { k, v ->
                ai++
                ai == an ? pw.println("    \"$k\": $v") : pw.println("    \"$k\": $v,")
            }
            tn == ti + 1 ? pw.println('  }') : pw.println('  },')
        }
        pw.println '}'
        pw.flush()
        pw.close()
    }
    ```

2. Execute task `dumpTasks`

    ```bash
    ./gradlew :your_module:dumpTasks
    ```

3. Find the output in your module's `build/outputs/tasks.json`

    Something like this:

    ```json
    {
      "assembleRelease": {
        "group": "build",
        "description": "Assembles all Release builds.",
        "didWork": false,
        "impliesSubProjects": false,
        "hasCustomActions": true,
        "enabled": true
      },
      "assembleReleaseUnitTest": {
        "didWork": false,
        "impliesSubProjects": false,
        "hasCustomActions": false,
        "enabled": true
      },
      "checkReleaseManifest": {
        "variantName": "release",
        "androidGradlePluginVersion": "2.0.0",
        "manifest": "**/Sample/app.main/src/main/AndroidManifest.xml",
        "didWork": false,
        "impliesSubProjects": false,
        "hasCustomActions": false,
        "enabled": true
      },
      "compileReleaseAidl": {
        "variantName": "release",
        "androidGradlePluginVersion": "2.0.0",
        "buildToolsVersion": "23.0.1",
        "incrementalFolder": "**/Sample/app.main/build/intermediates/incremental/compileReleaseAidl",
        "sourceOutputDir": "**/Sample/app.main/build/generated/source/aidl/release",
        "incremental": false,
        "didWork": false,
        "impliesSubProjects": false,
        "hasCustomActions": false,
        "enabled": true
      },
      "compileReleaseJavaWithJavac": {
        "sourceCompatibility": "1.7",
        "targetCompatibility": "1.7",
        "destinationDir": "**/Sample/app.main/build/intermediates/classes/release",
        "dependencyCacheDir": "**/Sample/app.main/build/intermediates/dependency-cache/release",
        "didWork": false,
        "impliesSubProjects": false,
        "hasCustomActions": true,
        "enabled": true
      },
      "compileReleaseNdk": {
        "variantName": "release",
        "androidGradlePluginVersion": "2.0.0",
        "objFolder": "**/Sample/app.main/build/intermediates/ndk/release/obj",
        "generatedMakefile": "**/Sample/app.main/build/intermediates/ndk/release/Android.mk",
        "soFolder": "**/Sample/app.main/build/intermediates/ndk/release/lib",
        "isForTesting": false,
        "debuggable": false,
        "ndkCygwinMode": false,
        "ndkRenderScriptMode": false,
        "didWork": false,
        "impliesSubProjects": false,
        "hasCustomActions": false,
        "enabled": true
      },
      "compileReleaseRenderscript": {
        "buildToolsVersion": "23.0.1",
        "variantName": "release",
        "androidGradlePluginVersion": "2.0.0",
        "sourceOutputDir": "**/Sample/app.main/build/generated/source/rs/release",
        "objOutputDir": "**/Sample/app.main/build/intermediates/rs/release/obj",
        "resOutputDir": "**/Sample/app.main/build/generated/res/rs/release",
        "libOutputDir": "**/Sample/app.main/build/intermediates/rs/release/lib",
        "ndkMode": false,
        "didWork": false,
        "impliesSubProjects": false,
        "hasCustomActions": false,
        "optimLevel": 3,
        "supportMode": false,
        "targetApi": 9,
        "debugBuild": false,
        "enabled": true
      },
      "compileReleaseSources": {
        "group": "build",
        "didWork": false,
        "impliesSubProjects": false,
        "hasCustomActions": false,
        "enabled": true
      },
      "compileReleaseUnitTestJavaWithJavac": {
        "sourceCompatibility": "1.7",
        "targetCompatibility": "1.7",
        "destinationDir": "**/Sample/app.main/build/intermediates/classes/test/release",
        "dependencyCacheDir": "**/Sample/app.main/build/intermediates/dependency-cache/test/release",
        "didWork": false,
        "impliesSubProjects": false,
        "hasCustomActions": false,
        "enabled": true
      },
      "compileReleaseUnitTestSources": {
        "group": "build",
        "didWork": false,
        "impliesSubProjects": false,
        "hasCustomActions": false,
        "enabled": true
      },
      "generateReleaseAssets": {
        "didWork": false,
        "impliesSubProjects": false,
        "hasCustomActions": false,
        "enabled": true
      },
      "generateReleaseBuildConfig": {
        "variantName": "release",
        "buildTypeName": "release",
        "versionName": "1.0",
        "androidGradlePluginVersion": "2.0.0",
        "appPackageName": "net.wequick.example.small.app.main",
        "flavorName": "",
        "buildConfigPackageName": "net.wequick.example.small.app.main",
        "sourceOutputDir": "**/Sample/app.main/build/generated/source/buildConfig/release",
        "debuggable": false,
        "versionCode": 1,
        "didWork": false,
        "impliesSubProjects": false,
        "hasCustomActions": false,
        "enabled": true
      },
      "generateReleaseResValues": {
        "variantName": "release",
        "androidGradlePluginVersion": "2.0.0",
        "resOutputDir": "**/Sample/app.main/build/generated/res/resValues/release",
        "didWork": false,
        "impliesSubProjects": false,
        "hasCustomActions": false,
        "enabled": true
      },
      "generateReleaseResources": {
        "didWork": false,
        "impliesSubProjects": false,
        "hasCustomActions": false,
        "enabled": true
      },
      "generateReleaseSources": {
        "didWork": false,
        "impliesSubProjects": false,
        "hasCustomActions": false,
        "enabled": true
      },
      "jarReleaseClasses": {
        "extension": "jar",
        "baseName": "app.main",
        "archiveName": "classes.jar",
        "classifier": "",
        "destinationDir": "**/Sample/app.main/build/intermediates/packaged/release",
        "archivePath": "**/Sample/app.main/build/intermediates/packaged/release/classes.jar",
        "caseSensitive": true,
        "includeEmptyDirs": true,
        "didWork": false,
        "impliesSubProjects": false,
        "hasCustomActions": false,
        "zip64": false,
        "enabled": true
      },
      "lintRelease": {
        "variantName": "release",
        "androidGradlePluginVersion": "2.0.0",
        "group": "verification",
        "description": "Runs lint on the Release build.",
        "didWork": false,
        "impliesSubProjects": false,
        "hasCustomActions": false,
        "enabled": true
      },
      "lintVitalRelease": {
        "variantName": "release",
        "androidGradlePluginVersion": "2.0.0",
        "description": "Runs lint on just the fatal issues in the Release build.",
        "didWork": false,
        "impliesSubProjects": false,
        "hasCustomActions": false,
        "enabled": true
      },
      "mergeReleaseAssets": {
        "variantName": "release",
        "androidGradlePluginVersion": "2.0.0",
        "outputDir": "**/Sample/app.main/build/intermediates/assets/release",
        "incrementalFolder": "**/Sample/app.main/build/intermediates/incremental/mergeReleaseAssets",
        "incremental": true,
        "didWork": false,
        "impliesSubProjects": false,
        "hasCustomActions": false,
        "enabled": true
      },
      "mergeReleaseJniLibFolders": {
        "variantName": "release",
        "androidGradlePluginVersion": "2.0.0",
        "outputDir": "**/Sample/app.main/build/intermediates/jniLibs/release",
        "incrementalFolder": "**/Sample/app.main/build/intermediates/incremental/mergeReleaseJniLibFolders",
        "incremental": true,
        "didWork": false,
        "impliesSubProjects": false,
        "hasCustomActions": false,
        "enabled": true
      },
      "mergeReleaseResources": {
        "variantName": "release",
        "androidGradlePluginVersion": "2.0.0",
        "buildToolsVersion": "23.0.1",
        "outputDir": "**/Sample/app.main/build/intermediates/res/merged/release",
        "incrementalFolder": "**/Sample/app.main/build/intermediates/incremental/mergeReleaseResources",
        "generatedPngsOutputDir": "**/Sample/app.main/build/generated/res/pngs/release",
        "blameLogFolder": "**/Sample/app.main/build/intermediates/blame/res/release",
        "useNewCruncher": true,
        "incremental": true,
        "crunchPng": true,
        "validateEnabled": true,
        "didWork": false,
        "minSdk": 9,
        "disableVectorDrawables": false,
        "impliesSubProjects": false,
        "hasCustomActions": false,
        "process9Patch": true,
        "enabled": true
      },
      "packageRelease": {
        "variantName": "release",
        "androidGradlePluginVersion": "2.0.0",
        "dexPackagingPolicy": "STANDARD",
        "resourceFile": "**/Sample/app.main/build/intermediates/res/resources-release.ap_",
        "markerFile": "**/Sample/app.main/build/intermediates/instant-run-support/release/package.marker",
        "outputFile": "**/Sample/app/smallLibs/x86/libnet_wequick_example_small_app_main.so",
        "minSdkVersion": 9,
        "incremental": false,
        "didWork": false,
        "jniDebugBuild": false,
        "impliesSubProjects": false,
        "hasCustomActions": false,
        "enabled": true
      },
      "prePackageMarkerForRelease": {
        "variantName": "release",
        "androidGradlePluginVersion": "2.0.0",
        "markerFile": "**/Sample/app.main/build/intermediates/instant-run-support/release/package.marker",
        "incremental": false,
        "didWork": false,
        "impliesSubProjects": false,
        "hasCustomActions": false,
        "enabled": true
      },
      "preReleaseBuild": {
        "didWork": false,
        "impliesSubProjects": false,
        "hasCustomActions": false,
        "enabled": true
      },
      "preReleaseUnitTestBuild": {
        "didWork": false,
        "impliesSubProjects": false,
        "hasCustomActions": false,
        "enabled": true
      },
      "prepareReleaseDependencies": {
        "variantName": "release",
        "androidGradlePluginVersion": "2.0.0",
        "didWork": false,
        "impliesSubProjects": false,
        "hasCustomActions": false,
        "enabled": true
      },
      "prepareReleaseUnitTestDependencies": {
        "variantName": "releaseUnitTest",
        "androidGradlePluginVersion": "2.0.0",
        "didWork": false,
        "impliesSubProjects": false,
        "hasCustomActions": false,
        "enabled": true
      },
      "processReleaseJavaRes": {
        "destinationDir": "**/Sample/app.main/build/intermediates/sourceFolderJavaResources/release",
        "caseSensitive": true,
        "includeEmptyDirs": true,
        "didWork": false,
        "impliesSubProjects": false,
        "hasCustomActions": false,
        "enabled": true
      },
      "processReleaseManifest": {
        "versionName": "1.0",
        "minSdkVersion": "9",
        "targetSdkVersion": "23",
        "variantName": "release",
        "androidGradlePluginVersion": "2.0.0",
        "manifestPlaceholders": "",
        "packageOverride": "net.wequick.example.small.app.main",
        "outputFile": "**/Sample/app.main/build/intermediates/manifests/full/release/AndroidManifest.xml",
        "manifestOutputFile": "**/Sample/app.main/build/intermediates/manifests/full/release/AndroidManifest.xml",
        "instantRunManifestOutputFile": "**/Sample/app.main/build/intermediates/bundles/release/instant-run/AndroidManifest.xml",
        "reportFile": "**/Sample/app.main/build/outputs/logs/manifest-merger-release-report.txt",
        "mainManifest": "**/Sample/app.main/src/main/AndroidManifest.xml",
        "versionCode": 1,
        "didWork": false,
        "impliesSubProjects": false,
        "hasCustomActions": true,
        "incremental": false,
        "enabled": true
      },
      "processReleaseResources": {
        "buildToolsVersion": "23.0.1",
        "variantName": "release",
        "androidGradlePluginVersion": "2.0.0",
        "packageForR": "net.wequick.example.small.app.main",
        "textSymbolOutputDir": "**/Sample/app.main/build/intermediates/symbols/release",
        "resDir": "**/Sample/app.main/build/intermediates/res/merged/release",
        "sourceOutputDir": "**/Sample/app.main/build/generated/source/r/release",
        "assetsDir": "**/Sample/app.main/build/intermediates/assets/release",
        "manifestFile": "**/Sample/app.main/build/intermediates/manifests/full/release/AndroidManifest.xml",
        "packageOutputFile": "**/Sample/app.main/build/intermediates/res/resources-release.ap_",
        "mergeBlameLogFolder": "**/Sample/app.main/build/intermediates/blame/res/release",
        "instantRunManifestFile": "**/Sample/app.main/build/intermediates/bundles/release/instant-run/AndroidManifest.xml",
        "debuggable": false,
        "pseudoLocalesEnabled": false,
        "didWork": false,
        "enforceUniquePackageName": true,
        "impliesSubProjects": false,
        "hasCustomActions": true,
        "incremental": false,
        "enabled": true
      },
      "processReleaseUnitTestJavaRes": {
        "destinationDir": "**/Sample/app.main/build/intermediates/sourceFolderJavaResources/test/release",
        "caseSensitive": true,
        "includeEmptyDirs": true,
        "didWork": false,
        "impliesSubProjects": false,
        "hasCustomActions": false,
        "enabled": true
      },
      "testReleaseUnitTest": {
        "executable": "/Library/Java/JavaVirtualMachines/jdk1.8.0_77.jdk/Contents/Home/bin/java",
        "group": "verification",
        "defaultCharacterEncoding": "US-ASCII",
        "description": "Run unit tests for the release build.",
        "workingDir": "**/Sample/app.main",
        "testClassesDir": "**/Sample/app.main/build/intermediates/classes/test/release",
        "binResultsDir": "**/Sample/app.main/build/test-results/binary/testReleaseUnitTest",
        "scanForTestClasses": true,
        "maxParallelForks": 1,
        "debug": false,
        "ignoreFailures": false,
        "didWork": false,
        "impliesSubProjects": false,
        "hasCustomActions": false,
        "enableAssertions": true,
        "enabled": true
      },
      "transformClassesWithDexForRelease": {
        "variantName": "release",
        "androidGradlePluginVersion": "2.0.0",
        "streamOutputFolder": "**/Sample/app.main/build/intermediates/transforms/dex/release",
        "didWork": false,
        "impliesSubProjects": false,
        "hasCustomActions": true,
        "enabled": true
      },
      "transformNative_libsWithMergeJniLibsForRelease": {
        "variantName": "release",
        "androidGradlePluginVersion": "2.0.0",
        "streamOutputFolder": "**/Sample/app.main/build/intermediates/transforms/mergeJniLibs/release",
        "didWork": false,
        "impliesSubProjects": false,
        "hasCustomActions": false,
        "enabled": true
      },
      "transformResourcesWithMergeJavaResForRelease": {
        "variantName": "release",
        "androidGradlePluginVersion": "2.0.0",
        "streamOutputFolder": "**/Sample/app.main/build/intermediates/transforms/mergeJavaRes/release",
        "didWork": false,
        "impliesSubProjects": false,
        "hasCustomActions": false,
        "enabled": true
      },
      "transformResourcesWithMergeJavaResForReleaseUnitTest": {
        "variantName": "releaseUnitTest",
        "androidGradlePluginVersion": "2.0.0",
        "streamOutputFolder": "**/Sample/app.main/build/intermediates/transforms/mergeJavaRes/test/release",
        "didWork": false,
        "impliesSubProjects": false,
        "hasCustomActions": false,
        "enabled": true
      },
      "uninstallRelease": {
        "variantName": "release",
        "androidGradlePluginVersion": "2.0.0",
        "group": "Install",
        "description": "Uninstalls the Release build.",
        "adbExe": "/Users/galen/Tools/android-sdk-macosx/platform-tools/adb",
        "timeOutInMs": 0,
        "didWork": false,
        "impliesSubProjects": false,
        "hasCustomActions": false,
        "enabled": true
      }
    }

    ```