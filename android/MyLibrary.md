gradle根目录
```
allprojects {
    repositories {
        maven { url "https://jitpack.io" }
        jcenter()
    }
}
```
gradle app文件
```
    compile 'com.github.cai1449074828:myLibrary:2.2'
    compile 'com.jakewharton:butterknife:7.0.1'
    compile 'com.android.support.constraint:constraint-layout:1.0.0-beta2'
    compile 'com.ashokvarma.android:bottom-navigation-bar:1.3.0'
    compile 'com.flyco.tablayout:FlycoTabLayout_Lib:2.0.6@aar'
    compile 'de.hdodenhof:circleimageview:2.1.0'
    compile 'com.android.support:cardview-v7:23.4.0'
    //加载图片
    compile 'com.github.bumptech.glide:glide:3.7.0'
    //鸿洋大神的okhttp
    compile 'com.zhy:okhttputils:2.6.2'
    compile 'com.google.code.gson:gson:2.8.0'
    compile 'com.luffykou:android-common-utils:1.1.3'
```