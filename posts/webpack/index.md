# webpack


## 入口

指示webpack使用哪个模块，来作为构建其内部依赖图的开始

在webpack.config.js

1. 对象写法（可扩展性高）

```javascript
module.exports = {
  entry: {
    a2: 'dependingfile.js',
    b2: {
      dependOn: 'a2',
      import: './src/app.js',
    },
  },
};
```

2.单入口写法

```javascript
module.exports = {
  entry: {
    main: './path/to/my/entry/file.js',
  },
};

module.exports = {
  entry: ['./src/file_1.js', './src/file_2.js'],
  output: {
    filename: 'bundle.js',
  },
};
```

### 描述入口对象属性

1. dependOn：当前入口所依赖的入口，必须在该入口被加载前被加载

2. runtime：运行时 chunk 的名字。如果设置了，就会创建一个新的运行时 chunk。在 webpack 5.43.0 之后可将其设为 `false` 以避免一个新的运行时 chunk。

   - `runtime` 和 `dependOn` 不应在同一个入口上同时使用

     ```javascript
     module.exports = {
       entry: {
         a2: './a',
         b2: {
           runtime: 'x2',
           dependOn: 'a2',
           import: './b',
         },
       },
     };
     ```

   - `runtime` 不能指向已存在的入口名称

     ```javascript
     module.exports = {
       entry: {
         a1: './a',
         b1: {
           runtime: 'a1',
           import: './b',
         },
       },
     };
     ```

   - `dependOn` 不能是循环引用的

     ```
     module.exports = {
       entry: {
         a3: {
           import: './a',
           dependOn: 'b3',
         },
         b3: {
           import: './b',
           dependOn: 'a3',
         },
       },
     }
     ```

     

## 输出

1. 使用入口(此chunk的名称)名称

   ```javascript
   module.exports = {
     //...
     output: {
       filename: '[name].bundle.js',
     },
   };
   ```

2. 使用内部chunk id

   ```javascript
   module.exports = {
     //...
     output: {
       filename: '[id].bundle.js',
     },
   };
   ```

3. 同时配置多个入口

   ```javascript
   module.exports = {
     entry: {
       app: './src/app.js',
       search: './src/search.js',
     },
     output: {
       filename: '[name].js',
       path: __dirname + '/dist',
     },
   };
   ```

   

## loader

使用loader告诉webpack加载css文件或者解析ts

1. 首先安装loader：npm install --save-dev css-loader ts-loader

2. webpack配置

   ```javascript
   module.exports = {
     module: {
       rules: [
         { test: /\.css$/, use: 'css-loader' },
         { test: /\.ts$/, use: 'ts-loader' },
       ],
     },
   };
   ```

### 配置方式

[`module.rules`](https://webpack.docschina.org/configuration/module/#modulerules) 允许在 webpack 配置中指定多个 loader，loader 从右到左（或从下到上）地取值(evaluate)/执行(execute)

```javascript
module.exports = {
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [
          // [style-loader](/loaders/style-loader)
          { loader: 'style-loader' },
          // [css-loader](/loaders/css-loader)
          {
            loader: 'css-loader',
            options: {
              modules: true
            }
          },
          // [sass-loader](/loaders/sass-loader)
          { loader: 'sass-loader' }
        ]
      }
    ]
  }
}
```



## plugin

插件可以携带参数，必须在webpack配置中，向plugins属性传入一个new实例。

```javascript
const HtmlWebpackPlugin = require('html-webpack-plugin'); // 通过 npm 安装
const webpack = require('webpack'); // 访问内置的插件
const path = require('path');

module.exports = {
  entry: './path/to/my/entry/file.js',
  output: {
    filename: 'my-first-webpack.bundle.js',
    path: path.resolve(__dirname, 'dist'),
  },
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        use: 'babel-loader',
      },
    ],
  },
  plugins: [
    new webpack.ProgressPlugin(),
    new HtmlWebpackPlugin({ template: './src/index.html' }),
  ],
};
```

## 配置

webpack的配置文件是JavaScript文件，文件内导出webpack配置对象。webpack会根据该配置定义的属性进行处理。

## 模式
