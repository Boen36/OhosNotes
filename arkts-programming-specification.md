# ArkTS编程规范

ArkTS类名，枚举名，命名空间采用UpperCamelCase风格

常量名，枚举值采用大写，单词间采用下划线分隔

多个变量和赋值语句不允许写在一行，每个变量一行更有利于代码调试

必须使用`Number.isNaN`来判断一个值是否为`Number.NaN`，Number.NaN不等于任何值，包括它本身

遍历数组时，优先使用Array对象，例如forEach，map，find，findIndex，filter, every, some, reduce

在finally代码块中，不要使用return, break，continue或抛出异常，因为这样会导致finally块异常结束，必须确保finally代码块正常结束

避免使用ESObject，因为ESObject是ArkTS和JS/TS跨语言调用场景中的类型标注，在非跨语言调用场景中使用ESObject会造成不必要的开销

建议使用`T[]`来表示数组类型，而不是`Array<T>`，提高代码可读性 `let a: number[] = [1, 2, 3]`
