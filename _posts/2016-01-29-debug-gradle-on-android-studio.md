---
layout: post
title:  "Debug gradle on android studio"
date:   2016-01-29 16:36:03
categories: gradle
---

1. Create debugger
     Run->Edit Configurations

2. Open debug mode
     $ export GRADLE_OPTS="-Xdebug -Xrunjdwp:transport=dt_socket,server=y,suspend=y,address=5005"
3. Start debugger
     ./gradlew someTask -Dorg.gradle.daemon=false #!important, disable daemon mode
4. Attach debugger

5. Off debug mode
     $ unset GRADLE_OPTS