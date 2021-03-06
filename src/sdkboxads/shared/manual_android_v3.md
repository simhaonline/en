### Copy Files
Copy the following __jar__ files from `plugin/android/libs` folder of this
bundle into your project's __<project_root>/libs__ folder.

> PluginSdkboxAds.jar

> sdkbox.jar


<<[../../shared/copy_jars.md]

Copy the `sdkboxads_lib` directories from `plugin/android/libs` to your `<project_root>/libs/` directory.

<<[../../shared/copy_jni_lib.md]


### Edit `AndroidManifest.xml`
Include the following permissions above the __application tag__:
```xml
  <uses-permission android:name="android.permission.INTERNET" />
```

### Edit `Android.mk`
Edit `<project_root>/jni/Android.mk` to:

Add additional requirements to __LOCAL_WHOLE_STATIC_LIBRARIES__:
```
LOCAL_WHOLE_STATIC_LIBRARIES += PluginSdkboxAds
LOCAL_WHOLE_STATIC_LIBRARIES += sdkbox
```

Add a call to:
```
$(call import-add-path,$(LOCAL_PATH))
```
before any __import-module__ statements.

Add additional __import-module__ statements at the end:
```
$(call import-module, ./sdkbox)
$(call import-module, ./pluginsdkboxads)
```

This means that your ordering should look similar to this:
```
$(call import-add-path,$(LOCAL_PATH))
$(call import-module, ./sdkbox)
$(call import-module, ./pluginsdkboxads)
```

  __Note:__ It is important to make sure these statements are above the existing `$(call import-module,./prebuilt-mk)` statement, if you are using the pre-built libraries.

### Modify `Application.mk` (Cocos2d-x v3.0 to v3.2 only)
Edit `<project_root>/jni/Application.mk` to make sure __APP_STL__ is defined
correctly. If `Application.mk` contains `APP_STL := c++_static`, it should be
changed to:
```
APP_STL := gnustl_static
```


### Important

For each AdUnit, you have to add:

JNI:

All AdUnit's JNI library contents.

Manifest:

All changes needed by each AdUnit's plugin.

__jar__:

Jar files necessary for included AdUnits. Basically all jar files present in the Plugin's lib folder.



__LOCAL_WHOLE_STATIC_LIBRARIES__ the module references for each of them, e.g.:

```
LOCAL_WHOLE_STATIC_LIBRARIES += pluginvungle
LOCAL_WHOLE_STATIC_LIBRARIES += pluginadcolony
```

Android.mk __import-module__:

```
$(call import-module, ./pluginadcolony)
$(call import-module, ./pluginvungle)
```
