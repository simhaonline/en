### Copy Files
#### Copy jar files
Copy the following __jar__ files from `plugin/android/libs` folder of this
bundle into your project's __<project_root>/libs__ folder.

> billing-1.0.jar

> PluginIAP.jar

> sdkbox.jar


<<[../../shared/copy_jars.md]

<<[../../shared/copy_jni_lib.md]

### Edit `AndroidManifest.xml`
Include the following permissions above the __application tag__:
```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="com.android.vending.BILLING"/>
```

Include the following activity in the __application tag__:
```xml
<activity android:configChanges="keyboard|keyboardHidden|screenLayout|screenSize|orientation" android:name="com.android.billingclient.api.ProxyBillingActivity" android:theme="@android:style/Theme.Translucent.NoTitleBar" />
```

### Edit `Android.mk`
Edit `<project_root>/jni/Android.mk` to:

Add additional dependencies to __LOCAL_WHOLE_STATIC_LIBRARIES__:
```
LOCAL_WHOLE_STATIC_LIBRARIES += PluginIAP
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
$(call import-module, ./pluginiap)
```

This means that your ordering should look similar to this:
```
$(call import-add-path,$(LOCAL_PATH))
$(call import-module, ./sdkbox)
$(call import-module, ./pluginiap)
```

  __Note:__ It is important to make sure these statements are above the existing `$(call import-module,./prebuilt-mk)` statement, if you are using the pre-built libraries.

### Modify `Application.mk` (Cocos2d-x v3.0 - v3.2 only)
Edit `<project_root>/jni/Application.mk` to make sure __APP_STL__ is defined
correctly. If `Application.mk` contains `APP_STL := c++_static`, it should be
changed to:
```
APP_STL := gnustl_static
```
