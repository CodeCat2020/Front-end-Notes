

# 错误处理与调试





## 1. 浏览器报告的错误



### IE

### FireFox

### Safari

### Opera

### Chrome







## 2. 错误处理



### 2.1 try-catch语句



try... catch ... finally 用于处理 JavaScript 中的异常。



```js
try{
    // 可能会导致错误的代码
} catch(error){
    // 在错误发生时怎么处理
}
```



#### finally 子句



#### 错误类型

-  Error
-  EvalError
-  RangeError
-  ReferenceError
-  SyntaxError
-  TypeError
-  URIError



#### **合理使用 try-catch**





### 2.2 抛出错误

throw 操作符，用于随时抛出自定义错误。

#### 抛出错误的时机

#### 抛出错误与使用try-catch



### 2.3 error 事件

### 2.4 处理错误的策略



### 2.5 常见的错误类型

由于 JavaScript 是松散类型的，而且也不会验证函数的参数，因此错误只会在代码运行期间出现。一般来说，需要关注三种错误：

-  类型转换错误
-  数据类型错误
-  通信错误



- 





### 2.6 区分致命错误和非致命错误



### 2.7 把错误记录到服务器



## 3. 调试技术

### 将消息记录到控制台

### 将消息记录到当前页面

### 抛出错误







## 4. 常见的 IE 错误

























































