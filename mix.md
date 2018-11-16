```
-keepattributes Exceptions,InnerClasses,...
-keep class cn.yunzhisheng.oralEdu{*;}
-keep class cn.yunzhisheng.oraleval.sdk.OpusEncoder{*;}
-keep class com.unisound.jni.UniVadnn{*;}
-keep class com.unisound.edu.oraleval.sdk.sep15.IOralEvalSDK{*;}
-keep class com.unisound.edu.oraleval.sdk.sep15.IOralEvalSDK$*{*;}
-keep class com.unisound.edu.oraleval.sdk.sep15.OralEvalSDKFactory{*;}
-keep class com.unisound.edu.oraleval.sdk.sep15.OralEvalSDKFactory$*{*;}
-keep class com.unisound.edu.oraleval.sdk.sep15.SDKError{*;}
-keep class com.unisound.edu.oraleval.sdk.sep15.SDKError$*{*;}
-keep class com.unisound.edu.oraleval.sdk.sep15.OralEvalModel{*;}
-keep class com.unisound.edu.oraleval.sdk.sep15.utils.LogBuffer{*;}
-keep class com.unisound.edu.oraleval.sdk.sep15.utils.OralEvalEnum{*;}

-keepclassmembers enum * {
    public static **[] values();
    public static ** valueOf(java.lang.String);
}
```

> 说明：以上是SDK 混淆配置文件
