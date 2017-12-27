# 前端 javascript 经典题目
##一、闭包   
####1   
```
for (var i = 0; i < 5; i++) {
  setTimeout(function() {
    console.log(i);
  }, 1000 * i);
}   

```
####2   
```
for (var i = 0; i < 5; i++) {
  (function(i) {
    setTimeout(function() {
      console.log(i);
    }, i * 1000);
  })(i);
}   

```
####3   
```
for (var i = 0; i < 5; i++) {
  (function() {
    setTimeout(function() {
      console.log(i);
    }, i * 1000);
  })(i);
}   

```
####4   
```
for (var i = 0; i < 5; i++) {
  setTimeout((function(i) {
    console.log(i);
  })(i), i * 1000);
}   

```
###PS:附加一道promise   
####5   
```
setTimeout(function() {
  console.log(1)
}, 0);
new Promise(function executor(resolve) {
  console.log(2);
  for( var i=0 ; i<10000 ; i++ ) {
    i == 9999 && resolve();
  }
  console.log(3);
}).then(function() {
  console.log(4);
});
console.log(5);   

```
##二、this   
####6   
```
　　var name = "The Window";
　　var object = {
　　　　name : "My Object",
　　　　getNameFunc : function(){
　　　　　　var that = this;
　　　　　　return function(){
　　　　　　　　return that.name;
　　　　　　};
　　　　}
　　};
　　alert(object.getNameFunc()());
　　
```   
####7   
```
　　var name = "The Window";
　　var object = {
　　　　name : "My Object",
　　　　getNameFunc : function(){
　　　　　　return function(){
　　　　　　　　return this.name;
　　　　　　};
　　　　}
　　};
　　alert(object.getNameFunc()());

```
####8   
```
var obj = {
  id:'abc',
  foo:function fooFn(){
    console.log(this.id);
  }
}
var id = 'def';
obj.foo();
window.setTimeout(obj.foo,100);　　

```
##三、提升   
####9   
```
var x = 1;
var y = 0;
var z = 0;
function add(n) {
    n = n + 1;
}
y = add(x);
function add(n) {
    n = n + 3;
}
z = add(x);
s = y + z;

```
####10   
```
var x = 1;
var y = 0;
var z = 0;
function add(n) {
    return n = n + 1;
}
y = add(x);
function add(n) {
    return n = n + 3;
}
z = add(x);
s = y + z;

```
####11   
```
var x = function() {
    alert(0)
};
x();
var x = function() {
    alert(1)
};
x();   

```
####12   
```
function x() {
    alert(2)
};
x();
var x = function() {
    alert(0)
};
x();
var x = function() {
    alert(1)
};
x();
function x() {
    alert(3)
};
x();   

```
##四、原型   
####13   
```
var Per = function(){

}
var per1 = new Per();
var per2 = new Per();
per1.name = 'zhangsan';
Per.prototype={
    name:"lisi"
}
console.log(per1.name);  
console.log(per2.name);

```
