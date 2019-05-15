## C#中using的三种使用方式
### 1.using 命名空间
引用命名空间，如：using System；这样声明即可在程序内直接使用命名空间中的类型，而不用指定类型的详细命名空间。
### 2.using 别名
为命名空间或类创建别名。例：using 别名 = System.IO;
用于解决命名冲突问题
### 3.using 语句
using 语句允许程序员指定使用资源的对象应当何时释放资源。using 语句中使用的对象必须实现 IDisposable 接口。此接口提供了 Dispose 方法，该方法将释放此对象的资源。
适用于对单个类型资源释放的管理，多个类型还是使用try/catch更佳。
using语句实质上是编译器自动生成了try/catch代码。在finally中调用类型的Dispose方法。