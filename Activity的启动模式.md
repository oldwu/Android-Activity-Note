# Activity的启动模式

* 任务栈是一种"后进先出"的栈结构，当栈内无Activity的时候，系统就会回收这个栈

## 四种启动模式

### standard    标准模式
* 每次启动activity都会创建一个实例，不论实例是否存在
* 谁启动该Activity，该Activity就会进入那个任务栈
* 若启动Activity的是非Activity类型的，例如ApplicationContext，那在启动Activity的时候需要指定FLAG_ACTIVITY_NEW_TASK标记位，为其创建一个新的任务栈

### singleTop   栈顶复用模式
* 若新的Activity已经在栈顶，那么此Activity不会被重新创建，同时onNewIntent方法会被回调
* 已在栈顶的Activity的onCreate,onStart不会被系统调用
* 若不再栈顶，则新的Activity会被重建


### singleTask  栈内复用模式
* 单例模式， 只要Activity在任务栈中出现，就不会被创建，并且onIntent方法也会被回调
* 当需要启动的Activity所需的任务栈不存在的时候，会先创建一个任务栈，在将Activity创建后放入栈中，此时Activity按照标准的生命流程
* singleTask 默认clearTop，即Activity存在于任务栈中时，若启动，会将该Activity之上的Activity全部出栈，例如ADBC，singleTask启动D，任务栈中变成AD

### singleInstance  单实例模式
* 加强的singleTask模式，包含singleTask的全部特性
* 除此之外，就是Activity只能单独地位于一个任务栈中，例如A是启动模式是singleInstance，启动A，系统会为A创建一个任务栈，并将A放置其中，除非任务栈被销毁，否则后续的请求不会再创建新的Activity
    
### TaskAffinity
* 标识了任务栈的名称，默认状态下为应用的包名，也可以在Manifest中手动给Activity设置，android:taskAffinity，相当于手动指定任务栈

### Activity的Flags
* FLAG_ACTIVITY_NEW_TASK    singleTask
* FLAG_ACTIVITY_SINGLE_TOP  singleTop
* FLAG_ACTIVITY_CLEAR_TOP   启动Activity时，位于它之上的Activity全部清除


