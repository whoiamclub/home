---
title: 怎么使用react搭建工程1—计数器
date: 2017-07-04 13:17:44
tags: [react,javascript]
categories: react
---

react配合redux搭建最简单的应用——计数器。
<!--more-->
``` bash
import React, { Component } from 'react'
import PropTypes from 'prop-types'
import ReactDOM from 'react-dom'
import { createStore } from 'redux'
import { Provider, connect } from 'react-redux'

/* 无状态页面组件 */
// 组件只需要两种来源于props的变量
// 一个是来自于store的state
// 一个来源事件句柄
class Counter extends Component {
  render() {
    const { value, onIncreaseClick } = this.props
    return (
      <div>
        <span>{value}</span>
        <button onClick={onIncreaseClick}>Increase</button>
      </div>
    )
  }
}

Counter.propTypes = {
  value: PropTypes.number.isRequired,
  onIncreaseClick: PropTypes.func.isRequired
}

/* 页面业务逻辑 */
// 数据关联store.state中储存的值
function mapStateToProps(state) {
  return {
    value: state.count
  }
}
// 事件句柄与Reducer关联
function mapDispatchToProps(dispatch) {
  return {
    onIncreaseClick: () => dispatch({ type: 'increase' })
  }
}

// 将数据、方法与组件关联起来
const App = connect(
  mapStateToProps,
  mapDispatchToProps
)(Counter)


// Reducer同步处理
function counter(state = { count: 0 }, action) {
  const count = state.count
  switch (action.type) {
    case 'increase':
      return { count: count + 1 }
    default:
      return state
  }
}

// Store:将Reducer同步处理的state存在store中
const store = createStore(counter)


ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
)

/* 代码来源阮一峰先生*/
```
基于以上代码，我们可以清楚看清楚react的数据流。
>Component （事件）-> 句柄或异步请求 -> Reducer -> store -> (state)Component