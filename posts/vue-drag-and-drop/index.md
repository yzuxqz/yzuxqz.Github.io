# Vue Drag and Drop


# Vue Drag and Drop

1. 设置 div 元素允许拖拽

   ```javascript
   draggable="true"
   ```

2. 设置元素拖拽开始事件

   @dragstart="drag(item.data)"

   ```javascript
   <div style="border:1px solid green;" draggable="true" @dragstart="dragstart($event, item.data)" @dragend="dragend">
     {{item.data}}
   </div>
   ```

   ```csharp
   dragstart (event, data) {
     console.log('drag')
     event.dataTransfer.setData('item', data)
   },
   dragend (event) {
     event.dataTransfer.clearData()
   },
   ```

3. 在拖放区 drop 事件中获取数据

   ```kotlin
   <div style="border:1px solid red;height: 100px;width:300px;" @drop="drop" @dragover.prevent>
     <p style="color:#ccc;">{{this.dropData}}</p>
   </div>
   ```

   ```kotlin
   drop (event) {
     console.log('drop')
     let data = event.dataTransfer.getData('item')
     this.dropData = data
     console.log('data: ', data)
   }
   ```

   **注意**

   必须给拖放区元素添加 dragover.prevent，才能使 drop 事件正确执行

   


