# VUE全局变量的几种实现方式

### （1）全局专用模块Global.vue

```
<script type="text/javascript">
const colorList = [
  '#F9F900',
  '#6FB7B7',
  '#9999CC',
  '#B766AD',
  '#B87070',
  '#FF8F59',
  '#FFAF60',
  '#FFDC35',
  '#FFFF37',
  '#B7FF4A',
  '#28FF28',
  '#1AFD9C',
  '#00FFFF',
  '#2894FF',
  '#6A6AFF',
  '#BE77FF',
  '#FF77FF',
  '#FF79BC',
  '#FF2D2D',
  '#ADADAD'
]
const colorListLength = 20
function getRandColor () {
  var tem = Math.round(Math.random() * colorListLength)
  return colorList[tem]
}
export default
{
  colorList,
  colorListLength,
  getRandColor
}
</script>
```
在需要使用全局变量的模块引入改文件即可使用。

### （2）全局变量模块挂载到Vue.prototype里

Global.js同上，在程序入口的main.js里加下面代码：

```
import global_ from './components/tool/Global'
Vue.prototype.GLOBAL = global_
```
挂载之后，在需要引用全局量的模块处，不需再导入全局量模块，直接用this就可以引用了，如下:

```
<script type="text/javascript">
    export default {
      data () {
        return {
          getColor: this.GLOBAL.getRandColor,
          mainList: [
            {
              id: 1,
              img: require('../../assets/rankIcon.png'),
              title: '登录界面'
            },
            {
              id: 2,
              img: require('../../assets/rankIndex.png'),
              title: '主页'
            }
          ]
        }
      }
    }
</script>
```
### （3）使用VUEX

