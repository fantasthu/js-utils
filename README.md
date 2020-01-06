# js-utils

### 封装重复点击

```js
const btn = document.querySelector('button')
btn.onclick = overTimeClick(() => {
	console.log(12)
}, 1000)

function overTimeClick(func, delay = 1000) {
	return (function() {
		var last = Date.now()
		return function() {
			var now = Date.now()
			console.log('now', now)

			if (now - last > delay) {
				func()
			}
			last = now
		}
	})()
}
```

### 类型数据判断

```javascript
Object.prototype.toString.call(obj).slice(8, -1) === 'String'
```

### 获取时分秒

```js
;/\d\d:\d\d:\d\d/.exec(new Date().toString())[0]
ps: **:**:**
```

[更多](https://www.cnblogs.com/xiaohuochai/p/5777757.html)

### 数组的合并

```js
var arr1 = []
var arr2 = []
arr1.push(...arr2)
```

- 伪数组转数组

```js
const fakeArr = document.querySelectorAll('div')
const Arr = [...fakeArr]
```

### 实现 bind 方法逻辑

```js
1.bind是绑定在方法上的
Function.prototype.myBind = function(){}
2.bind的返回值类型是function
Function.prototype.myBind = function(){
    return function(){}
}
3.bind 修改该方法的上下文对象,第二次运行此方法
Function.prototype.myBind = function (obj){
    return function(){
        const args = arguments.slice(0,-1)
        this.apply(obj,args)
    }
}
```
