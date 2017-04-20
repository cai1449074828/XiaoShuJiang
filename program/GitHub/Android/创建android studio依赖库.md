github.exe
github首页创建repository
![enter description here][1]
 github.exe clone repository
![enter description here][2]
/***************重点
![enter description here][3]
 
 修改两个
project的build.gradle
```
buildscript {
dependencies {
classpath 'com.github.dcendents:android-maven-gradle-plugin:1.5'
}
}
```
mylibrary的build.gradle
```
apply plugin: 'com.github.dcendents.android-maven'
group='com.github.cai1449074828'
```
***************重点/
把项目复制进入clone repository
![enter description here][4]
 删除app文件留下mylibrary
github网页去发布(releases)
![enter description here][5]
 
https://jitpack.io/
 ![enter description here][6]
 


  [1]: ./images/1480485506405.jpg "1480485506405.jpg"
  [2]: ./images/1480485510356.jpg "1480485510356.jpg"
  [3]: ./images/1480485515866.jpg "1480485515866.jpg"
  [4]: ./images/1480485549821.jpg "1480485549821.jpg"
  [5]: ./images/1480485557320.jpg "1480485557320.jpg"
  [6]: ./images/1480485566573.jpg "1480485566573.jpg"