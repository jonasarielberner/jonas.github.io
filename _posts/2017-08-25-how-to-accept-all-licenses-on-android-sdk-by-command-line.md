---
layout:     post
title:      "How to accept all licenses of Android SDK by CLI at once"
subtitle:   "Accepting all licenses of Android SDK sometimes comes in handy"
date:       2017-08-25 11:35:00
author:     "Cedulio Cezar"
tags: [programming,java,android]
summary: ""
comments: True
---
#### TL;DR

After configured an environment variable called ANDROID_HOME, run the following command.

```
yes | $ANDROID_HOME/tools/bin/sdkmanager --licenses
```

To Android Developers usually it is normal to accept licenses of Android SDK on GUI, however sometimes you need to do it by Command-line Interface because you are configuring a Continuous Integration(CI) for your project. And that can be a bit tricky.

## Use sdkmanager instead of android

Use to be normal to use the android binary file that comes with Android SDK, however nowadays if you do that you will receive an message telling you that android file deprecated to that task and you should be using sdkmanager as the following shows.

```

*************************************************************************
The "android" command is deprecated.
For manual SDK, AVD, and project management, please use Android Studio.
For command-line tools, use tools/bin/sdkmanager and tools/bin/avdmanager
*************************************************************************
```

To do it by using sdkmanager it is easier just type this command on your CLI after configuring an environment variable called $ANDROID_HOME pointing to your android sdk directory.

```
yes | $ANDROID_HOME/tools/bin/sdkmanager --licenses
```

## Accepting licenses on Jenkins

If you are using Jenkins and you do not have access to the console and yet need to accept the licenses, you can add an pre build Execute Shell task to do it for you, as the image shows:

<img src="{{ site.baseurl }}/img/posts/android-sdk-licenses/pre_build_execute_shell_task.PNG" alt="Pre build Execute Shell task example">{: .center-image }
