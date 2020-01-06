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
```

[更多](https://www.cnblogs.com/xiaohuochai/p/5777757.html)

###
