---
layout: post
title: Object.defineProperty()
author: CAO qisen
date: :year/:month/:day/
subtitle: 浅析Object.defineProperty()
header-img:
cdn:
tags:
    - Object.defineProperty
---


Object.defineProperty()
----
> The static method Object.defineProperty() defines a new property directly on an object, or modifies an existing property on an object, and returns the object.   -- MDN
> 通过Object.defineProperty()可以在一个对象上定义新的属性或者修改存在的属性，并最终返回该对象。
<!-- excerpt -->
语法
-----
```javascript
	Object.defineProperty(obj, prop, descriptor)
```
参数
-----
+ obj: 要添加或者修改属性的对象（必须）
+	prop: 要添加属性的名称（必须）
+	descriptor: 要被定义或修改的属性描述符（必须）

DEMO

```javascript
	let person = {};
	
	Object.defineProperty(person, 'name', {
		value: 'cao'
	});
	
	console.log(person.name)  //  cao
```

返回值
----
+	返回传递给函数的对象。

Description
----
> descriptor允许我们准确的描述要添加或者修改的属性。
	
descriptor可设置的属性有以下几个：

* configurable

> 默认: false
> 
> 当值为true时，该属性不可修改或者删除。

```javascript
	let person = {};
	Object.defineProperty(obj, 'name', {
	    value: 'cao',
	    configurable: false
	})

	person.name = 'ccc';
	
	delete person.name;
	
	console.log(person.name);  // cao
```

* enumerable

> 默认: false
> 
> 当值为true时，该属性才可以被枚举。

```javascript
	let person = {};
	Object.defineProperty(person, 'name', {
	    value: 'cao',
	    configurable: false,
	    enumerable: true
	})
	
	for (let key in person) {
	    console.log(key)	// name
	}
```



* value

> 默认: undefined
>
> 被添加或者修改的属性的值，该值可以是任意的JavaScript value (如 number, object, function, etc)。


* writable

> 默认: false
> 
> 当值为true时，value才可以被赋值运算符改变。

```javascript
	let person = {};
	Object.defineProperty(person, 'name', {
	    value: 'cao',
	    configurable: false,
	    writable: false
	})
	
	person.name = 'ccc';
		
	console.log(person.name);	// cao
```

* get

> 默认: undefined
> 
> 给该属性提供getter方法，该方法返回属性值value，否则为undefined。

* set

> 默认: undefined
> 
> 给该属性提供setter方法，如果没有 setter 则为 undefined。该方法将接受唯一参数，并将该参数的新值分配给该属性。



	
