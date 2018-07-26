### 1. 开发项目中引入一个插件（eslint-config-airbnb-base），该插件是基础配置。
[规则传送门](https://github.com/airbnb/javascript)

> 下列配置为项目开发自定义rule
### 2. no-debugge 禁用no-debugge
```js
// bad
/*eslint no-debugger: "error"*/

function isTruthy(x) {
    debugger;
    return Boolean(x);
}
// good
/*eslint no-debugger: "error"*/

function isTruthy(x) {
    return Boolean(x); // set a breakpoint at this line
}
```
### 3. no-alert 禁用 Alert

```js
// bad
/*eslint no-alert: "error"*/

alert("here!");

confirm("Are you sure?");

prompt("What's your name?", "John Doe");

// good
/*eslint no-alert: "error"*/

customAlert("Something happened!");

customConfirm("Are you sure?");

customPrompt("Who are you?");

function foo() {
    var alert = myCustomLib.customAlert;
    alert();
}
```
### 4. 要求或禁止使用分号代替 ASI
```js
// bad
/*eslint semi: ["error", "never"]*/

var name = "ESLint";

object.method = function() {
    // ...
};

// good

/*eslint semi: ["error", "never"]*/

var name = "ESLint"

object.method = function() {
    // ...
}

var name = "ESLint"

;(function() {
    // ...
})()

import a from "a"
(function() {
    // ...
})()

import b from "b"
;(function() {
    // ...
})()
```

### 5. no-console 禁用 console
```js
// bad

/*eslint no-console: "error"*/
console.log("Log a debug level message.");
console.warn("Log a warn level message.");
console.error("Log an error level message.");

// good
/*eslint no-console: "error"*/

// custom console
Console.log("Hello world!");
// example
window.console.log('Hello world!')
```
### 6. prefer-const 要求使用 const 声明那些声明后不再被修改的变量
```js
// bad
/*eslint prefer-const: "error"*/
/*eslint-env es6*/

// it's initialized and never reassigned.
let a = 3;
console.log(a);

let a;
a = 0;
console.log(a);

// `i` is redefined (not reassigned) on each loop step.
for (let i in [1, 2, 3]) {
    console.log(i);
}

// `a` is redefined (not reassigned) on each loop step.
for (let a of [1, 2, 3]) {
    console.log(a);
}

// good
/*eslint prefer-const: "error"*/
/*eslint-env es6*/

// using const.
const a = 0;

// it's never initialized.
let a;
console.log(a);

// it's reassigned after initialized.
let a;
a = 0;
a = 1;
console.log(a);

// it's initialized in a different block from the declaration.
let a;
if (true) {
    a = 0;
}
console.log(a);

// it's initialized at a place that we cannot write a variable declaration.
let a;
if (true) a = 0;
console.log(a);

// `i` gets a new binding each iteration
for (const i in [1, 2, 3]) {
  console.log(i);
}

// `a` gets a new binding each iteration
for (const a of [1, 2, 3]) {
  console.log(a);
}

// `end` is never reassigned, but we cannot separate the declarations without modifying the scope.
for (let i = 0, end = 10; i < end; ++i) {
    console.log(a);
}

// suggest to use `no-var` rule.
var b = 3;
console.log(b);
```
### 7. eol-last 要求或禁止文件末尾存在空行
```js
// bad

/*eslint eol-last: ["error", "always"]*/

function doSmth() {
  var foo = 2;
}\n

// good

/*eslint eol-last: ["error", "always"]*/

function doSmth() {
  var foo = 2;
}
```
### 8. object-shorthand 要求或禁止对象字面量中方法和属性使用简写语法
```js
// bad
/*eslint object-shorthand: "error"*/
/*eslint-env es6*/

var foo = {
    w: function() {},
    x: function *() {},
    [y]: function() {},
    z: z
};

// good

/*eslint object-shorthand: "error"*/
/*eslint-env es6*/

var foo = {
    w() {},
    *x() {},
    [y]() {},
    z
};
```

### 9. 要求或禁止使用拖尾逗号 (comma-dangle)
```js
// bad
/*eslint comma-dangle: ["error", "always"]*/

var foo = {
    bar: "baz",
    qux: "quux"
};

var arr = [1,2];

foo({
  bar: "baz",
  qux: "quux"
});

// good

/*eslint comma-dangle: ["error", "always"]*/

var foo = {
    bar: "baz",
    qux: "quux",
};

var arr = [1,2,];

foo({
  bar: "baz",
  qux: "quux",
});
```
### 10. 要求或禁止函数圆括号之前有一个空格 (space-before-function-paren)
```js
// bad
/*eslint space-before-function-paren: ["error", "never"]*/
/*eslint-env es6*/

function foo () {
    // ...
}

var bar = function () {
    // ...
};

var bar = function foo () {
    // ...
};

class Foo {
    constructor () {
        // ...
    }
}

var foo = {
    bar () {
        // ...
    }
};

var foo = async () => 1

// good

/*eslint space-before-function-paren: ["error", "never"]*/
/*eslint-env es6*/

function foo() {
    // ...
}

var bar = function() {
    // ...
};

var bar = function foo() {
    // ...
};

class Foo {
    constructor() {
        // ...
    }
}

var foo = {
    bar() {
        // ...
    }
};

var foo = async() => 1
```
### 11. 建议使用模板而非字符串连接 (prefer-template)

```js
// bad
/*eslint prefer-template: "error"*/

var str = "Hello, " + name + "!";
var str = "Time: " + (12 * 60 * 60 * 1000);

// good

/*eslint prefer-template: "error"*/
/*eslint-env es6*/

var str = "Hello World!";
var str = `Hello, ${name}!`;
var str = `Time: ${12 * 60 * 60 * 1000}`;
```
### 12. 要求 return 语句要么总是指定返回的值，要么不指定 (consistent-return)
```js
// bad
/*eslint consistent-return: "error"*/

function doSomething(condition) {
    if (condition) {
        return true;
    } else {
        return;
    }
}

function doSomething(condition) {
    if (condition) {
        return true;
    }
}

// good

/*eslint consistent-return: "error"*/

function doSomething(condition) {
    if (condition) {
        return true;
    } else {
        return false;
    }
}

function Foo() {
    if (!(this instanceof Foo)) {
        return new Foo();
    }

    this.a = 0;
}
```
### 13. 要求对象字面量属性名称使用引号 (quote-props)

```js
// bad
/*eslint quote-props: ["error", "as-needed"]*/

var object = {
    "a": 0,
    "0": 0,
    "true": 0,
    "null": 0
};

// good

/*eslint quote-props: ["error", "as-needed"]*/
/*eslint-env es6*/

var object1 = {
    "a-b": 0,
    "0x0": 0,
    "1e2": 0
};

var object2 = {
    foo: 'bar',
    baz: 42,
    true: 0,
    0: 0,
    'qux-lorem': true
};

var object3 = {
    foo() {
        return;
    }
};

```
### 14. 禁止或强制在括号内使用空格 (array-bracket-spacing)
```js
// bad

/*eslint array-bracket-spacing: ["error", "never"]*/
/*eslint-env es6*/

var arr = [ 'foo', 'bar' ];
var arr = ['foo', 'bar' ];
var arr = [ ['foo'], 'bar'];
var arr = [[ 'foo' ], 'bar'];
var arr = [ 'foo',
  'bar'
];
var [ x, y ] = z;
var [ x,y ] = z;
var [ x, ...y ] = z;
var [ ,,x, ] = z;

// good

/*eslint array-bracket-spacing: ["error", "never"]*/
/*eslint-env es6*/

var arr = [];
var arr = ['foo', 'bar', 'baz'];
var arr = [['foo'], 'bar', 'baz'];
var arr = [
  'foo',
  'bar',
  'baz'
];
var arr = ['foo',
  'bar'
];
var arr = [
  'foo',
  'bar'];

var [x, y] = z;
var [x,y] = z;
var [x, ...y] = z;
var [,,x,] = z;
```

### 15. 禁止未使用过的变量 (no-unused-vars)
```js
// bad

/*eslint no-unused-vars: "error"*/
/*global some_unused_var*/

// It checks variables you have defined as global
some_unused_var = 42;

var x;

// Write-only variables are not considered as used.
var y = 10;
y = 5;

// A read for a modification of itself is not considered as used.
var z = 0;
z = z + 1;

// By default, unused arguments cause warnings.
(function(foo) {
    return 5;
})();

// Unused recursive functions also cause warnings.
function fact(n) {
    if (n < 2) return 1;
    return n * fact(n - 1);
}

// When a function definition destructures an array, unused entries from the array also cause warnings.
function getY([x, y]) {
    return y;
}

// good

/*eslint no-unused-vars: "error"*/

var x = 10;
alert(x);

// foo is considered used here
myFunc(function foo() {
    // ...
}.bind(this));

(function(foo) {
    return foo;
})();

var myFunc;
myFunc = setTimeout(function() {
    // myFunc is considered used
    myFunc();
}, 50);

// Only the second argument from the descructured array is used.
function getY([, y]) {
    return y;
}

```

### 16. 禁止或强制在计算属性中使用空格 (computed-property-spacing)
```js
// bad

/*eslint computed-property-spacing: ["error", "never"]*/
/*eslint-env es6*/

obj[foo ]
obj[ 'foo']
var x = {[ b ]: a}
obj[foo[ bar ]]

// good

/*eslint computed-property-spacing: ["error", "never"]*/
/*eslint-env es6*/

obj[foo]
obj['foo']
var x = {[b]: a}
obj[foo[bar]]
```

### 17. 强制行的最大长度 (max-len)默认80
```js
// bad
/*eslint max-len: ["error", { "code": 80 }]*/

var foo = { "bar": "This is a bar.", "baz": { "qux": "This is a qux" }, "difficult": "to read" };

// good
/*eslint max-len: ["error", { "code": 80 }]*/

var foo = {
  "bar": "This is a bar.",
  "baz": { "qux": "This is a qux" },
  "easier": "to read"
};
```

### 18. 要求构造函数首字母大写 (new-cap)
```js
// bad

/*eslint new-cap: ["error", { "newIsCap": true }]*/

var friend = new person();

// good

/*eslint new-cap: ["error", { "newIsCap": true }]*/

var friend = new Person();
```

### 19. 附加一个标准的函数注释
```js
/**
 * Add two numbers
 * @param {number} num1 - The first number
 * @param {number} num2 - The second number
 * @return {number} The sum of the two numbers
 */
add(num1, num2) {
  return num1 + num2
},
```
