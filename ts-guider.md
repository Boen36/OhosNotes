# TypeScript到ArkTS适配指导

为了确保程序的正确性，动态语言需要在运行时检查对象类型，例如js不允许访问undefined的属性，这个操作只能在运行时完成。TS代码总是被编译为js代码，因此也会遇到同样的问题。在ArkTS中采用严格的静态类型系统，并且编译为方舟字节码，因此运行速度更快更稳定

ArkTS中，对象的属性名不能为数字和字符串，例如`let a = {'name': boen, 2: '3'}`这是不允许的

ArkTS不支持以#开头的私有字段

var是函数作用域，不受代码块限制，let是块级作用域，只在最近的一对{}内有效。现在主流语言都采用块级作用域，函数作用域的范围过大，不确定性更高。块级作用域更小，更精细

var声明的变量会被提升到作用域顶部，并且会初始化为undefined，因此不存在暂时性死区，可以在var变量声明之前使用
let声明的变量同样会被提升到作用域顶部，但是不会有初始化的操作，因此在声明之前使用它是非法的，会报错

ArkTS不支持unknown

ArkTS不支持call signature，call signature可以让对象像函数一样直接被调用

ArkTS 不支持 intersaction type，使用继承代替

```
interface A {}
interface B {}
type AB = A & B // 不支持
interface AB extends A, B {} // 可以使用继承代替
```

ArkTS 不支持this类型，该用具体类型代替

ArkTS不支持通过索引访问对象字段，类数组对象可以使用索引访问

类或接口中存在方法，readonly属性，any/Object/object类型的属性，自定义参数构造函数时，无法使用对象字母量初始化类或接口

ArkTS不支持函数表达式，可以使用箭头函数代替
```
let f = () => {}
```

ArkTS类型转换只支持as语法

ArkTS禁止隐式地将字符串转换为数值

ArkTS中，instanceof 左操作数必须为 引用类型

ArkTS不支持in运算符

ArkTS不支持解构赋值

ArkTS中catch语句中不支持标记类型
```
try {} catch(e) {}
```

ArkTS不支持for-in语法，不支持with语句

ArkTS只支持throw Error获取派生类，不支持抛出其他类型

ArkTS不支持在函数内声明函数，改用箭头函数

ArkTS接口只能继承接口

ArkTS中命名空间仅用于定义标识符的可见范围，只在编译时有效

ArkTS不支持require，例如`import m = require(moduleA)`，只能使用正常import语句

ArkTS没有原型的概念

ArkTS不支持全局作用域和GlobalThis

ArkTS仅支持Partial(部分的)， Required，ReadOnly，Record这些Utility Types
```
interface User {
    name: string
    age: number
}
type PartialUser = Partial<User> // 将所有属性变为可选属性 name?: string; age?: number
type RequiredUser = Required<User>
type ReadOnlyUser = ReadOnly<User>
```

ArkTS禁止使用Function.apply和Function.call和Function.bind，因为ArkTS严格遵循传统的OOP风格，函数中无法使用this

ArkTS不允许通过注释关闭编译时的类型检查

除动态import外，所有的import语句需要在文件顶部
