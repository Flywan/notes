####正文：
最近遇到一个问题，在更改Android的系统应用时，要引用一个aar文件。之前引用的主要是jar包，而aar文件包含Android的资源文件，如：布局、样式、图片等，如果按照源码中jar的引用方式会遇到编译不过的问题，提示找不到相关的资源文件。

国内的相关论坛也有同行遇到相同的问题，不过相关的解决方案并没有，不过在stackoverflow有相关的解决方案，网址如下：
[aar-support-in-android-mk: http://stackoverflow.com/questions/31205856/aar-support-in-android-mk](http://stackoverflow.com/questions/31205856/aar-support-in-android-mk)

```
LOCAL_STATIC_JAVA_AAR_LIBRARIES:= <aar alias>
.
.
.
include $(BUILD_PACKAGE)

include $(CLEAR_VARS)

LOCAL_PREBUILT_STATIC_JAVA_LIBRARIES := <aar alias>:libs/<lib file>.aar

include $(BUILD_MULTI_PREBUILT)
```
其中，`LOCAL_PREBUILT_STATIC_JAVA_LIBRARIES := <aar alias>:libs/<lib file>.aar` 也可以如下面这样写：
```
include $(CLEAR_VARS)
LOCAL_MODULE := <aar alias>
LOCAL_SRC_FILES := <lib file>.aar
LOCAL_MODULE_CLASS := JAVA_LIBRARIES
LOCAL_MODULE_SUFFIX := $(COMMON_JAVA_PACKAGE_SUFFIX)
LOCAL_BUILT_MODULE_STEM := javalib.jar
include $(BUILD_PREBUILT)
```
这里主要是LOCAL_STATIC_JAVA_AAR_LIBRARIES，剩下的和jar包大同小异，注意在manifest文件里minSdkVersion要满足aar文件的要求。

搜索Android源码，也可以发现：
>\#LOCAL_STATIC_JAVA_AAR_LIBRARIES are special LOCAL_STATIC_JAVA_LIBRARIES
>LOCAL_STATIC_JAVA_LIBRARIES := $(strip $(LOCAL_STATIC_JAVA_LIBRARIES) $(LOCAL_STATIC_JAVA_AAR_LIBRARIES))

这一步完成后，代码可以顺利编译过了，不过在运行apk时如果使用到aar文件里面的资源可能会crash，所以还需要加上以下语句：
```
LOCAL_AAPT_FLAGS := \
  --auto-add-overlay \
  --extra-packages <aar package name>
```
 关于LOCAL_AAPT_FLAGS，可以参考以下网址，在开发Android系统应用时可能会遇到和这个相关的一些小坑，比如修改完相关代码后，push进机器却不起作用。
 
 [Android AAPT and Overlay: http://blog.csdn.net/sunny09290/article/details/20943261](http://blog.csdn.net/sunny09290/article/details/20943261)

这里把相关aar文件的资源打包到我们的apk里，apk即可正常运行。

另外一点是在make文件中可以指定具体的manifest文件：
`LOCAL_MANIFEST_FILE := <manifest file path>`

####参考链接： 
[Android AAPT and Overlay: http://blog.csdn.net/sunny09290/article/details/20943261](http://blog.csdn.net/sunny09290/article/details/20943261)
[aar-support-in-android-mk: http://stackoverflow.com/questions/31205856/aar-support-in-android-mk](http://stackoverflow.com/questions/31205856/aar-support-in-android-mk)
[Android4.4 Makefile属性：LOCAL_AAPT_FLAGS的使用: http://blog.csdn.net/visionliao/article/details/43233743](http://blog.csdn.net/visionliao/article/details/43233743)

