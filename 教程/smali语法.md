## smali语法

### 数据类型

| smali          | Java                                                         |
| -------------- | ------------------------------------------------------------ |
| V              | void（返回值的数据类型）                                     |
| Z              | Boolean                                                      |
| B              | Byte                                                         |
| S              | short                                                        |
| C              | Char                                                         |
| I              | int                                                          |
| J              | long                                                         |
| F              | float                                                        |
| D              | double                                                       |
| [类型          | 数组 <br />[I表示一个int型数据<br />[Ljava/lang/String 表示一个String的对象数组 |
| Lpackage/name; | 对象类型 L表示这是一个对象类型<br />package表示该对象所在的包<br />；表示对象名称的结束 |



### 语法关键字

| 关键词          | 说明                                                         |
| --------------- | ------------------------------------------------------------ |
| .class          | 定义Java类的名字                                             |
| .super          | 定义父类类名                                                 |
| .source         | 定义Java源文件                                               |
| .field          | 定义字段（就是局部变量名的声明）<br />.field <访问权限> <变量名>:<变量类型><br />.field actionBar:Landroid/app/ActionBar; <br /><=><br />ActionBar actionBar; |
| .method         | 方法的开始                                                   |
| .end method     | 方法的结束                                                   |
| .annotation     | 注释的开始                                                   |
| .end annotation | 注释的结束                                                   |
| .implements     | 定义接口指令                                                 |
| .local          |                                                              |
| .line N关键字   | line N代表其下代码还原成java代码在源文件第N行 <br />.line 3<br />const/4 v0 0x01<br />iput v0,p0,LTest;->a:I |
| .prologue       | 表示函数的代码逻辑从这一行开始<br />.method public Test()V<br/>    .registers N<br/>    .prologue<br/>    #do-something<br/>    return-void<br/>.end method |
| .registers      | 指定方法内使用寄存器的总数<br />同高级编程语言将数据存入内存时刻调用实现变量存储不同<br />smali语言类似汇编<br />将所有的变量和常量都使用寄存器存储<br />因此，为了在函数的开头便将需要用到的寄存器入栈<br />（其他函数也会用到寄存器，先将寄存器中原本的值入栈，在使用完毕后出栈，以保证当前函数对寄存器的使用不会导致其他函数存储在寄存器中的值被破坏），在一个函数内部的变量个数应当尽量少，并且总数必须在函数的开头声明。<br/> |
| .prologue       | 表示java源文件中指定行                                       |
| .paramter       | 指定了方法的参数                                             |
|                 |                                                              |
|                 |                                                              |
|                 |                                                              |
|                 |                                                              |

