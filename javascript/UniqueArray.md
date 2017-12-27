
## 数组去重的几种解决方案
```
var arr = [1,2,2,3,4,6,6,6,8]
var uniqueArr = [];
toUnique(arr);
```
####一、indexOf法

```
function toUnique(testArr){
    for(var i=0;i<testArr.length;i++){
        if(uniqueArr.indexOf(arr[i])==-1){
            uniqueArr.push(arr[i]);
        }
    }
    console.log(uniqueArr);
}
```

####二、双重for循环法
```
function toUnique(testArr) {
    for(var i=0; i<testArr.length; i++){
        for(var j=i+1; j<testArr.length; j++){
            if(testArr[i] === testArr[j]){
                j = ++i;
            }
        }
        uniqueArr.push(testArr[i]);
    }
    console.log(uniqueArr);
}
```

####三、ES6 includes法
```
function toUnique(testArr){
    for(var i=0;i<testArr.length;i++){
        if(!uniqueArr.includes(testArr[i])){
            uniqueArr.push(testArr[i]);
        }
    }
    console.log(uniqueArr);
}
```

####四、利用对象的key唯一
```
function toUnique(testArr) {
    var obj = {};
    for(var i=0; i<testArr.length; i++){
        if(!obj[testArr[i]]){
            obj[testArr[i]] = 1;
            uniqueArr.push(testArr[i]);
        }
    }
    console.log(uniqueArr);
}
```
####五、利用ES6的Map
```
function toUnique(testArr){
    var obj = new Map();
    for(var i=0; i<testArr.length; i++){
        if(!obj.get(testArr[i])){
            obj.set(testArr[i], 1);
            uniqueArr.push(testArr[i]);
        }
    }
    console.log(uniqueArr);
}
```

####六、利用ES6的Set
```
function toUnique(testArr){
    var set = new Set(testArr);
    console.log(Array.from(set));
}
```
