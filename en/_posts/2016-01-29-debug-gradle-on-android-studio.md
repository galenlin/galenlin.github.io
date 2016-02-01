---
layout: post
title:  "Debug gradle on android studio"
date:   2016-01-29 16:36:03
categories: android
tags: [android, gradle]
---

1. Create debugger

    Run->Edit Configurations<br/>
    ![Edit configurations](/images/debug-gradle-1.png)

    Add New Configuration<br/>
    ![Add New Configuration](/images/debug-gradle-2.png)

    Add Remote configuration<br/>
    ![Add Remote configuration](/images/debug-gradle-3.png)

2. Open debug mode
    
    ```
    $ export GRADLE_OPTS="-Xdebug -Xrunjdwp:transport=dt_socket,server=y,suspend=y,address=5005"
    ```

3. Start debugger

    ```
    $ ./gradlew someTask -Dorg.gradle.daemon=false #!important, disable daemon mode
    ```

4. Attach debugger

    Set breakpoints<br/>
    ![Add Remote configuration](/images/debug-gradle-6.png)

    Start debug<br/>
    ![Add Remote configuration](/images/debug-gradle-7.png)

5. Disable debug mode

    ```
    $ unset GRADLE_OPTS
    ```