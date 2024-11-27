# WebGL 核心概念解释

## 基础概念

### WebGL 上下文 (Context)
就像画家需要画布才能作画，WebGL 需要一个"画布"来绘制 3D 图形。这个"画布"就是 WebGL 上下文。
```javascript
const gl = canvas.getContext('webgl');
```
当我们获取 WebGL 上下文时，就相当于准备好了画画的工具和场地。

### 着色器 (Shader)
着色器是在 GPU 上运行的小程序，就像是给 GPU 的"指令书"。

#### 顶点着色器 (Vertex Shader)
```glsl
attribute vec4 a_position;
void main() {
    gl_Position = a_position;
}
```
- 就像是在告诉 GPU "这些点应该画在哪里"
- 每个顶点（点）都会执行一次这个程序
- `attribute` 变量就像是从 JavaScript 传递给顶点着色器的"参数"

#### 片段着色器 (Fragment Shader)
```glsl
precision mediump float;
void main() {
    gl_FragColor = vec4(1.0, 0.0, 0.0, 1.0);
}
```
- 决定每个像素的颜色
- 就像是在告诉 GPU "这些点应该是什么颜色"
- `precision mediump float` 是在说"我们需要中等精度的小数"

## 数据传输

### 缓冲区 (Buffer)
```javascript
const positionBuffer = gl.createBuffer();
```
缓冲区就像是 GPU 的"记事本"，我们把要画的点的位置信息写在这个"记事本"上。

### 属性 (Attribute)
```javascript
const positionAttributeLocation = gl.getAttribLocation(program, 'a_position');
```
属性是着色器中的变量，用来接收从 JavaScript 传来的数据。就像是 GPU 和 JavaScript 之间的"传话筒"。

## 坐标系统

### 标准化设备坐标 (Normalized Device Coordinates)
WebGL 使用的坐标系统范围是 -1 到 1：
- (-1, -1) 是屏幕的左下角
- (1, 1) 是屏幕的右上角
- (0, 0) 是屏幕的中心

这就像是把整个画布标准化到一个 2x2 的正方形中。

## 渲染流程

### 视口 (Viewport)
```javascript
gl.viewport(0, 0, canvas.width, canvas.height);
```
视口定义了绘制区域的大小，就像是在画布上画一个"框"，告诉 WebGL "就在这个范围内画画"。

### 清除缓冲区 (Clear Buffer)
```javascript
gl.clearColor(1.0, 1.0, 1.0, 1.0);
gl.clear(gl.COLOR_BUFFER_BIT);
```
就像是用橡皮擦把画布擦干净，准备开始新的绘制。

### 绘制命令 (Draw Call)
```javascript
gl.drawArrays(gl.POINTS, 0, 5);
```
终于要开始画画了！这行代码就是在告诉 GPU：
- 画点 (`gl.POINTS`)
- 从第一个点开始 (`0`)
- 一共画 5 个点 (`5`)

## 在本教程中的应用

在我们的向量学习工具中：
1. 我们用 **顶点着色器** 来确定每个向量终点的位置
2. 用 **片段着色器** 给不同的向量设置不同的颜色
3. 通过 **缓冲区** 把向量的坐标传给 GPU
4. 使用 **标准化设备坐标** 在屏幕上直观地展示向量
5. 最后通过 **绘制命令** 把所有向量画出来

这些概念组合在一起，就构成了一个完整的 WebGL 应用，帮助我们可视化向量运算的结果。
