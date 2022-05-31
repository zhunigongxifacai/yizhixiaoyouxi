# 扫雷游戏
## 编写原因
想试一下uniapp能不能支持写游戏，插件市场也没有一款看得过去的游戏作为参考和教程，所以我自己写了一个扫雷游戏作为uniapp游戏开发初探

## 安装
下载插件后使用`import saolei from '@components/gwh-saolei/gwh-saolei.vue'`加载扫雷插件，
在需要用的页面使用
```
<template>
	<view>
		<saolei :width="8" :height="8" :boomNum="10"></saolei>
	</view>
</template>
<script>
	export default{
		components:{
			saolei
		},
		// ...
	}
</script>
// ...
```
引入扫雷游戏

## 玩法介绍
### 游戏目标
扫雷游戏要求玩家尽可能多地依照周围信息排除雷，当雷排完时，游戏成功；当玩家误触雷时，游戏失败。

### 地图说明
| 图形 | 说明 |
| :-: | :- |
| 实心方块 | 未排除的地区 | 
| 空方块或1-8数字块 | 当玩家点击`@tap`（PC端鼠标左键或移动端单指点击）后，如果该方块周围（左、左上、上、右上、右、右下、下、左下）8个方块中有雷，则显示总雷数，当总雷数=0时，为空方块 | 
| 雷方块 | 当玩家点击`@tap`的方块是雷时，游戏结束 | 
| 标记方块 | 当玩家认为该实心方块可能是雷方块时，通过长按`@longpress`标记该雷方块为标记方块 |
| 误标方块 | 当玩家标记了一个自以为是雷的方块但该方块其实是数字块或空方块，且失误点击了一个本来是雷方块的方块导致游戏结束时，系统提示玩家误标的方块 |

### 操作说明
#### 开实心方块
鼠标左键或单指**点击实心**方块（`@tap`事件）

#### 标记雷方块
鼠标左键或单指**长按实心**方块（`@longpress`事件）

#### 取消标记雷方块
鼠标左键或单指**长按标记**方块（`@longpress`事件）

#### 快速开周围方块
在用户标记某个雷后，鼠标左键或单指**点击周围数字**方块（`@tap`事件）

#### 开始新一轮游戏
点击笑脸/骷髅头位置

## 参数说明
| 参数名称 | 类型 | 默认值 | 说明 | 
| :-: | :-: | :-: | :- |
| width | `Number` | `8` | 扫雷游戏地图宽 | 
| height | `Number` | `8` | 扫雷游戏地图高 | 
| boomNum | `Number` | `10` | 雷数 |
 
## 方法
### @init 
游戏初始化时触发，将返回游戏`map`数组：`-1`为雷位置，`0-9`为周围有几个雷。
在改变`width | height | boomNum`时，会自动刷新游戏。同时点击左上角笑脸，也会开始新一轮游戏。

### @result
游戏结束时触发，返回游戏结果：`code=0`游戏成功，否则失败