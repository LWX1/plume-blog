---
title: 高级类型（接口、泛型）
createTime:  2020-07-10T00:00:00.000Z
isShowComments: false
date:  2025/06/03 20:01:27
permalink: /article/0uienjkp/

---

# 接口
## 介绍
接口对值所具有的结构进行类型检查，并规定其一定得拥有这部分数据。不可拥有其他数据

## 变量接口

```
interface person{
    readonly name: string, // 只读属性，确定了值就不可更改
    age: number,
    sex?:boolean // 表示可选参数
}
let xm:person = {
    name: '小明',
    age: 18,
    sex: true,
    money: 200 // 没有改属性，报错
}
```

## 函数接口
```
interface person{
    readonly name: string,
    age: number,
    sex?:boolean
}

function getPerson(params:person):number { // 声明函数参数为接口，返回值为数字
    console.log(params)
    params.name = '小区'; // 只读属性，报错
    params.age = 20;
    return 1
}

getPerson({name: '笑话', sex: true, age: 1})
```

## 类接口

```
interface person{
    readonly name: string,
    age: number,
    sex?:boolean
}

class getPerson implements person{
    name: '小明';
    age: 19
    constructor() {
         this.age  =10; // 报错
        this.name = '小明'; // 报错
    }
}

```
## 继承接口
```
interface person{
    readonly name: string,
    age: number,
    sex?:boolean
}

interface work extends person {
    morning: string
}

let obj:work = {
    name: '小绿',
    morning: '早上',
    age: 11
}
```

# 泛型

## 介绍
为了创建一致的定义良好的API，同时也要考虑可重用性。组件不仅能够支持当前的数据类型，同时也能支持未来的数据类型，这时就需要使用泛型了。

## 基本泛型
```
function loggingIdentity<T>(arg: Array<T>): Array<T> {
    console.log(arg.length);  
    return arg;
}
```
## 多变量泛型
```
function identity <T, U>(value: T, message: U) : [T,U] {
    console.log(message);
    return [value,message];
  }
  
  console.log(identity<Number, string>(10, "a"));
```