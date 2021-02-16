[TOC]

# Nim 精简指南

## Part1

hello world

```nim
echo "hello world!"
```

### 变量声明

```nim
var
  x, y: int   # 同类型
  a, b, c: string  # 多行声明
var x, y = 3 # 自动类型推导

const
  x = 1
  y = 2
  z = y + 5 # 表达式编译期计算

let x = "abc"  # let只可以单行赋值
x = "xyz"  # 错误,let变量不可更改值
```

#### `let`

只可以单行声明，且变量值不可改变

#### `const`

可多行声明，表达式必须编译期可计算

#### `var`

常规可变变量声明



### 编译命令

`nim compile --run greetings.nim`

#### 带参数运行

`nim compile --run greetings.nim arg1 arg2`





## Part 2

### template

```nim
import math

template liftScalarProc(fname) =
  proc fname[T](x: openarray[T]): auto =
    var temp: T
    type outType = typeof(fname(temp))
    result = newSeq[outType](x.len)
    for i in 0..<x.len:
      result[i] = fname(x[i])

liftScalarProc(sqrt) 
echo sqrt(@[4.0, 16.0, 25.0, 36.0]) 

```

template 通过在**编译时**的简单替换操作语法树.