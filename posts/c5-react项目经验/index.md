# c5项目经验


### antd的global全局样式修改

在umi.ts中引入的全局less文件修改默认样式时不需要写global，在组件中单独使用less文件时用styles.xxx，此时浏览器会对class名进行编译

### antd3.x中的tooltip没有color属性如何改变背景色

```javascript
  .ant-tooltip-arrow::before{ //箭头
    background-color: #FFFFFF;
  }
  .ant-tooltip-inner{  //框
    background-color: #ffffff;
    padding: 14px;
  }
```

### tooltip没有挂载到父元素，或挂载到父元素后样式出错

```javascript
getPopupContainer={node => document.getElementById('modalContent')}
```


