# 环形槽计算器 (Ring Groove Calculator)

[English](#english) | [中文](#chinese)

## 中文

一个用于数控车床环形槽加工的辅助工具，自动生成 Fanuc 格式 G 代码。支持带倒角的环形槽参数化设计，并提供坐标数据预览与程序导出功能。

### ✨ 功能特点

- **参数化设计**：支持设置最大/最小直径、台阶深度、粗切余量、C1/C2 倒角大小与角度、加工进给等参数。
- **自动生成程序**：根据输入参数智能生成数控 G 代码（Fanuc 格式），支持粗切与精切逻辑。
- **倒角延长线**：C1 倒角从接近高度直接斜线切入，C2 倒角支持终点向下延伸，符合实际加工工艺。
- **坐标数据展示**：自动计算并显示关键节点坐标（X/Z 值），便于验证刀具路径。
- **导出与复制**：支持一键复制程序或导出为 `.txt` 文件，方便传输至数控系统。
- **粗切预览**：实时显示粗切刀数、直径范围与深度。
- **示例参数 & 清除功能**：一键加载示例参数，或一键清空所有输入。
- **深色/浅色模式**：跟随系统自动切换主题，护眼舒适。
- **移动端适配**：响应式设计，支持手机、平板、桌面设备。

### 📐 参数说明

#### 几何参数

| 参数 | 说明 |
|------|------|
| **最大直径 D₁** | 环形槽大径（mm） |
| **最小直径 D₂** | 环形槽小径（mm） |
| **台阶深度 Zs** | 环形槽轴向深度（mm） |

#### C1 倒角（大径处上侧）

| 参数 | 说明 |
|------|------|
| **C₁ 倒角大小** | 斜边长度（mm），角度与 Z 轴夹角 |
| **A₁ 角度** | 倒角与 Z 轴的夹角（°） |
| **接近高度 Z_app** | 斜线切入的起点 Z 坐标（mm） |

> 计算逻辑：Z 向深度 = C₁ × sin(A₁)，直径变化 = 2 × C₁ × cos(A₁)，从接近高度直接斜线切入至终点。

#### C2 倒角（小径处下侧）

| 参数 | 说明 |
|------|------|
| **C₂ 倒角大小** | 斜边长度（mm），角度与 Z 轴夹角 |
| **A₂ 角度** | 倒角与 Z 轴的夹角（°） |
| **C₂ 终点向下延伸** | 倒角终点再向 Z 负方向延伸的距离（mm） |

> 计算逻辑：先水平移动至台阶底部理论起点（X = D₂ + 直径变化），再斜线切入至延伸后的终点。

#### 加工参数

| 参数 | 说明 |
|------|------|
| **精切进给 F** | 精加工进给速度（mm/min） |
| **粗切进给 F₂** | 粗加工进给速度（mm/min） |
| **安全高度 Z_safe** | 快速移动的安全 Z 坐标（mm） |
| **粗切余量** | 粗加工保留的 Z 向余量（台阶深度 > 1.0 时生效） |
| **粗切步长** | 直径方向每次粗切的增量（mm） |
| **退刀间隙 X** | 粗切退刀时的 X 向安全距离（mm） |

### 🔧 生成程序示例

以下为示例参数生成的 Fanuc 程序：

```gcode
N1
T1
M20
G98
M03S1500
G0X24.00
Z2.00
G01Z-1.70F250
G0U-1.00Z2.00
G0Z20.0
G0X22.62
Z2.00
G01X18.20Z-0.21F200
G01Z-2.20F200
G01X13.22F200
G01X11.80Z-2.91F200
G0Z20.0
M30
```

📊 坐标数据表格
工具会自动生成关键节点坐标：

节点	X 直径 (mm)	Z 深度 (mm)	说明
C1 斜线起点	22.62	2.00	从 Z=2.00 开始斜线切入
C1 倒角终点	18.20	-0.21	C1 终点 (D₁)
台阶底部	18.20	-2.20	槽底平面
C2 起点	13.22	-2.20	水平移动到此处
C2 终点	11.80	-2.91	终点向下延伸 0.50 mm
🚀 使用方法
打开 index.html 文件。

在参数配置卡片中输入几何、倒角、加工参数。

程序将实时自动生成，无需点击“生成”按钮。

可通过“复制程序”按钮将 G 代码复制到剪贴板。

可通过“输出 txt 格式”按钮将程序保存为 .txt 文件。

使用“示例参数”按钮加载演示数据，或使用“清除全部参数”重置表单。

查看“关键坐标点”表格验证刀路。

🛠️ 技术栈
HTML5：结构

CSS3：样式（渐变背景、玻璃拟态、响应式布局，支持深色/浅色模式）

JavaScript (ES6)：核心计算与交互

无外部依赖：纯原生实现

👥 作者
开发者：鱼 (Xiaowuyu273637)
AI 辅助：DeepSeek AI

📄 开源协议
本项目采用 MIT 许可证。

🙏 致谢
感谢所有测试和使用本工具的朋友，特别感谢 DeepSeek AI 提供的算法优化与技术支持。


### Ring Groove Calculator

[English](#english) | [Chinese](#chinese)

## English

An auxiliary tool for CNC lathe ring groove machining that automatically generates Fanuc format G-code. Supports parametric design of ring grooves with chamfers, and provides coordinate data preview and program export.

### ✨ Features

- **Parametric Design**: Set max/min diameter, step depth, roughing stock, C1/C2 chamfer sizes/angles, machining feeds, etc.
- **Auto-Generate Program**: Intelligently generates CNC G-code (Fanuc format) based on input, supports roughing and finishing logic.
- **Chamfer Extension Lines**: C1 chamfer cuts directly from approach height; C2 chamfer supports downward extension of the end point, matching actual machining practice.
- **Coordinate Data Display**: Automatically calculates and displays key node coordinates (X/Z values) for toolpath verification.
- **Export & Copy**: One-click copy of program or export as `.txt` file for easy transfer to CNC systems.
- **Roughing Preview**: Real-time display of number of roughing passes, diameter range, and depth.
- **Example & Clear**: One-click load example parameters or clear all inputs.
- **Dark/Light Mode**: Automatically follows system theme for eye comfort.
- **Mobile Friendly**: Responsive design, works on phones, tablets, and desktops.

### 📐 Parameter Explanation

#### Geometry Parameters

| Parameter | Description |
|-----------|-------------|
| **Max Diameter D₁** | Large diameter of ring groove (mm) |
| **Min Diameter D₂** | Small diameter of ring groove (mm) |
| **Step Depth Zs** | Axial depth of ring groove (mm) |

#### C1 Chamfer (Upper side at large diameter)

| Parameter | Description |
|-----------|-------------|
| **C₁ Chamfer Size** | Hypotenuse length (mm), angle relative to Z-axis |
| **A₁ Angle** | Chamfer angle from Z-axis (°) |
| **Approach Height Z_app** | Starting Z coordinate of oblique cut (mm) |

> Calculation logic: Z depth = C₁ × sin(A₁), diameter change = 2 × C₁ × cos(A₁), direct oblique cut from approach height to end point.

#### C2 Chamfer (Lower side at small diameter)

| Parameter | Description |
|-----------|-------------|
| **C₂ Chamfer Size** | Hypotenuse length (mm), angle relative to Z-axis |
| **A₂ Angle** | Chamfer angle from Z-axis (°) |
| **C₂ End Point Downward Extension** | Distance to extend the chamfer end point further in -Z direction (mm) |

> Calculation logic: First move horizontally to theoretical start point at step bottom (X = D₂ + diameter change), then oblique cut to extended end point.

#### Machining Parameters

| Parameter | Description |
|-----------|-------------|
| **Finishing Feed F** | Finishing feed rate (mm/min) |
| **Roughing Feed F₂** | Roughing feed rate (mm/min) |
| **Safe Height Z_safe** | Safe Z coordinate for rapid traverse (mm) |
| **Roughing Stock** | Z-direction stock left for roughing (effective when step depth > 1.0) |
| **Roughing Step** | Diameter increment per roughing pass (mm) |
| **Retract Clearance X** | X-direction safety distance for roughing retract (mm) |

### 🔧 Example Generated Program

Example Fanuc program generated with sample parameters:

```gcode
N1
T1
M20
G98
M03S1500
G0X24.00
Z2.00
G01Z-1.70F250
G0U-1.00Z2.00
G0Z20.0
G0X22.62
Z2.00
G01X18.20Z-0.21F200
G01Z-2.20F200
G01X13.22F200
G01X11.80Z-2.91F200
G0Z20.0
M30
```

📊 Coordinate Data Table
The tool automatically generates key node coordinates:

Node	X Diameter (mm)	Z Depth (mm)	Description
C1 Oblique Start	22.62	2.00	Start oblique cut from Z=2.00
C1 Chamfer End	18.20	-0.21	C1 end point (D₁)
Step Bottom	18.20	-2.20	Groove bottom plane
C2 Start	13.22	-2.20	Horizontal move to here
C2 End	11.80	-2.91	End point extended downward by 0.50 mm
🚀 Usage
Open the index.html file.

Enter geometry, chamfer, and machining parameters in the configuration card.

The program is generated automatically and instantly – no "Generate" button needed.

Use the "Copy Program" button to copy G-code to clipboard.

Use the "Export as txt" button to save the program as a .txt file.

Use "Example Parameters" to load demo data, or "Clear All" to reset the form.

Check the "Key Coordinates" table to verify the toolpath.

🛠️ Tech Stack
HTML5: Structure

CSS3: Styling (gradient backgrounds, glassmorphism, responsive layout, dark/light mode support)

JavaScript (ES6): Core calculation and interaction

No external dependencies: Pure vanilla implementation

👥 Authors
Developer: Yu (Xiaowuyu273637)

AI Assistance: DeepSeek AI

📄 License
This project is licensed under the MIT License.

🙏 Acknowledgements
Thanks to all who tested and used this tool, and special thanks to DeepSeek AI for algorithm optimization and technical support.
