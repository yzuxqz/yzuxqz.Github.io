# react+ts


# 初始化与配置

## 初始化react+ts项目

create-react-app xxx --template typescript

## 规范配置

1. 在引入文件时直接使用根路径：在tsconfig.json中配置baseUrl为'./src'

2. prettier配置代码自动格式化：https://prettier.io/

   - npm install --save-dev --save-exact prettier

   - 新建.prettierrc.json

   - 新建.prettierignore，忽略build，coverage

   - 为了在commit之前自动格式化：npx mrm lint-staged，package.json中配置扩展名

     ```json
     "husky": {
       "hooks": {
         "pre-commit": "lint-staged"
       }
     },
     "lint-staged": {
       "*.{js,css,md,ts,tsx}": "prettier --write"
     }
     ```

   - 为了避免和eslint冲突

     npm install eslint-config-prettier -D

     ```json
       "eslintConfig": {
         "extends": [
           "react-app",
           "react-app/jest",
           "prettier"
         ]
       }
     ```

3. commit提交规范：commitlint

## MOCK方案配置

- npm install json-server -g

- npm install json-server -D

- script中配置

  ```json
   "json-server":"json-server __json_server_mock__/db.json --watch"
  ```




# project-list

- 状态提升

  ```jsx
  import React from 'react'
  import * as qs from 'qs'
  
  import {SearchPanel} from "./search-panel";
  import {List} from "./list";
  import {useEffect, useState} from "react";
  import {cleanObject,useDebounce,useMount} from "../../utils";
  
  export const ProjectListScreen=()=>{
    const [users, setUsers] = useState([])
    const [param, setParam] = useState({
      name: '',
      personId: ''
    })
    const debounceParam= useDebounce(param,1000)
    const [list, setList] = useState([])
    //当用户输入关键词或选择select框，param变化
    useEffect(() => {
      fetch(`http://localhost:3000/projects?${qs.stringify(cleanObject(debounceParam))}`).then(async response => {
        if (response.ok) {
          setList(await response.json())
        }
      })
    }, [debounceParam])
  
    useMount(()=>{
      fetch('http://localhost:3000/users').then(async response=>{
        if(response.ok){
          setUsers(await response.json())
        }
      })
    })
    return <div>
      <SearchPanel param={param} users={users} setParam={setParam}/>
      <List list={list} users={users}/>
    </div>
  }
  
  ```

- hooks

- clearObject

  ```jsx
  export const isFalsy = (value) => (value === 0 ? false : !value);
  //在一个函数中，改变传入的对象本身是不好的
  export const cleanObject = (object) => {
    const result = { ...object };
    Object.keys(result).forEach((key) => {
      const value = result[key];
      if (isFalsy(value)) {
        delete result[key];
      }
    });
    return result;
  };
  ```

# customhooks

- useMount

  ```
  export const useMount = (callback) => {
    useEffect(() => {
      callback();
    }, []);
  };
  ```

- useDebounce

  ```jsx
  export const useDebounce = (value, delay) => {
    const [newValue, setNewValue] = useState(value);
    useEffect(() => {
      //每次在value变化以后，设置一个定时器
      const timer = setTimeout(() => {
        setNewValue(value);
      }, 2000);
      //每次在上一个useEffect处理完以后再运行，第一个effect的timer被第二个effect清理，最后一个无人清理
      return () => {
        clearTimeout(timer);
      };
    }, [value, delay]);
    return newValue;
  };
  ```

- more in reacthooks_learn

# ts

- more in typescript_learn


