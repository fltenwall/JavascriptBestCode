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

24.特定的变量说明
```javascript
// bad
if (value.length < 8) { // 容易产生疑惑，8代表什么呢？
    ....
}

// good
const MAX_INPUT_LENGTH = 8;
if (value.length < MAX_INPUT_LENGTH) { // 常量名说明，明确表示是不能超过都最大输入长度
    ....
}
```

25.函数传参说明
```javascript
// 这样的传参无法让人知道true和false代表什么
page.getSVG(api, true, false);

// good
page.getSVG({
    imageApi: api,
    isIncludePageBackground: true, 
    isCompress: false,
})
```

26.switch代替if..else
```javascript

// 分支过多
if (a === 1) {
    ...
} else if (a === 2) {
    ...
} else if (a === 3) {
    ...
} else {
   ...
}

// good
switch(a) {
   case 1:
           ....
   case 2:
           ....
   case 3:
           ....
  default:
       ....
}

// best
let handler = {
    1: () => {....},
    2: () => {....}.
    3: () => {....},
    default: () => {....}
}

handler[n]() || handler['default']()
```

27.使用Object.is()判断两个值是否相等
```javascript
// bad 使用 ==
"" == false // true == 运算符在判断相等前对两边的变量(如果它们不是同一类型)进行强制转换,应该避免使用

// good 使用 === 
+0 === -0 // true ===比==好一点，但是将数字 -0 和 +0 视为相等 
NaN === NaN //  false 将Number.NaN 与NaN视为不相等

// best 使用Object.is()，会正确的判断两个值是否为同一个值
Object.is(+0, -0) // false
Object.is(NaN, NaN) // true
```

28.使用数字分隔符
```javascript
// bad 数字太长时候能看出来这是多少吗？
const num = 1000000000; 

// good 使用数字分割符就清晰很多了
const num = 1_000_000_000;
```
29.控制台打印的 hack 技能
`console.log()`的hack技能
```javascript
const name = 'flten';

// 最普通的
console.log(name); // 'flten'

// 使用变量包装，可以打印出变量名和变量值
console.log({name}); // {name: 'flten'}

// 设置打印的样式 %c 是标识符，需要加的
console.log(`%c ${name}`,'color:red;font-size:24px'); // 效果很神奇
```

`console.table`
```javascript
const obj = {
  a : 'a',
  b : 'b'
};

// 最普通的方式
console.log(obj); // {a: 'a', b: 'b'}
// 使用console.table 你会在控制台得到一个表格
console.table(obj); 

// 更好是示例
// 来源于忘记出处的公众号
const users = [ 
   { 
      "first_name":"Harcourt",
      "last_name":"Huckerbe",
      "gender":"Male",
      "city":"Linchen",
      "birth_country":"China"
   },
   { 
      "first_name":"Allyn",
      "last_name":"McEttigen",
      "gender":"Male",
      "city":"Ambelókipoi",
      "birth_country":"Greece"
   },
   { 
      "first_name":"Sandor",
      "last_name":"Degg",
      "gender":"Male",
      "city":"Mthatha",
      "birth_country":"South Africa"
   }
]
console.table(users, ['first_name', 'last_name', 'city']);
```

`console.assert()` 断言输出
```javascript
const age = 24;

// 只有条件为false时，才会输出
console.assert(age > 30, "老了..."); // Assertion failed: 老了...
console.assert(age > 18, "成年了..."); // undefined
```

`console.count()` 统计打印的次数
```javascript
console.count('fltenwall'); // 1
console.count('fltenwall'); // 2
console.count('fltenwall'); // 3
console.count('fltenwall'); // 4
console.count('fltenwall'); // 5
```

30.事件监听
```javascript
// 如果添加的事件监听器只运行一次，可以使用 once 选项
element.addEventListener('click', () => console.log('flten'), {
    once: true
});           
```

31.获取鼠标位置
```javascript
document.addEventListener('mousemove', (e) => {
    console.log(`Mouse X: ${e.clientX}, Mouse Y: ${e.clientY}`);
});
```

32.获取 html 元素的属性数据
```html
<div id="user" data-name="flten" data-age="24">
    ...
</div>

<script>
    const user = document.getElementById('user');
  
    console.log(user.dataset); // { name: "flten", age: "24" }
  
    console.log(user.dataset.name); // "flten"
    console.log(user.dataset.age); // "24"
</script>     
```