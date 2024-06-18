# matlab图论

## 基础

### plot函数

```
plot(G) 绘制图 G 中的节点和边。

plot(G,LineSpec) 设置线型、标记符号和颜色。例如，plot(G,'-or') 对节点使用红色圆圈，对边使用红线。

plot(___,Name,Value) 使用一个或多个名称-值对组参数（采用上述语法中的任意输入参数组合）指定的其他选项。

plot(G,'Layout','circle') 绘制图形的圆环形布局

plot(G,'XData',X,'YData',Y,'ZData',Z) 指定图形节点的 (X,Y,Z) 坐标。

plot(ax,___) 将图形绘制到 ax 指定的坐标区中，而不是当前坐标区 (gca) 中。选项 ax 可以位于上述语法中的任何输入参数组合之前。

h = plot(___) 返回 GraphPlot 对象。使用此对象可检查和调整所绘制图的属性。
```

#### `G` — 输入图 `graph` 对象 | `digraph` 对象

输入图，指定为 `graph` 或 `digraph` 对象。可使用 [`graph`](https://ww2.mathworks.cn/help/matlab/ref/graph.html) 创建一个无向图，或使用 [`digraph`](https://ww2.mathworks.cn/help/matlab/ref/digraph.html) 创建一个有向图。

**示例：** `G = graph(1,2)`

**示例：** `G = digraph([1 2],[2 3])`



#### `LineSpec` — 线型、标记符号和颜色 字符向量 | 字符串向量

线型、标记符号和颜色，指定为符号的字符向量或字符串向量。符号可以按任意顺序出现，而且您可以省略一个或多个特征。如果您省略线型，绘图会将图边显示为实线。

**示例：** `'--or'` 用红圈作为节点标记，用红色虚线表示边。

**示例：** `'r*'` 用红色星号作为节点标记，用红色实线表示边。

| 线型   | 描述   | 表示的线条                                                   |
| :----- | :----- | :----------------------------------------------------------- |
| `"-"`  | 实线   | ![Sample of solid line](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/linestyle_solid.png) |
| `"--"` | 虚线   | ![Sample of dashed line](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/linestyle_dashed.png) |
| `":"`  | 点线   | ![Sample of dotted line](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/linestyle_dotted.png) |
| `"-."` | 点划线 | ![Sample of dash-dotted line, with alternating dashes and dots](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/linestyle_dashdotted.png) |

| 标记          | 描述     | 生成的标记                                                   |
| :------------ | :------- | :----------------------------------------------------------- |
| `"o"`         | 圆圈     | ![Sample of circle marker](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/marker_o.png) |
| `"+"`         | 加号     | ![Sample of plus sign marker](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/marker_plus.png) |
| `"*"`         | 星号     | ![Sample of asterisk marker](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/marker_asterisk.png) |
| `"."`         | 点       | ![Sample of point marker](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/marker_point.png) |
| `"x"`         | 叉号     | ![Sample of cross marker](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/marker_x.png) |
| `"_"`         | 水平线条 | ![Sample of horizontal line marker](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/marker_hline.png) |
| `"|"`         | 垂直线条 | ![Sample of vertical line marker](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/marker_vline.png) |
| `"square"`    | 方形     | ![Sample of square marker](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/marker_s.png) |
| `"diamond"`   | 菱形     | ![Sample of diamond line marker](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/marker_d.png) |
| `"^"`         | 上三角   | ![Sample of upward-pointing triangle marker](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/marker_uptriangle.png) |
| `"v"`         | 下三角   | ![Sample of downward-pointing triangle marker](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/marker_downtriangle.png) |
| `">"`         | 右三角   | ![Sample of right-pointing triangle marker](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/marker_righttriangle.png) |
| `"<"`         | 左三角   | ![Sample of left-pointing triangle marker](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/marker_lefttriangle.png) |
| `"pentagram"` | 五角形   | ![Sample of pentagram marker](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/marker_p.png) |
| `"hexagram"`  | 六角形   | ![Sample of hexagram marker](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/marker_h.png) |

| 颜色名称    | 短名称 | RGB 三元组 | 外观                                                         |
| :---------- | :----- | :--------- | :----------------------------------------------------------- |
| `"red"`     | `"r"`  | `[1 0 0]`  | ![Sample of the color red](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/hg_red.png) |
| `"green"`   | `"g"`  | `[0 1 0]`  | ![Sample of the color green](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/hg_green.png) |
| `"blue"`    | `"b"`  | `[0 0 1]`  | ![Sample of the color blue](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/hg_blue.png) |
| `"cyan"`    | `"c"`  | `[0 1 1]`  | ![Sample of the color cyan](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/hg_cyan.png) |
| `"magenta"` | `"m"`  | `[1 0 1]`  | ![Sample of the color magenta](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/hg_magenta.png) |
| `"yellow"`  | `"y"`  | `[1 1 0]`  | ![Sample of the color yellow](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/hg_yellow.png) |
| `"black"`   | `"k"`  | `[0 0 0]`  | ![Sample of the color black](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/hg_black.png) |
| `"white"`   | `"w"`  | `[1 1 1]`  | ![Sample of the color white](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/hg_white.png) |



#### `ax` — 坐标区对象 对象

坐标区对象。如果不指定坐标区对象，则 `plot` 使用当前坐标区 (`gca`)。



#### 名称-值函数

##### `EdgeColor` — 边颜色 `[0 0.4470 0.7410]` （默认） | RGB 三元组 | 十六进制颜色代码 | 颜色名称 | 矩阵 | `'flat'` | `'none'`

边颜色，指定为逗号分隔的对组，其中包含 `'EdgeColor'` 和下列值之一：

- `'none'` - 不绘制边。

- `'flat'` - 每条边的颜色取决于 `EdgeCData` 的值。

- 矩阵 - 每行都是一个 RGB 三元组，表示一条边的颜色。矩阵的大小为 `numedges(G)`×`3`。

- RGB 三元组、十六进制颜色代码或颜色名称 - 边使用指定的颜色。

  RGB 三元组和十六进制颜色代码对于指定自定义颜色非常有用。

  - RGB 三元组是包含三个元素的行向量，其元素分别指定颜色中红、绿、蓝分量的强度。强度值必须位于 `[0,1]` 范围内，例如 `[0.4 0.6 0.7]`。
  - 十六进制颜色代码是字符向量或字符串标量，以井号 (`#`) 开头，后跟三个或六个十六进制数字，范围可以是 `0` 到 `F`。这些值不区分大小写。因此，颜色代码 `'#FF8800'` 与 `'#ff8800'`、`'#F80'` 与 `'#f80'` 是等效的。

  

  此外，还可以按名称指定一些常见的颜色。下表列出了命名颜色选项、等效 RGB 三元组和十六进制颜色代码。

  | 颜色名称    | 短名称 | RGB 三元组 | 十六进制颜色代码 | 外观                                                         |
  | :---------- | :----- | :--------- | :--------------- | :----------------------------------------------------------- |
  | `"red"`     | `"r"`  | `[1 0 0]`  | `"#FF0000"`      | ![Sample of the color red](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/hg_red.png) |
  | `"green"`   | `"g"`  | `[0 1 0]`  | `"#00FF00"`      | ![Sample of the color green](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/hg_green.png) |
  | `"blue"`    | `"b"`  | `[0 0 1]`  | `"#0000FF"`      | ![Sample of the color blue](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/hg_blue.png) |
  | `"cyan"`    | `"c"`  | `[0 1 1]`  | `"#00FFFF"`      | ![Sample of the color cyan](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/hg_cyan.png) |
  | `"magenta"` | `"m"`  | `[1 0 1]`  | `"#FF00FF"`      | ![Sample of the color magenta](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/hg_magenta.png) |
  | `"yellow"`  | `"y"`  | `[1 1 0]`  | `"#FFFF00"`      | ![Sample of the color yellow](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/hg_yellow.png) |
  | `"black"`   | `"k"`  | `[0 0 0]`  | `"#000000"`      | ![Sample of the color black](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/hg_black.png) |
  | `"white"`   | `"w"`  | `[1 1 1]`  | `"#FFFFFF"`      | ![Sample of the color white](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/hg_white.png) |

  以下是 MATLAB® 在许多类型的绘图中使用的默认颜色的 RGB 三元组和十六进制颜色代码。

  | RGB 三元组               | 十六进制颜色代码 | 外观                                                         |
  | :----------------------- | :--------------- | :----------------------------------------------------------- |
  | `[0 0.4470 0.7410]`      | `"#0072BD"`      | ![Sample of RGB triplet [0 0.4470 0.7410], which appears as dark blue](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/colororder1.png) |
  | `[0.8500 0.3250 0.0980]` | `"#D95319"`      | ![Sample of RGB triplet [0.8500 0.3250 0.0980], which appears as dark orange](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/colororder2.png) |
  | `[0.9290 0.6940 0.1250]` | `"#EDB120"`      | ![Sample of RGB triplet [0.9290 0.6940 0.1250], which appears as dark yellow](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/colororder3.png) |
  | `[0.4940 0.1840 0.5560]` | `"#7E2F8E"`      | ![Sample of RGB triplet [0.4940 0.1840 0.5560], which appears as dark purple](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/colororder4.png) |
  | `[0.4660 0.6740 0.1880]` | `"#77AC30"`      | ![Sample of RGB triplet [0.4660 0.6740 0.1880], which appears as medium green](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/colororder5.png) |
  | `[0.3010 0.7450 0.9330]` | `"#4DBEEE"`      | ![Sample of RGB triplet [0.3010 0.7450 0.9330], which appears as light blue](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/colororder6.png) |
  | `[0.6350 0.0780 0.1840]` | `"#A2142F"`      | ![Sample of RGB triplet [0.6350 0.0780 0.1840], which appears as dark red](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/colororder7.png) |

**示例：** `plot(G,'EdgeColor','r')` 创建一个具有红色边的图论图。



##### `EdgeLabel` — 边标签 `{}` （默认） | 向量 | 字符向量元胞数组 | 字符串数组

边标签，指定为逗号分隔的对组，其中包含 `'EdgeLabel'` 和一个数值向量、字符向量元胞数组或字符串数组。`EdgeLabel` 的长度必须等于图中的边数。默认情况下，`EdgeLabel` 是空元胞数组（不显示边标签）。

**示例：** `{'A', 'B', 'C'}`

**示例：** `[1 2 3]`

**示例：** `plot(G,'EdgeLabel',G.Edges.Weight)` 使用图边的权重作为其标签。

**数据类型：** `single` | `double` | `int8` | `int16` | `int32` | `int64` | `uint8` | `uint16` | `uint32` | `uint64` | `cell` | `string`



##### `Layout` — 图布局方法 `'auto'` （默认） | `'circle'` | `'force'` | `'layered'` | `'subspace'` | `'force3'` | `'subspace3'`

图布局方法，指定为逗号分隔的对组，其中包含 `'Layout'` 和下表中的选项之一。下表还列出了兼容的名称-值对组，可用于进一步优化每一种布局方法。有关这些特定于布局的名称-值对组的详细信息，请参阅 [`layout`](https://ww2.mathworks.cn/help/matlab/ref/matlab.graphics.chart.primitive.graphplot.layout.html) 参考页。

| 选项               | 描述                                                         | 特定于布局的名称-值对组                                      |
| :----------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| `'auto'`（默认值） | 根据图的大小和结构自动选择布局方法。                         | —                                                            |
| `'circle'`         | 圆形布局。将图节点放置在以原点为中心、半径为 1 的圆形上。    | `'Center'` - 圆形布局的中心节点                              |
| `'force'`          | 力导向图布局 [[1\]](https://ww2.mathworks.cn/help/matlab/ref/graph.plot.html#bvbo2_e)。在相邻节点之间使用引力，在远距离节点之间使用斥力。 | `'Iterations'` - 力导向图布局迭代次数`'WeightEffect'` - 边权重对布局的影响效果`'UseGravity'` - 多分量布局的引力切换`'XStart'` - 节点的起始 x 坐标`'YStart'` - 节点的起始 y 坐标 |
| `'layered'`        | 分层节点布局 [[2\]](https://ww2.mathworks.cn/help/matlab/ref/graph.plot.html#bvbo2_k)、[[3\]](https://ww2.mathworks.cn/help/matlab/ref/graph.plot.html#bvbo2_p)、[[4\]](https://ww2.mathworks.cn/help/matlab/ref/graph.plot.html#bvbo2_t)。将图节点置于多层中，表示层级结构。默认情况下是逐层向下的（有向无环图的箭头向下）。 | `'Direction'` - 层的方向`'Sources'` - 第一层包含的节点`'Sinks'` - 最后一层包含的节点`'AssignLayers'` - 层分配方法 |
| `'subspace'`       | 子空间嵌入式节点布局 [[5\]](https://ww2.mathworks.cn/help/matlab/ref/graph.plot.html#bvbo2_y)。在高维嵌入式子空间中绘制图节点，然后将位置投影回二维。默认情况下，子空间维度是 100 或节点总数（以两者中较小者为准）。 | `'Dimension'` - 嵌入式子空间的维度                           |
| `'force3'`         | 三维力导向图布局。                                           | `'Iterations'` - 力导向图布局迭代次数`'WeightEffect'` - 边权重对布局的影响效果`'UseGravity'` - 多分量布局的引力切换`'XStart'` - 节点的起始 x 坐标`'YStart'` - 节点的起始 y 坐标`'ZStart'` - 节点的起始 z 坐标 |
| `'subspace3'`      | 三维子空间嵌入式布局。                                       | `'Dimension'` - 嵌入式子空间的维度                           |

**示例：** `plot(G,'Layout','force3','Iterations',10)`

**示例：** `plot(G,'Layout','subspace','Dimension',50)`

**示例：** `plot(G,'Layout','layered')`



##### `LineStyle` — 线型 `'-'` （默认） | `'--'` | `':'` | `'-.'` | `'none'` | 元胞数组 | 字符串向量

线型，指定为逗号分隔的、由 `'LineStyle'` 和下表中列出的线型之一组成的对组，或者指定为由此类值构成的元胞数组或字符串向量。指定字符向量元胞数组或字符串向量，以便为每条边使用不同线型。

| 字符     | 线型   | 表示的线条                                                   |
| :------- | :----- | :----------------------------------------------------------- |
| `'-'`    | 实线   | ![Sample of a solid line](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/linestyle_solid.png) |
| `'--'`   | 虚线   | ![Sample of a dashed line](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/linestyle_dashed.png) |
| `':'`    | 点线   | ![Sample of a dotted line](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/linestyle_dotted.png) |
| `'-.'`   | 点划线 | ![Sample of a dash-dotted line](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/linestyle_dashdotted.png) |
| `'none'` | 无线条 | 无线条                                                       |



##### `LineWidth` — 边线宽 `0.5` （默认） | 正值 | 向量

边线宽，指定为逗号分隔的对组，其中包含 `'LineWidth'` 和一个正值（以磅为单位）或由此类值组成的向量。指定一个向量以对图中的每条边使用不同线宽。

**示例：** `0.75`



### highlight函数

```
highlight(H,nodeIDs) 通过增加由 nodeIDs 指定的节点的标记大小突出显示这些节点。

highlight(H,G) 通过分别增加图 G 的节点标记大小和边线宽，突出显示这些节点和边。G 必须具有与基础图 H 相同的节点，但具有的边是后者具有的边的子集。如果 G 包含重复的边，这些边都会突出显示。度数为 0 的孤立节点不会突出显示。

highlight(H,s,t) 通过增加边的线宽来突出显示 s 和 t 中指定的源节点和目标节点对之间的所有边。如果知道边索引而不是节点对 (s,t)，则可以改用 highlight(H,'Edges',idx)。

highlight(___,Name,Value) 使用一个或多个名称-值对组参数（采用上述语法中的任意输入参数组合）指定的其他选项。
例如，
highlight(H,nodes,'NodeColor','g') 通过将部分节点的颜色更改为绿色（而不是增加其标记大小）突出显示这些节点。
```



#### `H` — 输入图论图 `GraphPlot` 对象

输入图论图，指定为 `GraphPlot` 对象。使用 [`graph`](https://ww2.mathworks.cn/help/matlab/ref/graph.html) 或 [`digraph`](https://ww2.mathworks.cn/help/matlab/ref/digraph.html) 函数创建一个图，然后结合使用 [`plot`](https://ww2.mathworks.cn/help/matlab/ref/graph.plot.html) 与输出参数返回 [`GraphPlot`](https://ww2.mathworks.cn/help/matlab/ref/matlab.graphics.chart.primitive.graphplot.html) 对象。

**示例：** `H = plot(G)`



#### `nodeIDs` — 要突出显示的节点 逻辑向量 | 节点索引 | 节点名称

要突出显示的节点，指定为逻辑向量，或指定为一个或多个节点索引或节点名称。如果 `nodeIDs` 是逻辑向量，则其长度必须为 `numnodes(G)`。

下表显示通过数值节点索引或节点名称引用一个或多个节点的不同方法。

| 形式                      | 单一节点                            | 多个节点                                  |
| :------------------------ | :---------------------------------- | :---------------------------------------- |
| 节点索引                  | 标量**示例：**`1`                   | 向量**示例：**`[1 2 3]`                   |
| 节点名称                  | 字符向量**示例：**`'A'`             | 字符向量元胞数组**示例：**`{'A' 'B' 'C'}` |
| 字符串标量**示例：**`"A"` | 字符串数组**示例：**`["A" "B" "C"]` |                                           |



`nodeIDs` 不得指定与 `highlight` 的任何可选参数名称冲突的节点名称，例如 `'Edges'` 或 `'EdgeColor'`。对于这些情况，请改用 `findnode` 传入节点索引。



#### `G` — 要突出显示的图 `graph` 对象 | `digraph` 对象

要突出显示的图，指定为 `graph` 或 `digraph` 对象。`G` 必须具有与基础图 `H` 相同的节点，但具有的边是后者的边的子集。度为 `0` 的孤立节点不会突出显示。



#### `s,t` — 节点对组（以单独参数指定） 节点索引 | 节点名称

节点对组，指定为单独的节点索引或节点名称参数。`s` 和 `t` 中位置类似的元素指定图中边的源和目标节点。

`s` 和 `t` 不得指定与 `highlight` 的任何可选参数名称冲突的节点名称，例如 `'Edges'` 或 `'EdgeColor'`。对于这些情况，请改用 `findnode` 传入节点索引。

**示例：** `highlight(H,[1 2],[3 3])` 突出显示图边 `(1,3)` 和 `(2,3)`。

**示例：** `highlight(H,'a','b')` 突出显示从 `'a'` 到 `'b'` 的所有边。



#### 名称-值函数

##### `Edges` — 要突出显示的边 标量 | 向量

要突出显示的边，以逗号分隔的对组形式指定，该对组由 `'Edges'` 和一个标量边索引、边索引向量或逻辑向量组成。当相同的两个节点之间存在多条边时，可以使用此名称-值对组来突出显示节点之间的特定边。

此名称-值对组的值可以是来自 `shortestpath` 或 `shortestpathtree` 的第三个输出，例如 `[path,d,edgepath] = shortestpath(…)`。

**示例：** `highlight(p,'Edges',edgepath)`



**边属性**

##### `EdgeColor` — 边颜色 `[0 0.4470 0.7410]` （默认） | RGB 三元组 | 十六进制颜色代码 | 颜色名称

边颜色，指定为逗号分隔的对组，其中包含 `'EdgeColor'` 以及一个 RGB 三元组、十六进制颜色代码或颜色名称。

- RGB 三元组和十六进制颜色代码对于指定自定义颜色非常有用。

  - RGB 三元组是包含三个元素的行向量，其元素分别指定颜色中红、绿、蓝分量的强度。强度值必须位于 `[0,1]` 范围内，例如 `[0.4 0.6 0.7]`。
  - 十六进制颜色代码是字符向量或字符串标量，以井号 (`#`) 开头，后跟三个或六个十六进制数字，范围可以是 `0` 到 `F`。这些值不区分大小写。因此，颜色代码 `'#FF8800'` 与 `'#ff8800'`、`'#F80'` 与 `'#f80'` 是等效的。

  

  此外，还可以按名称指定一些常见的颜色。下表列出了命名颜色选项、等效 RGB 三元组和十六进制颜色代码。

  | 颜色名称    | 短名称 | RGB 三元组 | 十六进制颜色代码 | 外观                                                         |
  | :---------- | :----- | :--------- | :--------------- | :----------------------------------------------------------- |
  | `"red"`     | `"r"`  | `[1 0 0]`  | `"#FF0000"`      | ![Sample of the color red](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/hg_red.png) |
  | `"green"`   | `"g"`  | `[0 1 0]`  | `"#00FF00"`      | ![Sample of the color green](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/hg_green.png) |
  | `"blue"`    | `"b"`  | `[0 0 1]`  | `"#0000FF"`      | ![Sample of the color blue](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/hg_blue.png) |
  | `"cyan"`    | `"c"`  | `[0 1 1]`  | `"#00FFFF"`      | ![Sample of the color cyan](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/hg_cyan.png) |
  | `"magenta"` | `"m"`  | `[1 0 1]`  | `"#FF00FF"`      | ![Sample of the color magenta](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/hg_magenta.png) |
  | `"yellow"`  | `"y"`  | `[1 1 0]`  | `"#FFFF00"`      | ![Sample of the color yellow](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/hg_yellow.png) |
  | `"black"`   | `"k"`  | `[0 0 0]`  | `"#000000"`      | ![Sample of the color black](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/hg_black.png) |
  | `"white"`   | `"w"`  | `[1 1 1]`  | `"#FFFFFF"`      | ![Sample of the color white](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/hg_white.png) |

  以下是 MATLAB® 在许多类型的绘图中使用的默认颜色的 RGB 三元组和十六进制颜色代码。

  | RGB 三元组               | 十六进制颜色代码 | 外观                                                         |
  | :----------------------- | :--------------- | :----------------------------------------------------------- |
  | `[0 0.4470 0.7410]`      | `"#0072BD"`      | ![Sample of RGB triplet [0 0.4470 0.7410], which appears as dark blue](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/colororder1.png) |
  | `[0.8500 0.3250 0.0980]` | `"#D95319"`      | ![Sample of RGB triplet [0.8500 0.3250 0.0980], which appears as dark orange](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/colororder2.png) |
  | `[0.9290 0.6940 0.1250]` | `"#EDB120"`      | ![Sample of RGB triplet [0.9290 0.6940 0.1250], which appears as dark yellow](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/colororder3.png) |
  | `[0.4940 0.1840 0.5560]` | `"#7E2F8E"`      | ![Sample of RGB triplet [0.4940 0.1840 0.5560], which appears as dark purple](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/colororder4.png) |
  | `[0.4660 0.6740 0.1880]` | `"#77AC30"`      | ![Sample of RGB triplet [0.4660 0.6740 0.1880], which appears as medium green](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/colororder5.png) |
  | `[0.3010 0.7450 0.9330]` | `"#4DBEEE"`      | ![Sample of RGB triplet [0.3010 0.7450 0.9330], which appears as light blue](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/colororder6.png) |
  | `[0.6350 0.0780 0.1840]` | `"#A2142F"`      | ![Sample of RGB triplet [0.6350 0.0780 0.1840], which appears as dark red](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/colororder7.png) |

**示例：** `plot(G,'EdgeColor','r')` 创建一个具有红色边的图论图。

##### `LineStyle` — 线型 `'-'` （默认） | `'--'` | `':'` | `'-.'` | `'none'`

线型，指定为逗号分隔的对组，其中包含 `'LineStyle'` 和下表中列出的线型之一。

| 字符     | 线型   | 表示的线条                                                   |
| :------- | :----- | :----------------------------------------------------------- |
| `'-'`    | 实线   | ![Sample of a solid line](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/linestyle_solid.png) |
| `'--'`   | 虚线   | ![Sample of a dashed line](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/linestyle_dashed.png) |
| `':'`    | 点线   | ![Sample of a dotted line](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/linestyle_dotted.png) |
| `'-.'`   | 点划线 | ![Sample of a dash-dotted line](https://hila-1300222503.cos.ap-shanghai.myqcloud.com/md_image/linestyle_dashdotted.png) |
| `'none'` | 无线条 | 无线条                                                       |



##### `LineWidth` — 边线宽 `0.5` （默认） | 正值

边线宽，指定为逗号分隔的对组，其中包含 `'LineWidth'` 和一个正值（以磅为单位）。

**示例：** `0.75`



### size函数

```
sz = size(A) 返回一个行向量，其元素是 A 的相应维度的长度。例如，如果 A 是一个 3×4 矩阵，则 size(A) 返回向量 [3 4]。
```



### find函数

```
查找某个元素在向量中的位置：
m=find(A==5);  %A是向量，5是要查找的元素值，返回位置m
```



### ind2sub函数

```
[row,col] = ind2sub(sz,ind) 
返回数组 row 和 col，其中包含与大小为 sz 的矩阵的线性索引 ind 对应的等效行和列下标。
此处，sz 是包含两个元素的向量，其中 sz(1) 指定行数，sz(2) 指定列数。
```





## Dijkstra算法

### 功能：

求两点之间的最短路

### 条件：

边权是非负的情形

### matlab函数：

```
[path,d,edgepath] = shortestpath(G,start,end,'Method',algorithm)
```

### `algorithm` — 最短路径算法 `'auto'` （默认） | `'unweighted'` | `'positive'` | `'mixed'` | `'acyclic'`

最短路径算法，指定为下表中的选项之一。

| 选项                              | 描述                                                         |
| :-------------------------------- | :----------------------------------------------------------- |
| `'auto'`（默认值）                | `'auto'` 选项会自动选择算法：`'unweighted'` 用于没有边权重的 `graph` 和 `digraph` 输入。`'positive'` 用于具有边权重的所有 `graph` 输入，并要求权重为非负数。此选项还用于具有非负边权重的 `digraph` 输入。`'mixed'` 用于其边权重包含某些负值的 `digraph` 输入。图不能包含负循环。 |
| `'unweighted'`                    | 广度优先计算，将所有边权重都视为 `1`。                       |
| `'positive'`                      | Dijkstra 算法，要求所有边权重均为非负数。                    |
| `'mixed'`（仅适用于 `digraph`）   | 适用于有向图的 Bellman-Ford 算法，要求图没有负循环。尽管对于相同的问题，`'mixed'` 的速度慢于 `'positive'`，但 `'mixed'` 更为通用，因为它允许某些边权重为负数。 |
| `'acyclic'`（仅适用于 `digraph`） | 算法旨在改进具有加权边的有向无环图 (DAG) 的性能。使用 [`isdag`](https://ww2.mathworks.cn/help/matlab/ref/digraph.isdag.html) 确认有向图是否无环。 |

**注意**

对于大多数图，`'unweighted'` 是速度最快的算法，然后是 `'acyclic'`、`'positive'` 和 `'mixed'`。



### `P` — 节点之间的最短路径 节点索引 | 节点名称

节点之间的最短路径，以节点索引的向量或节点名称的数组形式返回。如果节点之间没有路径，则 `P` 为空，即 `{}`。

- 如果 `s` 和 `t` 包含数值节点索引，则 `P` 是节点索引的数值向量。
- 如果 `s` 和 `t` 包含节点名称，则 `P` 是包含节点名称的元胞数组或字符串数组。

如果 `s` 和 `t` 之间有多条最短路径，则 `P` 只包含其中一条路径。返回的路径可能根据 `Method` 指定的具体算法而有所不同。

### `d` — 最短路径距离 标量

最短路径距离，以数值标量形式返回。`d` 是 `P` 中连续节点之间的边权重的总和。如果节点之间没有路径，则 `d` 是 `Inf`。

### `edgepath` — 最短路径上的边 边索引向量

最短路径上的边，以边索引向量形式返回。对于多重图，此输出指示两个节点之间的哪条边位于该路径上。此输出与 [`highlight`](https://ww2.mathworks.cn/help/matlab/ref/matlab.graphics.chart.primitive.graphplot.highlight.html) 的 `'Edges'` 名称-值对组兼容，例如：`highlight(p,'Edges',edgepath)`。



## Floyd算法

### 功能：

求所有顶点对之间的最短路

### 条件：

允许赋权图包含负权的边或弧，但对赋权图中的每个圈，要求每个圈上所有弧的权总和为非负

### matlab代码

求距离矩阵和路径矩阵

```
a=zeros(4);
a(1,3)=10;
a(1,4)=60;
a(2,3)=5;
a(2,4)=20;
a(3,4)=1;
n=length(a)
b=a+a';
b(b==0)=inf;
b(1:n+1:end)=0;

R=zeros(n);


for k=1:n
    for i=1:n
        for j=1:n
            if b(i,k)+b(k,j)<b(i,j)
                b(i,j)=b(i,k)+b(k,j);
                R(i,j)=k;
            end
        end
    end
end
b
R

```

​		
