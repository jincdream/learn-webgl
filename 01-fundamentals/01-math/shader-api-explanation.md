# WebGL 着色器 API 详解

## 创建着色器函数 (createShader)

### 1. `gl.createShader(type)`
```javascript
const shader = gl.createShader(type);
```
- 作用：创建一个新的着色器对象
- 参数 `type` 可以是：
  - `gl.VERTEX_SHADER`：创建顶点着色器
  - `gl.FRAGMENT_SHADER`：创建片段着色器
- 返回：一个新的着色器对象

### 2. `gl.shaderSource(shader, source)`
```javascript
gl.shaderSource(shader, source);
```
- 作用：设置着色器的源代码
- 参数：
  - `shader`：之前创建的着色器对象
  - `source`：着色器的源代码（GLSL 语言编写的字符串）
- 类比：就像是把代码写入一个文件

### 3. `gl.compileShader(shader)`
```javascript
gl.compileShader(shader);
```
- 作用：编译着色器代码
- 参数：要编译的着色器对象
- 类比：就像是把源代码编译成机器可以理解的形式

### 4. `gl.getShaderParameter(shader, gl.COMPILE_STATUS)`
```javascript
if (!gl.getShaderParameter(shader, gl.COMPILE_STATUS))
```
- 作用：检查着色器是否编译成功
- 参数：
  - `shader`：要检查的着色器
  - `gl.COMPILE_STATUS`：表示要检查编译状态
- 返回：`true` 表示编译成功，`false` 表示失败

### 5. `gl.getShaderInfoLog(shader)`
```javascript
console.error('着色器编译错误:', gl.getShaderInfoLog(shader));
```
- 作用：获取着色器编译错误信息
- 参数：出错的着色器对象
- 返回：包含错误详情的字符串
- 使用场景：调试着色器代码时非常有用

### 6. `gl.deleteShader(shader)`
```javascript
gl.deleteShader(shader);
```
- 作用：删除着色器对象，释放内存
- 参数：要删除的着色器
- 使用场景：编译失败或不再需要时清理资源

## 创建着色器程序函数 (createProgram)

### 1. `gl.createProgram()`
```javascript
const program = gl.createProgram();
```
- 作用：创建一个着色器程序对象
- 返回：新的程序对象
- 类比：相当于创建一个新的应用程序

### 2. `gl.attachShader(program, shader)`
```javascript
gl.attachShader(program, vertexShader);
gl.attachShader(program, fragmentShader);
```
- 作用：将编译好的着色器附加到程序对象
- 参数：
  - `program`：着色器程序
  - `shader`：要附加的着色器（顶点或片段）
- 类比：就像是把不同的模块组装到一个程序中

### 3. `gl.linkProgram(program)`
```javascript
gl.linkProgram(program);
```
- 作用：链接着色器程序
- 参数：要链接的程序对象
- 类比：就像是把所有的代码模块连接成一个可执行程序

### 4. `gl.getProgramParameter(program, gl.LINK_STATUS)`
```javascript
if (!gl.getProgramParameter(program, gl.LINK_STATUS))
```
- 作用：检查程序是否链接成功
- 参数：
  - `program`：要检查的程序
  - `gl.LINK_STATUS`：表示要检查链接状态
- 返回：`true` 表示链接成功，`false` 表示失败

### 5. `gl.getProgramInfoLog(program)`
```javascript
console.error('着色器程序链接错误:', gl.getProgramInfoLog(program));
```
- 作用：获取程序链接错误信息
- 参数：出错的程序对象
- 返回：包含错误详情的字符串
- 使用场景：调试链接错误时使用

## 完整流程图解

```
创建着色器
↓
设置源代码
↓
编译着色器
↓
检查编译状态
↓
创建程序
↓
附加着色器
↓
链接程序
↓
检查链接状态
↓
程序准备就绪
```

## 错误处理最佳实践

1. 总是检查编译状态
2. 编译失败时获取详细错误信息
3. 及时清理失败的着色器对象
4. 检查程序链接状态
5. 链接失败时获取详细错误信息

这些 API 的组合使用，构成了 WebGL 中着色器初始化的完整流程，确保了着色器代码能够正确地在 GPU 上运行。
