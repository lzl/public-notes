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
