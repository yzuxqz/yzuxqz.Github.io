# hooks


## useState

```jsx
import React, { useState } from 'react';

function Example() {
  // 声明一个叫 "count" 的 state 变量
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

## useEffect

```jsx
import React, { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  
  useEffect(() => {
    document.title = `You clicked ${count} times`;
  });

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

- useEffect如果第二个参数不写，相当于class中的componentDidMounted和componentDidUpdate

  ```jsx
    useEffect(() => {
      document.title = `You clicked ${count} times`;
    });
  ```

- 返回一个函数，相当于componentWillUnMounted

  ```jsx
    useEffect(() => {
      console.log(count)
      return ()=>{
        console.log('离开')
      }
    })
  ```

- 第二个参数表示要根据哪些状态的改变而去重新渲染，如果为空数组，则无论什么状态改变都不会调用effect

  ```jsx
    useEffect(() => {
      console.log(count)
      return ()=>{
        console.log('离开')
      }
    }，[])
  ```

- 数组中有哪些值，就会随着这些状态的改变而重新执行副作用

  ```jsx
    useEffect(() => {
      console.log(count)
      return ()=>{
        console.log('离开')
      }
    },[count])//只有count变化了才会调用effect中的函数
  ```

  

## useContext

```jsx
import React ,{useState,createContext,useContext} from 'react'
const CountContext = createContext({})//1
function Counter() {
  let {count} = useContext(CountContext)//3
  return <h2>{count}</h2>
}

function Context() {
  const [count,setCount] = useState(0)
  return(
    <div>
      <h1>{count}</h1>
      <button onClick={()=>{setCount(count+1)}}>点击	</button>
      <CountContext.Provider value={count}>//2如果初始值为对象，这里要写成对象的形式
        <Counter/>
      </CountContext.Provider>
    </div>
  )
}
export  default Context
```

- 父组件创建context

- 在父组件中包裹子组件

  ```jsx
        <CountContext.Provider value={count}>
          <Counter/>
        </CountContext.Provider>
  ```

- 子组件中使用useContext获取父组件中传递的数据

## memo

## useMemo

## useCallback

https://blog.csdn.net/fedlover/article/details/103347989?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.control&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.control

记忆函数

## useReducer

和useContxt结合可以实现redux的效果，但是不建议使用，使用useDispatch和useSlelector来使用redux

## useRef

- 相当于class中的createRef()

```jsx
import React ,{useRef}from 'react'
function Ref() {
  const textRef= useRef(null)

  return(
    <div>
      <input type="text" ref={textRef}/>
      <button onClick={()=>{
        console.log(textRef.current.value)}}>点击</button>
    </div>
  )
}
export default Ref
```



## useDispatch

- 用于结合redux使用

- 首先创建redux的store，action，reducer。并在外层容器包裹provider传递store

- 在需要使用dispatch发布action时

  ```jsx
  import React from 'react'
  import {useDispatch} from 'react-redux'
  import {createChangeColorAction} from "./redux/action";
  function ChangeColor() {
    const dispatch = useDispatch()
    return (
      <div>
        <button onClick={()=>{dispatch(createChangeColorAction('red'))}}>红色</button>
        <button onClick={()=>{dispatch(createChangeColorAction('blue'))}}>蓝色</button>
      </div>
    )
  }
  
  export default ChangeColor
  ```

  

## useSelector

- 需要使用store中的state时

  ```jsx
  import React, {createContext} from 'react'
  import {useSelector} from "react-redux";
  
  export const ColorContext = createContext({})
  export const Color = (props) => {
    const color = useSelector(state=>state.color)
    return (
      <ColorContext.Provider value={{color}}>
        {props.children}
      </ColorContext.Provider>
    )
  }
  ```

## 自定义hooks

- 动态获取浏览器窗口大小的hooks

```jsx
import React,{useState,useEffect,useCallback} from 'react'


function useWinSize() {
  const [width,setWidth] = useState(document.body.clientWidth)
  const [height,setHeight] = useState(document.body.clientWidth)

  const reSize=useCallback(()=> {
    setWidth(document.body.clientWidth)
    setHeight(document.body.clientHeight)
  },[])

  useEffect(()=>{
    window.addEventListener('resize',reSize)
    return ()=>{
      window.removeEventListener('resize',reSize)
    }
  },[])

  return ({width,height})
}

export default function UseWinSize() {
  const {width,height} = useWinSize()
  return(
    <div>
      <h1>{width}</h1>
      <h1>{height}</h1>
    </div>

  )
}

```

- useDebounce：修改value的更新频率

  ```jsx
  export const useDebounce = (value, delay) => {
    const [newValue, setNewValue] = useState(value)
    useEffect(() => {
      //每次在value变化以后，设置一个定时器
      const timer = setTimeout(() => {
          setNewValue(value)
        },
        2000)
      //每次在上一个useEffect处理完以后再运行，第一个effect的timer被第二个effect清理，最后一个无人清理
      return () => {
        clearTimeout(timer)
      }
    }, [value, delay])
    return newValue
  }
  ```

  使用

  ```jsx
   const debounceParam= useDebounce(param,1000)
  //当用户输入关键词或选择select框，param变化
    useEffect(() => {
      fetch(`http://localhost:3000/projects?${qs.stringify(cleanObject(debounceParam))}`).then(async response => {
        if (response.ok) {
          setList(await response.json())
        }
      })
    }, [debounceParam])
  ```

  
