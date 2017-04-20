# activity四种启动方式
参考http://blog.csdn.net/liuhe688/article/details/6754323/
安卓activity的启动方式共四种
设置方式如下
![enter description here][1]
## 1.Standard:
startActivity(new Intent(StandardActivity.this,StandardActivity.class));
多次启动发现每次生成新的activity
![enter description here][2]![enter description here][3]
## 2.SingleTop
startActivity(new Intent(SingleTopActivity.this,SingleTopActivity.class));
发现自己启动自己时不会产生新的activity
![enter description here][4]![enter description here][5]
## 3.SingleTask
SingleTop由自己启动自己不会生成新的，但由其他activity启动会生成新的activity。
singleTask则不会
![enter description here][6]![enter description here][7]![enter description here][8]
singletop ->mainactivity->singletop
4.SingleInstance
发现SingleInstance会在一个新的acitivity栈中产生新的acitivity
Ttask id=36
 ![enter description here][9]![enter description here][10]
 
代码:
![enter description here][11]
Main:

```
findViewById(R.id.button).setOnClickListener(new View.OnClickListener() {
@Override
public void onClick(View v) {
startActivity(new Intent(MainActivity.this,StandardActivity.class));
}
});
findViewById(R.id.button2).setOnClickListener(new View.OnClickListener() {
@Override
public void onClick(View v) {
startActivity(new Intent(MainActivity.this,SingleTopActivity.class));
}
});
findViewById(R.id.button3).setOnClickListener(new View.OnClickListener() {
@Override
public void onClick(View v) {
startActivity(new Intent(MainActivity.this,SingleTaskActivity.class));
}
});
findViewById(R.id.button4).setOnClickListener(new View.OnClickListener() {
@Override
public void onClick(View v) {
startActivity(new Intent(MainActivity.this,SingleInstanceActivity.class));
}
});
```
StandardActivity:
```
((TextView)findViewById(R.id.textView)).setText(this.toString()+"\ncurrent task id: " + this.getTaskId());
findViewById(R.id.button).setOnClickListener(new View.OnClickListener() {
@Override
public void onClick(View v) {
startActivity(new Intent(StandardActivity.this,StandardActivity.class));
}

});
```
SingleTopActivity:
```
((TextView)findViewById(R.id.textView)).setText(this.toString()+"\ncurrent task id: " + this.getTaskId());
findViewById(R.id.button2).setOnClickListener(new View.OnClickListener() {
@Override
public void onClick(View v) {
startActivity(new Intent(SingleTopActivity.this,SingleTopActivity.class));
}

});
findViewById(R.id.button_main).setOnClickListener(new View.OnClickListener() {
@Override
public void onClick(View v) {
startActivity(new Intent(SingleTopActivity.this,MainActivity.class));
}

});
```
SingleTaskActivity:
```
((TextView)findViewById(R.id.textView)).setText(this.toString()+"\ncurrent task id: " + this.getTaskId());
findViewById(R.id.button_main).setOnClickListener(new View.OnClickListener() {
@Override
public void onClick(View v) {
startActivity(new Intent(SingleTaskActivity.this,MainActivity.class));
}

});
```
SingleInstanceActivity:
```
setContentView(R.layout.activity_singleinstance);
((TextView)findViewById(R.id.textView)).setText(this.toString()+"\ncurrent task id: " + this.getTaskId());
 ```
 
layout:
       main:
```
        <?xml version="1.0" encoding="utf-8"?>
<LinearLayout
xmlns:android="http://schemas.android.com/apk/res/android"
android:id="@+id/activity_main"
android:layout_width="match_parent"
android:layout_height="match_parent"
android:orientation="vertical">

    <Button
android:text="Standard"
android:layout_width="match_parent"
android:layout_height="wrap_content"
android:id="@+id/button"/>

    <Button
android:text="SingTop"
android:layout_width="match_parent"
android:layout_height="wrap_content" android:id="@+id/button2"/>

    <Button
android:text="SingTask"
android:layout_width="match_parent"
android:layout_height="wrap_content" android:id="@+id/button3"/>

    <Button
android:text="SingInstance"
android:layout_width="match_parent"
android:layout_height="wrap_content" android:id="@+id/button4"/>

</LinearLayout>
Standard:
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
xmlns:android="http://schemas.android.com/apk/res/android"
xmlns:tools="http://schemas.android.com/tools"
android:id="@+id/activity_standard"
android:layout_width="match_parent"
android:layout_height="match_parent"
tools:context="com.example.administrator.ex158.StandardActivity" android:orientation="vertical">

    <TextView
android:text="TextView"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:id="@+id/textView"/>

    <Button
android:text="Standard"
android:layout_width="wrap_content"
android:layout_height="wrap_content" android:id="@+id/button"/>

</LinearLayout>
Singletop
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
xmlns:android="http://schemas.android.com/apk/res/android"
xmlns:tools="http://schemas.android.com/tools"
android:id="@+id/activity_standard"
android:layout_width="match_parent"
android:layout_height="match_parent"
tools:context="com.example.administrator.ex158.StandardActivity" android:orientation="vertical">

    <TextView
android:text="TextView"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:id="@+id/textView"/>

    <Button
android:text="SingTop"
android:layout_width="wrap_content"
android:layout_height="wrap_content" android:id="@+id/button2"/>

    <Button
android:text="Main"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:id="@+id/button_main"/>

</LinearLayout>
Singletask:
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
xmlns:android="http://schemas.android.com/apk/res/android"
xmlns:tools="http://schemas.android.com/tools"
android:id="@+id/activity_standard"
android:layout_width="match_parent"
android:layout_height="match_parent"
tools:context="com.example.administrator.ex158.StandardActivity" android:orientation="vertical">

    <TextView
android:text="TextView"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:id="@+id/textView"/>

    <Button
android:text="Main"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:id="@+id/button_main"/>

</LinearLayout>
Singleinstance:
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
xmlns:android="http://schemas.android.com/apk/res/android"
xmlns:tools="http://schemas.android.com/tools"
android:id="@+id/activity_standard"
android:layout_width="match_parent"
android:layout_height="match_parent"
tools:context="com.example.administrator.ex158.StandardActivity" android:orientation="vertical">

    <TextView
android:text="TextView"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:id="@+id/textView"/>

</LinearLayout>
```
Androidmainifest:
```
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
package="com.example.administrator.ex158">


    <application
android:allowBackup="true"
android:icon="@mipmap/ic_launcher"
android:label="@string/app_name"
android:supportsRtl="true"
android:theme="@style/AppTheme">

        <activity android:name=".MainActivity">

            <intent-filter>

                <action android:name="android.intent.action.MAIN"/>


                <category android:name="android.intent.category.LAUNCHER"/>

            </intent-filter>

        </activity>

        <activity android:name=".SingleTopActivity" android:launchMode="singleTop"></activity>

        <activity android:name=".StandardActivity" android:launchMode="standard"></activity>

        <activity android:name=".SingleTaskActivity" android:launchMode="singleTask"></activity>

        <activity android:name=".SingleInstanceActivity" android:launchMode="singleInstance"></activity>

    </application>


</manifest>
```
项目在androidstudio2.2.1中建立,api为24


  [1]: ./images/1480485067191.jpg "1480485067191.jpg"
  [2]: ./images/1480485089168.jpg "1480485089168.jpg"
  [3]: ./images/1480485102617.jpg "1480485102617.jpg"
  [4]: ./images/1480485164610.jpg "1480485164610.jpg"
  [5]: ./images/1480485170850.jpg "1480485170850.jpg"
  [6]: ./images/1480485232717.jpg "1480485232717.jpg"
  [7]: ./images/1480485236253.jpg "1480485236253.jpg"
  [8]: ./images/1480485239694.jpg "1480485239694.jpg"
  [9]: ./images/1480485246257.jpg "1480485246257.jpg"
  [10]: ./images/1480485249663.jpg "1480485249663.jpg"
  [11]: ./images/1480485255313.jpg "1480485255313.jpg"