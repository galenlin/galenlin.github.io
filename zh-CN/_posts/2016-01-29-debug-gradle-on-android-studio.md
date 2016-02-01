---
layout: post
title:  "Android Studio 调试 Gradle"
date:   2016-01-29 16:36:03
categories: android
tags: [android, gradle]
---

1. 创建调试器

    Run->Edit Configurations<br/>
    ![Edit configurations](/images/debug-gradle-1.png)

    Add New Configuration<br/>
    ![Add New Configuration](/images/debug-gradle-2.png)

    Add Remote configuration<br/>
    ![Add Remote configuration](/images/debug-gradle-3.png)

2. 开启调试模式
    
    ```
    $ export GRADLE_OPTS="-Xdebug -Xrunjdwp:transport=dt_socket,server=y,suspend=y,address=5005"
    ```

3. 启动任务

    ```
    $ ./gradlew someTask -Dorg.gradle.daemon=false #!important, disable daemon mode
    ```

4. 启动调试器

    Set breakpoints<br/>
    ![Add Remote configuration](/images/debug-gradle-6.png)

    Start debug<br/>
    ![Add Remote configuration](/images/debug-gradle-7.png)

5. 关闭调试模式

    ```
    $ unset GRADLE_OPTS
    ```