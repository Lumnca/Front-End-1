<a id="top" href="#top">ECharts 配置项 axis 坐标轴类型  :maple_leaf:</a> 
----
`坐标轴有三种类型，类目型、数值型和时间型，他们的区别在于：`
* `类目型`:`需要指定类目列表，坐标轴内有且仅有这些指定类目坐标`  **`type 参数：'category'`**
* `数值型`:`需要指定数值区间，不指定时则自定计算数值范围，坐标轴内包含数值区间内容全部坐标` **`type 参数：'value' `**
* `时间型`:`时间型坐标轴用法同数值型，只是目标处理和格式化显示时会自动转变为时间，并且随着时间跨度的不同自动切换需要显示的时间粒度` **`type 参数：'time' | 'log'`**
##### 通用配置参数
**`type`**:[`可选参数：'category' | 'value' | 'time' | 'log'`] `参数类型`：`字符串`  `坐标轴类型，横轴默认为类目型'category'，纵轴默认为数值型'value'`<br/>

**`show`**:[`默认：true`] `参数类型`：`boolean`   `true（显示） | false（隐藏）`<br/>

**`position`**:[`默认：'bottom' | 'left'`] `参数类型`：`字符串`  `坐标轴类型，横轴默认为类目型'bottom'，纵轴默认为数值型'left'，可选为：'bottom' | 'top' | 'left' | 'right'`<br/>

**`name`**:[`默认：`] `参数类型`：`字符串`  `坐标轴名称，默认为空`<br/>

##### <a href="#top">数值型,时间型 共有配置选项</a>
|名称|	默认值|	适用类型|	描述|
|----|-----|-----|-----|
|`{string} name` |''|`数值型，时间型 `     | `坐标轴名称，默认为空`   |
|`{string} nameLocation`| 'end' | `数值型，时间型`| `坐标轴名称位置，默认为end，可选为：start \| end `|
|`{Object} nameTextStyle`| {}     | 	`数值型，时间型`      | `坐标轴名称文字样式，默认取全局配置，颜色跟随axisLine主色，可设`         |
|`{Array} boundaryGap`| [0, 0] | \|`数值型，时间型`\|  |`坐标轴两端空白策略，数组内数值代表百分比，[原始数据最小值与最终最小值之间的差额，原始数据最大值与最终最大值之间的差额]`|
|`{number} min`|null|	`数值型，时间型`|`指定的最小值，eg: 0，默认无，会自动根据具体数值调整，指定后将忽略boundaryGap[0]`|
|`{number} max`|null|	`数值型，时间型`|`指定的最大值，eg: 100，默认无，会自动根据具体数值调整，指定后将忽略boundaryGap[1]`|
|`{boolean} scale`|false|`数值型，时间型`|`脱离0值比例，放大聚焦到最终_min，_max区间`|
|`{number} splitNumber`|null|`数值型，时间型`|`分割段数，不指定时根据min、max算法调整`|




##### <a href="#top">类目录 专有配置选项</a>
|名称|	默认值|	适用类型|	描述|
|----|-----|-----|-----|
|`{boolean} boundaryGap`|true|类目型[category]|类目起始和结束两端空白策略，见下图，默认为true留空，false则顶头          |
|`{Array} data`  | 	[]  |`类目型`   |`类目列表，同时也是label内容，详见axis.data`  |

**`不定格 boundaryGap:true`**

![不定格](/Echarts/IMG/buDingGe.png) 

**`定格 boundaryGap:false`**

![定格](/Echarts/IMG/dingGe.png)
##### <a href="#top">配置样式</a>
    
![属性值](/Echarts/IMG/axiStyle.png) 
* `axis.axisLine: {}`
  * `配置参数 {boolean} show` `默认值`:`true` `通用 是否展示`
  * `配置参数 {boolean} onZero` `默认值`:`true` `通用 定位到垂直方向的0值坐标上 如下所示` 
  * `配置参数 lineStyle 通用` `属性lineStyle控制线条样式，`
    ```javascript
      {
          color: '#48b',
          width: 2,
          type: 'solid'
      }  
    ```
   
```javascript
xAxis : [
 {
    type : 'category',
    boundaryGap : false,
    axisLine:{
        onZero:false
    },
    data : ['周一','周二','周三','周四','周五','周六','周日']
 }
]
```
![属性值](/Echarts/IMG/onZeroFlase.png) 

```javascript
xAxis : [
 {
    type : 'category',
    boundaryGap : false,
    axisLine:{
        onZero:true
    },
    data : ['周一','周二','周三','周四','周五','周六','周日']
 }
]
```
![属性值](/Echarts/IMG/onZeroTrue.png) 

* `axis.axisTick`
  * `配置参数 {boolean} show` `默认值`:`true` `通用 是否展示`
  * `配置参数 {string | number | function} interval`  `默认值`:`'auto'` `类目型专用`
    * `小标记显示挑选间隔，默认为'auto'，可选为`
    * `'auto'（随axisLabel，自动隐藏显示不下的） | 0（全部显示） |`
    * `{number}（用户指定选择间隔）`
    * `{function}函数回调，传递参数[index，data[index]]，返回true显示，返回false隐藏`
  * `配置参数 {boolean} inside` `默认值`：`false` `通用 小标记是否显示为在grid内部，默认在外部`
  * `配置参数 {number} length`  `默认值`:`5` `通用	属性length控制线长`
  * `配置参数 {Object} lineStyle`  `默认值`:`{ color: '#333',width: 1}` `通用 属性lineStyle控制线条样式，（详见lineStyle）`
  <br/>
  
  ```javascript
       axisTick:{
        inside:false,
        length:10,
      onGap:true,
       lineStyle:{
         color:'grey'
       }
    }
  ```
  
* `axis.axisLabel`
  * `配置参数 {boolean} show` `默认值`:`true` `通用 是否展示`
  * `配置参数 {string | number | function} interval`  `默认值`:`'auto'` `类目型专用`
    * `小标记显示挑选间隔，默认为'auto'，可选为`
    * `'auto'（随axisLabel，自动隐藏显示不下的） | 0（全部显示） |`
    * `{number}（用户指定选择间隔）`
    * `{function}函数回调，传递参数[index，data[index]]，返回true显示，返回false隐藏`
  * `配置参数 {number} rotate` `默认值`：`0` `通用 标签旋转角度，默认为0，不旋转，正值为逆时针，负值为顺时针，可选为：-90 ~ 90`
  * `配置参数 {number} margin`  `默认值`:`	8` `通用	坐标轴文本标签与坐标轴的间距，默认为8，单位px`
  * `配置参数 {boolean} clickable`  `默认值`:`false` `通用 坐标轴文本标签是否可点击`
  * `配置参数 {string | Function} formatter`  `默认值`:`	null` `通用 间隔名称格式器：{string}（Template） | {Function}`
     * {string}，模板（Template），其变量为：
      * {value}: 内容或值  
     *{Function}，传递参数同模板变量：
        eg：function (value){return "星期" + "日一二三四五六".charAt(value);'}
  * `配置参数{boolean} clickable`  `默认值`:`{ color: '#333',width: 1}` `通用 属性lineStyle控制线条样式，（详见lineStyle）`
  * `配置参数{boolean} clickable`  `默认值`:`{ color: '#333',width: 1}` `通用 属性lineStyle控制线条样式，（详见lineStyle）`
  <br/>
