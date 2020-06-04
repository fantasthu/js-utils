# js-utils

### 封装重复点击

```javascript
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

### 滚动到顶部函数

```javascript
top.addEventListener('click', function() {
	aniToTop()
})
function aniToTop() {
	// 距离顶部的位置
	var offset = document.body.scrollTop || document.documentElement.scrollTop
	// 初函数值
	var a = 2,
		x = 0,
		y = 0
	update()
	function update() {
		y = offset - a * Math.pow(x, 2)
		scrollTo(0, y)
		if (y <= 0) {
			cancelAnimationFrame(update)
			return
		}
		x++
		requestAnimationFrame(update)
	}
}
```

### 获取时分秒

```javascript
;/\d\d:\d\d:\d\d/.exec(new Date().toString())[0]
ps: **:**:**
```

[更多](https://www.cnblogs.com/xiaohuochai/p/5777757.html)

### 数组的合并

```javascript
var arr1 = []
var arr2 = []
arr1.push(...arr2)
```

- 伪数组转数组

```javascript
const fakeArr = document.querySelectorAll('div')
const Arr = [...fakeArr]
```

### 实现 bind 方法逻辑

```javascript
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

### 加入某个元素

```javascript
function appendTo(el, parent) {
	parent.appendChild(el)
}
```

### 获取兄弟元素

```javascript
function siblings(el) {
	return Array.prototype.filter.call(el.parentNode.children, function(child) {
		return child !== el
	})
}
```

### 获取下一个元素

```javascript
function next(item) {
	return item.nextElementSibling
}
```

### 获取前一个元素

```javascript
function pre(item) {
	return item.previousElementSibling
}
```

### 是否存在 className

```javascript
function hasClass(el, className) {
	if (el == null) {
		return false
	}
	if (el.classList) {
		return el.classList.contains(className)
	}
	return new RegExp('(^| )' + className + '( |$)', 'gi').test(el.className)
}
```

### 添加 class

```javascript
function addClass(el, className) {
	for (var i = 0; i < el.length; i++) {
		var item = el[i]
		if (item.classList) {
			item.classList.add(className)
		} else {
			item.className += ' ' + className
		}
	}
	return el
}
```

### 删除 class

```javascript
function removeClass(el, className) {
	var classNames = className.split(' ')

	for (var a = 0; a < classNames.length; a++) {
		className = classNames[a]
		for (var i = 0; i < el.length; i++) {
			var item = el[i]
			if (item.classList) {
				item.classList.remove(className)
			} else {
				item.className = item.className.replace(
					new RegExp('(^|\\b)' + className.split(' ').join('|') + '(\\b|$)', 'gi'),
					' '
				)
			}
		}
	}
	return el
}
```

### 设置 css 属性

```javascript
function css(items, props) {
	var key
	for (key in props) {
		if (props.hasOwnProperty(key)) {
			if (key !== null) {
				for (var i = 0; i < items.length; i++) {
					var item = items[i]
					item.style[key] = props[key]
				}
			}
		}
	}

	return items
}
```

### 深拷贝

```javascript
function deepExtend(out) {
	out = out || {}
	for (var i = 1, len = arguments.length; i < len; ++i) {
		var obj = arguments[i]
		if (!obj) {
			continue
		}
		for (var key in obj) {
			if (!obj.hasOwnProperty(key)) {
				continue
			}
			if (Object.prototype.toString.call(obj[key]) === '[object Object]') {
				out[key] = deepExtend(out[key], obj[key])
				continue
			}
			out[key] = obj[key]
		}
	}
	return out
}
```

### 事件触发

```javascript
function triggerEvent(event) {
	if (document.createEvent) {
		event = document.createEvent('HTMLEvents')
		event.initEvent('dataavailable', true, true)
		event.eventName = 'dataavailable'
		element.dispatchEvent(event)
	} else {
		event = document.createEventObject()
		event.eventName = 'dataavailable'
		event.eventType = 'dataavailable'
		element.fireEvent('on' + event.eventType, event)
	}
}
```

### 判断是否是可滑动设备

```javascript
function isTouchDevice() {
	var isTouchDevice = navigator.userAgent.match(
		/(iPhone|iPod|iPad|Android|playbook|silk|BlackBerry|BB10|Windows Phone|Tizen|Bada|webOS|IEMobile|Opera Mini)/
	)
}
```

### 判断是 ios 或者是 android

```javascript
function platform() {
	var u = navigator.userAgent
	var isAndroid = u.indexOf('Android') > -1 || u.indexOf('Adr') > -1 //android终端
	var isiOS = !!u.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/)
	if (isAndroid) {
	}
	return isAndroid ? 'android' : isiOS ? 'ios' : null
}
```

### 添加keyframes的 rules
```javascript
 function findKeyframesRule(rule) {
        var ss = document.styleSheets;
        console.log('ss', ss);

        for (var i = 0; i < ss.length; ++i) {
          for (var j = 0; j < ss[i].cssRules.length; ++j) {
            if (ss[i].cssRules[j].type && ss[i].cssRules[j].name == rule) {
              return ss[i].cssRules[j];
            }
          }
        }
        return null;
}

function insertMyRule(ruleName, str) {
	let keyFrames = findKeyframesRule(ruleName);
	console.log('keyframes', keyFrames);
	keyFrames.appendRule(str);
}
insertMyRule(
	'name',
	`
	0% { -webkit-transform: translate(100px, 100px)}
	`
);
```

### 封装js支持es5
```javascript

(function(global, factory) {
  'use strict';

  if (typeof module === 'object' && typeof module.exports === 'object') {
    module.exports = global.document
      ? factory(global, true)
      : function(w) {
          if (!w.document) {
            throw new Error('fantast requires a window with a document');
          }
          return factory(w);
        };
  } else {
    factory(global);
  }
})(typeof window !== 'undefined' ? window : this, function(window, noGlobal) {
  'use strict';
	// 此处填写内容返回值
	// var a = {}
	// return a;
});

```