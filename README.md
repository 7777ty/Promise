# Promise
① Promise的用途
② 如何创建一个new Promise
③ 如何使用Promise.prototype.then
④ 如何使用Promise.all
⑤ 如何使用Promise.race

1. Promise对象是一个代理对象（代理一个值），被代理的值在Promise对象创建时可能时未知的。它允许你为异步操作的的成功和失败分别绑定相应的处理方法。这让异步方法可以像同步方法那样返回值。

2. 
```javascript
return new Promise((resolve,reject)=>{...})
```
3. then()方法返回一个Promise。它作用是为 Promise 实例添加状态改变时的回调函数。前面说过，then方法的第一个参数是resolved状态的回调函数，第二个参数（可选）是rejected状态的回调函数。
```javascript
var p1=new Promise((resolve,reject)=>{
    resolve('成功')；
    //or
    //reject(new Error('出错了'));
});
p1.then(
    value=>{
        console.log(value);
    },reson=>{
        console.error(reson);
    }
);
```

4. **Promise.all(iterable)** 方法返回一个Promise实例，此实例在iterable参数内所有的Promise都“完成（resolved）”或参数中不包含Promise时回调完成（resolve）；如果参数中promise有一个失败（rejected），此实例回调失败，失败原因的是第一个失败 promise 的结果。
```javascript
var p1 = Promise.resolve(3);
var p2 = 1337;
var p3 = new Promise((resolve,reject)=>{
    setTimeout(resolve,100,'foo')
});
Promise.all([p1,p2,p3]).then(value=>{
    console.log(value);//[3,1337,'foo']
})
```

5. **Promise.race(iterable)** 方法返回一个 promise，一旦迭代器中的某个promise解决或拒绝，返回的 promise就会解决或拒绝。
```javascript
var p1 = new Promise(function(resolve,reject){
    setTimeout(resolve,500,"one");
});
var p2 = new Promise(function(resolve,reject){
    setTimeout(resolve,100,"two");
});
Promise.race([p1,p2]).then(function(value){
    console.log(value);//"two"
    //两个都完成，但P2更快
})
```