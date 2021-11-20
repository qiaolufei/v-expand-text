# v-expand-text

> Collapse and expand multiline text for Vue.

## Installing
```js
// 安装 
npm install v-expand-text

// 在main.js中添加
import VExpandText from 'v-expand-text'
Vue.use(VExpandText)
```
## Usage

- 多行文本折叠
```js
<v-expand-text :text="text" />
```
- 按钮控制文本折叠/展开
```js
<v-expand-text :text="text" btn />
```
- popover展示全文本(hover展示)
```js
<v-expand-text :text="text" popover />
```

## Attributes
|  参数   | 说明  | 类型  | 可选值  | 默认值  |
|  ----  | ----  | ----  | ----  | ----  |
|  text | 文本内容 | String | -- | -- |
|  rows | 折叠显示行数 | Number | -- | 3 |
|  btn | 展开、折叠按钮 | Boolean | true/false | false |
|  btnIcon | 展开、折叠icon | Boolean | true/false | true |
|  popover | popover显示全文本 | Boolean | true/false | false |
|  placement | popover位置 | String | top/top-start/top-end/bottom/bottom-start/bottom-end/left/left-start/left-end/right/right-start/right-end | bottom |






