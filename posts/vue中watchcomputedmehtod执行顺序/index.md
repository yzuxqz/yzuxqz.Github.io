# vue中watch,computed,mehtod执行顺序


# vue中watch,computed,mehtod执行顺序

在[vue](https://so.csdn.net/so/search?q=vue&spm=1001.2101.3001.7020)中数据存在的方式有：data , props , computed 

由于vue的双向数据绑定，自动更新数据的机制，在数据变化后，对此数据依赖 的所有数据，watch事件都会被更新、触发。所以，只有数据本身变化了，依赖项才会改变。

computed：只有当computed 属性被使用后，才会执行computed的代码，若组件中未被使用，computed代码不会执行。

## 执行顺序：

1. 页面加载时：

   onload: watch(immediate：true) --> computed --> watch(默认computed：false)

2. 交互改变数据时：

​       event : watch --> computed --> method 

​       注：watch中的数据设置immediate：true时，在组件加载时将立刻执行（v-modal双向绑定的数据值都已更新，才会执行watch方法）。

​      另外，computed数据在method中和在html中被使用时，代码被执行的顺序稍有不同。通过打断点发现，当computed在method中被使用时，代码首先执行值computed被引用处，然后继续执行computed代码，其实，最后的结果都是一样，在method中拿到的computed数据都是更新过的。ps:尽量少用watch，不然数据流不清晰

ele组件的执行顺序：（绑定的都是change事件）

​    radio：        v-model --> watch--> method --> computed
​     radioGroup：   v-model --> watch--> method --> computed
​     checkbox:      v-model --> method --> computed --> watch
​     checkboxGroup: v-model --> watch  --> method  --> computed 
