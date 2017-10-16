### 输入一个数组，返回一个内容打乱的新数组
思路：  
- 定义一个新数组
- 内容顺序打乱 —— 生成数组长度的随机数
- 处理生成的随机数代表的位置已经填充了元素 
```js
function getRandomSortArr(arr) {
  // 定义新数组
  var newArr = [],
      len = arr.length || 0;
  
  // 获取随机数
  function random(length) {
    return Math.floor(Math.random() * length);
  }
  
  for (var i = 0; i < len; i++) {
    var order = random(len);
    // 当产生的随机数在newArr中有已经填充了元素时，进行相应的处理
    if (newArr[order]){
      while(newArr[order]) {
        order++;
        if (order >= len) {
          order = 0;
        }
      } 
    }
    // 返回新数组
    newArr[order] = arr[i];
  }
  return newArr;
}

var arr = [1,2,3,4,5];
console.log(getRandomSortArr(arr));
```

### 实现一个debounce函数
debounce函数就是在delay时间内，如果多次调用fn函数，则fn函数也只执行一次
思路：
- 要用到setTimeout
- 当多次调用时，要取消定时器，然后重新开启一个新的定时器，那么就需要保留
定时器的id，也就是timer，当取消定时器时，就clearTimeout(timer)，
因此可以通过返回一个闭包来保留timer
```js
function debounce(fn, delay) {
  var timer ;
  return function() {
    var context = this;
    var args = arguments;
    clearTimeout(timer);
    timer = setTimeout( () => {
      fn.apply(context, args);
    }, delay);
  }
}
```
