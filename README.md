# JavascriptBestCode 给你最好的javascript代码！

1.通过条件判断给变量赋布尔值

```javascript
// bad
if (a === 'a') {
	b = true;
} else {
	b = false;
}

// good
b = a === 'a';

// best
b = (a === 'a');
```

2.使用三元表达式代替if判断
```javascript
// bad
if (a === 'a') {
	b = a;
} else {
	b = c;
}

// good
b = a === 'a' ? a : c;

// best
b = (a === 'a' ? a :c);

```

3.使用“短路”的特性设置默认值(或者为数据兜底，不至于为undefined)
```javascript
const obj = {
	name : 'flten',
	age : 24,
};

// bad
let name = obj.name;

// good
let name = obj.name || 'wall';

```

4.
```javascript
const obj = {
	name : 'flten',
	age : 24,
	address : {
		city : 'BeiJing',
	}
}

// bad
let city = obj.address.city;

// good
let city = obj.address && obj.address.city;
```

5.解构设置默认值防止报错
```javascript
const obj = {
	name : 'flten',
	age : 24,
};

// bad
let {name, age} = obj;

// good
let {name = 'wall', age = 24};
```

6.使用解构取得数据，而不是直接接收一个对象
```javascript
// bad
getData (data) {
	this.name = data.name;
	this.age = data.age;
};

// good  可以同时设置默认值
getData ({name = 'flten', age = 24}) {
	this.name = name;
	this.age = age;
};
```

7.解构时可以重命名简化变量名
```javascript
// bad
getData ({this_is_name = 'flten', this_is_age = 24}) {
	this.name = this_is_name;
	this.age = this_is_age;
};

// good
getData ({this_is_name : name = 'flten', this_is_age : age = 24}) {
	this.name = name;
	this.age = age;
};
```

8.交换两个数据

```javascript
let num1 = 10, num2 = 20;

// bad
let temp = num1;
a = b;
b = temp;

// good
[a, b] = [b, a];
```

9.Array-inculdes 判断元素是否满足某条件
```javascript
let a = 1;

// bad
if (a === 1 || a === 2 || a === 3){
	// ...
}

// good
const arr = [1, 2, 3];
if (arr.includes(a)) {
	// ...
}

```

10.Array-some 判断元素是否满足某条件
```javascript
const arr = [1, 2, 3, 4, 5];

// bad
function hasNumber(n, arr){
	for (let i = 0; i < arr.length; i++) {
		if (arr[i] === n) return true;
	};
	return false;
};

// good
let hasNumber = (n, arr) => arr.some(num => num === n);
```

11.Array-filter 过滤原数组，返回新数组
```javascript
const arr = [1, 2, 3, 4, 5];

// bad;
const newArray = [];
for (let i = 0; i < arr.length; i++) {
	if (arr[i] > 3)  newArray.push(arr[i]);
}

// good
const newArray = arr.filter(n => n > 3);
```
