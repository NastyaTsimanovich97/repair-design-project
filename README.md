# repair-design-project
1. Initialize package.json
```
npm init
```
2. Load **webpack** as a module and **webpack-cli**
```
npm install webpack webpack-cli --save-dev
```
3. Add build script
```
"scripts": {
    "build": "webpack",
    "start": "webpack --watch"
  },
```
4. Install style plugins
```
npm install style-loader css-loader sass-loader node-sass extract-text-webpack-plugin -D
```
4.1 
```
npm install -D extract-text-webpack-plugin@next
```
5. Add webpack config
```
const path = require('path');
const ExtractTextPlugin = require('extract-text-webpack-plugin');

module.exports = {
  entry: './src/app.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
  },
  module: {
    rules: [
      {
        test: /\.scss$/,
        use: ExtractTextPlugin.extract({
          fallback: 'style-loader',
          use: ['css-loader', 'sass-loader']
        })
      }
    ]
  },
  plugins: [
    new ExtractTextPlugin('style.css')
    //if you want to pass in options, you can do so:
    //new ExtractTextPlugin({
    //  filename: 'style.css'
    //})
  ]
};
```
6. Import in src/app.js base.scss
```
import './scss/base.scss'
```
7. Add in index.html
```
<link rel='stylesheet' href='./dist/style.css'>

<script type="text/javascript" src="dist/bundle.js"></script>
```
8.
```
npm run build
npm run start
```
