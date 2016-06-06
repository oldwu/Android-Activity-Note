# Activity异常情况的生命周期


## 当出现资源配置改变的时候，比如屏幕旋转或者是分辨率变化的时候，Activity会发生重建
1. onPause->onSavaInstanceState->onStop->onDestory
2. onCreate->onStart->onRestoreInstanceState->onResume
    
## 资源内存不足的时候低优先级的Activity被杀死，优先级由高到低：
* 前台Activity
* 可见非前台Activity，例如出现dialog的activity
* 后台Activity
    
## 配置Activity的android:configChanges，可以使得Activity在某些指定异常下不会重建
* 常用参数：
    1. locale           本地语言发生改变
    2. keyboardHidden   用户调出键盘
    3. orientation      屏幕方向方式改变，API13之后与screenSize同时使用，才能生效
    4. screenSize       屏幕尺寸信息发生改变，API13之后有效