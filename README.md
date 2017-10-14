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
