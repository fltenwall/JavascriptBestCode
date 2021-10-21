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
// 缺点：由于 || 是一个布尔逻辑运算符，左侧的操作数会被强制转换成布尔值用于求值。任何假值（0， ''， NaN， null， undefined）都不会被返回。这导致如果你使用0，''或NaN作为有效值，就会出现不可预料的后果
let name = obj.name || 'wall';

// best 空值合并操作符
// 优点：只在第一个操作数为null 或 undefined 时（而不是其它假值）返回第二个操作数
let name = obj.name ?? 'wall';
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

// best 使用可选链操作符
let city = obj?.address?.city;
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
let {name = 'wall', age = 24} = obj;

// best 要注意解构的对象不能为undefined、null，因此要给一个兜底的默认值
let {name = 'wall', age = 24} = obj || {};
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

11.Array-filter 过滤原数组，返回所有符合条件项组成的数组
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
12.Array-find 查找一个值，找到符合条件的项，就不会继续遍历数组
```javascript
const arr = [1, 2, 3, 4, 5];

const result = arr.find( item =>{ return item === 3} ); // 3
```

13.Array-map 数组批量处理
```javascript
const arr = [1, 2, 3, 4, 5];

// bad
const newArr = [];
for (let i = 0;i < arr.length;i++){
	newArr.push(arr[i] + 1);
}

// good
const newArr = arr.map(n => n + 1);
```

14.使用箭头函数代替嵌套函数

```javascript
const arr = [1, 2, 3, 4, 5];

// bad
function isInculdes(n, arr) {
	return arr.includes(function (num) {
		return n === num;
	})
}

// good
let isInculdes = (n, arr) => arr.inculdes(num => num === n);
```

15.Array-forEach 数组批量处理，不返回新数组
```javascript
const arr = [1, 2, 3, 4, 5];

// bad
for (let i=0;i < arr.length;i++) {
	++arr[i];
}

// good
arr.forEach((item, index) => ++arr[index] );
```

16.Object.values快速获取对象键值
```javascript
const obj = {
	name : 'flten',
	age : 24,
}

// bad
const values = [];
for (key in obj) {
	values.push(obj[key]);
};

// good
const values = Object.values(obj);
```

17.Object.keys快速获取对象键名
```javascript
const obj = {
	name : 'flten',
	age : 24,
}

// bad
const keys = [];
for (key in obj) {
	keys.push(key);
};

// good
const keys = Object.keys(obj);
```

18.数组合并
```javascript
const a = [1, 2, 3];
const b = [3, 5, 6];

// bad 
// 缺点：没有去重
const c = a.concat(b); // [1,2,3,3,5,6]

// good
const c = [...new Set([...a, ...b])]; // [1,2,3,5,6]
```

19.对象合并
```javascript
const obj1 = {a:1,};
const obj2 = {b:2,};

// bad
const obj3 = Object.assign({},obj1,obj2); // {a:1, b:2}

// good
const obj3 = {...obj1, ...obj2}; // {a:1, b:2}
```

20.善于使用模板字符串
```javascript
const name = 'flten';
const age = 24;
let result = '';

// bad
if (age > 18){
	result = `${name}成年了`;
} else {
	result = `${name}还未成年`;
}

// good
// ${}中可以放入任意的JavaScript表达式，可以进行运算，以及引用对象属性
result = `${name}${age > 18 ? '成年了' : '还未成年'}`;
```

21.数组扁平化
```javascript
const deps = {
    'a':[1,2,3],
    'b':[3,4,5],
    'c':[5,6,7],
    'd':[7,8,9],
}

// good
let res = [Object.values(deps).flat(Infinity)]; // [1, 2, 3, 3, 4, 5, 5, 6, 7, 7, 8, 9]

// best 去重
let res = [...new Set(Object.values(deps).flat(Infinity))]; // [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

22.异步函数使用async await，而不是嵌套
```javascript
const fn1 = () =>{
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(1);
    }, 300);
  });
}
const fn2 = () =>{
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(2);
    }, 600);
  });
};

// bad 
const fn = () =>{
   fn1().then(res1 =>{
      console.log(res1);// 1
      fn2().then(res2 =>{
        console.log(res2)
      })
   })
};

// good
const fn = async () =>{
  const res1 = await fn1();
  const res2 = await fn2();
  console.log(res1);// 1
  console.log(res2);// 2
}
```

23.使用表达式添加对象属性
```javascript
let obj = {};
let order = 1;

// bad 需要额外创建一个变量
let content = `lang${index}`;
obj[key] = 'javascript';

// good 不额外创建变量
obj[`lang${index}`] = 'javascript';
```