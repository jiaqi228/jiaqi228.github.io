---
title: "React学习笔记：官方文档"
categories:
  - React
  - Learning Note
tags:
  - React
  - Learning Note
---

> 确认官方文档以了解最新的React规格。

## Handling Event
如果是ES6 Class形式定义的Component，对于将在Component中定义的Method绑定到事件上，官方推荐使用在构造函数中事先绑定this后再绑定到对应事件上去的作法。

Class中的Method无法解决this变量。
[LINK](https://www.smashingmagazine.com/2014/01/understanding-javascript-function-prototype-bind/)

```javascript
class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = {isToggleOn: true};

    // This binding is necessary to make `this` work in the callback
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    this.setState(state => ({
      isToggleOn: !state.isToggleOn
    }));
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        {this.state.isToggleOn ? 'ON' : 'OFF'}
      </button>
    );
  }
}

ReactDOM.render(
  <Toggle />,
  document.getElementById('root')
);
```

## Keys
React需要Key属性来判断更新列表对象。在什么地方设置Keys，并不是通过\<li\>标签判断，而是通过什么地方使用了map()函数。

## Controlled Component
HTML控件的值交由React的Handler方法管理的控件称为Controlled Component。

## [Thinking In React](https://reactjs.org/docs/thinking-in-react.html)
1. 分割画面确定Components
2. 使用props创建静态Component（注意此时不要考虑States，State仅用于需要交互的地方）
3. 确定States
4. 决定在哪里管理States

