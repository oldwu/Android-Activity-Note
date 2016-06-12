# IntentFilter的匹配规则

启动Activity的方式有两种，显式调用和隐式调用，原则上两种调用不同使用，同时使用的时候，优先调用显式调用

显式调用为JAVA代码调用的方式，隐式调用为manifest编写xml

## 三种匹配规则

action category data  
只有同时匹配过滤列表中的action, category, data才算是的匹配成功  
一个Activty可以拥有多个intent-filter, 只要能匹配任何一组intent-filter,就可以启动对应的Activity

### action
* 一个字符串，系统预定义了一些action
* 也可以在应用中定义自己的action
* 匹配规则：Intent中的action必须能够和过滤规则中的action匹配，及字符串值完全一样，且Intent中的action只要有一个且*至少要有一个*和intent-filter中的任何一个action相同及匹配成功
* 匹配过程区分大小写

### category
* 一个字符串，系统预定义了一些category
* 也可以在应用中定义自己的category
* 匹配规则：Intent中的category必须能够和过滤规则中的category匹配，及字符串值完全一样，且Intent中的*所有category*要和intent-filter中的任何一个category相同才算做匹配成功
* 匹配过程区分大小写
* 系统默认加上了"android:intent.category.DEFAULT", 因此要想隐式调用，就必须在intent-filter中加入"android:intent.category.DEFAULT"

### data
* 匹配规则类似于action
* 由两部分组成，mimeType和URI，前者指媒体类型，后者是URI模式和路径  
URL结构：
```
<scheme>://<host>:<port>/[<path>|<pathPrefix>|<pathPattern>]
```
* schemem默认值:file/content


#### 例子
1. manifest 
``` xml
<activity android:name=".IntentActivity">
    <intent-filter>
        <action android:name="com.wzy.touchtest.c"/>
        <action android:name="com.wzy.touchtest.d"/>
        <category android:name="com.wzy.touchtest.c"/>
        <category android:name="com.wzy.touchtest.d"/>
        <category android:name="android.intent.category.DEFAULT"/>
        <data android:mimeType="text/plain"/>
    </intent-filter>
</activity>
```

2. Intent的编写
```java
Intent intent = new Intent("com.wzy.touchtest.c");
intent.addCategory("com.wzy.touchtest.c");
intent.addCategory("com.wzy.touchtest.d");
intent.setDataAndType(Uri.parse("file://abc"), "text/plain");
startActivity(intent);
```
