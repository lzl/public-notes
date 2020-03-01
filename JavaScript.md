## Explain event delegation

事件委托。将事件监听器 event listeners 添加到父元素，而不是每个子元素单独设置事件监听器。当触发子元素时，事件会冒泡到父元素，监听器就会触发。

好处：减少内存占用；子元素变动时无需解绑或绑定。

```js
e.target && e.target.nodeName == "LI"
e.target && e.target.matches("a.classA")
```

- https://davidwalsh.name/event-delegate

在 React 中，所有事件监听器被委托给 document 做集中处理。针对 iOS Safari 早期版本的 bug，会自动对子元素添加一个空的监听器。

- https://github.com/facebook/react/issues/13625

在 React 中，在事件委托的过程中放入自定义数据，这种做法是一种 anti-pattern，因为它违背了数据单向流动原则。

- https://github.com/facebook/react/issues/10322#issuecomment-318912494
- https://blog.cloudboost.io/why-react-discourage-event-delegation-2b5fe3f52bea

## Explain how this works in JavaScript

函数的调用方式决定了 this 的值。

1. new Constructor(), 函数内的 this 是一个全新的对象。
2. call, apply or bind, 函数内的 this 是作为参数传入的对象。
3. obj.method(), 函数内的 this 将绑定到 obj 对象。
4. 如果不符合上述规则，this 的值指向全局对象。浏览器下 this 指向 window 对象，在严格模式 use strict 下，this 指向 undefined.
5. 如果符合上述多个规则，则较高的规则（1 号最高，4 号最低）将决定 this 的值。
6. 如果是箭头函数，this 被设置为它被创建时的上下文。

- https://codeburst.io/the-simple-rules-to-this-in-javascript-35d97f31bde3

## Explain how 'new' keyword works in JavaScript

1. this = {}; 创建一个全新对象，将其绑定到 this 上。
2. this.__proto__ = Constructor.prototype; this.constructor = Constructor;
3. 如果 Constructor 内 return 的不是对象、数组或函数，则 return this.
4. 如果 Constructor 内没有 return, 则 return this.

- https://codeburst.io/javascripts-new-keyword-explained-as-simply-as-possible-fec0d87b2741

## Explain how prototypal inheritance works

原型继承。所有对象都有一个 prototype 属性，指向它的原型对象。当试图访问一个对象的属性时，如果没有在该对象上找到，它还会搜寻该对象的原型，以及该对象的原型的原型，依次层层向上搜索，直到找到一个名字匹配的属性或到达原型链的末尾。

Constructor:

```js
function Foo(who) {
	this.me = who;
	this.me = who; // con: 无法保护属性不被更改
}

Foo.prototype.identify = function() {
	return "I am " + this.me;
};

function Bar(who) {
	Foo.call(this, "Bar:" + who);
}

Bar.prototype = Object.create(Foo.prototype);
Bar.prototype.constructor = Bar;  // "fixes" the delegated `constructor` reference

Bar.prototype.speak = function() {
	console.log("Hello, " + this.identify() + ".");
};

const b1 = new Bar("b1");

b1.speak(); // "Hello, I am Bar:b1."

// some type introspection
b1 instanceof Bar; // true
b1 instanceof Foo; // true
Bar.prototype instanceof Foo; // true
Bar.prototype.isPrototypeOf(b1); // true
Foo.prototype.isPrototypeOf(b1); // true
Foo.prototype.isPrototypeOf(Bar.prototype); // true
Object.getPrototypeOf(b1) === Bar.prototype; // true
Object.getPrototypeOf(Bar.prototype) === Foo.prototype; // true
```

OLOO (objects linked to other objects):

```js
const Foo = {
	Foo(who) {
		this.me = who;
		return this;
	},
	identify() {
		return "I am " + this.me;
	}
};

const Bar = Object.create(Foo);

Bar.Bar = function(who) {
	// "constructors" (aka "initializers") are now in the `[[Prototype]]` chain,
	// so `this.Foo(..)` works easily w/o any problems of relative-polymorphism
	// or .call(this,..) awkwardness of the implicit "mixin" pattern
	this.Foo("Bar:" + who);
	return this;
};

Bar.speak = function() {
	console.log("Hello, " + this.identify() + ".");
};

const b1 = Object.create(Bar).Bar("b1");

b1.speak(); // "Hello, I am Bar:b1."

// some type introspection
Bar.isPrototypeOf(b1); // true
Foo.isPrototypeOf(b1); // true
Foo.isPrototypeOf(Bar); // true
Object.getPrototypeOf(b1) === Bar; // true
Object.getPrototypeOf(Bar) === Foo; // true
```

Object.create:

```js
if (typeof Object.create !== "function") {
  Object.create = function(parent) {
    function Tmp() {}
    Tmp.prototype = parent;
    return new Tmp();
  };
}
```

- https://davidwalsh.name/javascript-objects
- https://stackoverflow.com/questions/29788181/kyle-simpsons-oloo-pattern-vs-prototype-design-pattern
- https://gist.github.com/getify/5572383
- https://medium.com/javascript-scene/javascript-factory-functions-vs-constructor-functions-vs-classes-2f22ceddf33e

## What is functional programming

Functional programming (often abbreviated FP) is the process of building software by composing pure functions, avoiding shared state, mutable data, and side-effects.

Pure functions. Given the same inputs, always returns the same output, and has no side-effects.

Function composition. `f(g(x))`

Avoid shared state. Any variable, object, or memory space that exists in a shared scope.

Avoid mutating state. Any object which can be modified after it’s created. Use `Immer`.

Avoid side effects. Any application state change that is observable outside the called function other than its return value. Modifying any external variable or object property. Logging to the console. Writing to the screen. Writing to a file. Writing to the network. Triggering any external process. Calling any other functions with side-effects. Random number generation.

- https://medium.com/javascript-scene/master-the-javascript-interview-what-is-functional-programming-7f218c68b3a0
- https://www.freecodecamp.org/news/functional-programming-principles-in-javascript-1b8fc6c3563f/
- https://hackernoon.com/two-years-of-functional-programming-in-javascript-lessons-learned-1851667c726
