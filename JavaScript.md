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
