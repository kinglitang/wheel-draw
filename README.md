# 🎉 SVG 转盘抽奖 / Lucky Wheel Draw

一个基于 SVG 的精美转盘抽奖应用，使用纯前端技术（HTML + CSS + JavaScript）实现。

A beautiful lottery wheel application based on SVG, built with pure front-end technologies (HTML + CSS + JavaScript).

## ✨ 特性 / Features

### 中文特性
- 🎨 **精美 UI 设计**：渐变背景 + 圆点纹理效果
- 🎯 **SVG 绘制转盘**：使用 SVG 技术绘制高质量的转盘图形
- 🔄 **流畅动画**：自然的缓动效果，转盘旋转体验流畅
- 🎲 **概率控制**：每个奖项可配置不同的中奖概率
- 💾 **本地存储**：使用 localStorage 保存用户 ID 和抽奖次数
- 📊 **抽奖历史**：记录并显示历史抽奖结果
- 🎁 **首次提升**：首次抽奖可设置特殊概率（当前设置为必中"谢谢参与"）
- 🔢 **次数限制**：支持限制每个用户的抽奖次数
- 📱 **响应式设计**：自适应不同屏幕尺寸

### English Features
- 🎨 **Beautiful UI Design**: Gradient background with dotted texture effect
- 🎯 **SVG Wheel Rendering**: High-quality wheel graphics using SVG technology
- 🔄 **Smooth Animations**: Natural easing effect for smooth wheel rotation
- 🎲 **Probability Control**: Each prize can be configured with different winning probabilities
- 💾 **Local Storage**: Save user ID and remaining chances using localStorage
- 📊 **Draw History**: Record and display historical draw results
- 🎁 **First-time Boost**: Special probability settings for first-time draws
- 🔢 **Attempt Limits**: Support for limiting each user's number of draws
- 📱 **Responsive Design**: Adapts to different screen sizes

## 🎮 使用方法 / Usage

### 中文说明

1. **打开应用**：在浏览器中打开 `index.html` 文件
2. **查看奖项**：转盘上显示了所有可能的奖项
3. **开始抽奖**：点击"开始抽奖"按钮
4. **查看结果**：等待转盘停止，系统会弹窗显示中奖结果
5. **查看历史**：页面下方会记录所有的抽奖历史

### English Instructions

1. **Open the App**: Open the `index.html` file in your browser
2. **View Prizes**: The wheel displays all possible prizes
3. **Start Drawing**: Click the "开始抽奖" (Start Draw) button
4. **View Results**: Wait for the wheel to stop, and the system will show a popup with the winning result
5. **View History**: All draw history is recorded at the bottom of the page

## 🎁 奖项配置 / Prize Configuration

当前配置了 14 个奖项，每个奖项包含名称和概率：

Currently configured with 14 prizes, each containing a name and probability:

| 奖项名称 / Prize Name | 概率 / Probability |
|---------------------|-------------------|
| 看电影 / Watch a Movie | 5% |
| 吃big披萨 / Big Pizza | 10% |
| 谢谢参与 / Thank You | 5% (×4) |
| 游乐场一日游 / Amusement Park | 5% |
| 拍拍立得 / Polaroid Photo | 10% |
| 小荷包一天使用权 / Wallet Access | 10% |
| 50元红包 / 50 Yuan Red Packet | 10% |
| 买蛋糕 / Buy a Cake | 10% |
| 吃云贵川 / Yun-Gui-Chuan Cuisine | 10% |
| 去沈阳玩一天 / Day Trip to Shenyang | 5% |
| 任意要求一次 / Any Request | 5% |

## ⚙️ 技术实现 / Technical Implementation

### 核心技术 / Core Technologies
- **HTML5**: 页面结构 / Page structure
- **CSS3**: 样式和动画 / Styling and animations
- **JavaScript ES6**: 业务逻辑 / Business logic
- **SVG**: 转盘图形绘制 / Wheel graphics rendering
- **LocalStorage**: 数据持久化 / Data persistence

### 关键功能实现 / Key Features Implementation

#### 1. SVG 转盘绘制 / SVG Wheel Rendering
```javascript
// 使用 SVG path 绘制扇形区域
// Using SVG path to draw sector areas
const path = document.createElementNS("http://www.w3.org/2000/svg", "path");
path.setAttribute("d", `M${centerX},${centerY} L${x1},${y1} A${radius},${radius} 0 ${largeArc},1 ${x2},${y2} Z`);
```

#### 2. 概率抽奖算法 / Probability Algorithm
```javascript
// 基于累积概率的随机选择
// Random selection based on cumulative probability
function choosePrize() {
  const totalProb = prizes.reduce((sum, p) => sum + p.probability, 0);
  const rand = Math.random() * totalProb;
  let cumulative = 0;
  for (const prize of prizes) {
    cumulative += prize.probability;
    if (rand <= cumulative) return prize;
  }
  return prizes[prizes.length - 1];
}
```

#### 3. 旋转动画 / Rotation Animation
```javascript
// 使用 CSS transform 和 cubic-bezier 缓动函数
// Using CSS transform with cubic-bezier easing function
svg.style.transition = "transform 4s cubic-bezier(0.25, 1, 0.5, 1)";
svg.style.transform = `rotate(${finalRotation}deg)`;
```

#### 4. 用户识别 / User Identification
```javascript
// 使用 localStorage 生成并保存唯一用户 ID
// Generate and save unique user ID using localStorage
function getUserId() {
  let uid = localStorage.getItem('wheel_user_id');
  if (!uid) {
    uid = 'u_' + Math.random().toString(36).slice(2) + Date.now();
    localStorage.setItem('wheel_user_id', uid);
  }
  return uid;
}
```

## 🔧 自定义配置 / Customization

### 修改奖项 / Modify Prizes
在 `index.html` 中找到 `prizes` 数组并修改：

Find the `prizes` array in `index.html` and modify it:

```javascript
const prizes = [
  { name: "奖品名称", probability: 0.1 },  // 10% 概率
  // 添加更多奖项...
];
```

### 修改抽奖次数 / Modify Draw Attempts
修改 `maxChance` 变量：

Modify the `maxChance` variable:

```javascript
let maxChance = 3; // 默认3次 / Default 3 times
```

### 修改首次抽奖概率 / Modify First-time Draw Probability
在 `spin()` 函数中修改：

Modify in the `spin()` function:

```javascript
if (isFirstSpin) {
  boostFirstPrize(prizes, originalProbabilities, "谢谢参与", 1);  // 第三个参数是目标奖项，第四个参数是概率
}
```

### 修改转盘圈数 / Modify Rotation Rounds
```javascript
const rotateRounds = 5; // 转5圈 / Rotate 5 rounds
```

## 📁 项目结构 / Project Structure

```
wheel-draw/
├── index.html          # 主页面文件（包含 HTML、CSS、JavaScript）
│                       # Main page file (includes HTML, CSS, JavaScript)
└── README.md          # 项目说明文档 / Project documentation
```

## 🚀 部署 / Deployment

### 本地运行 / Local Development
直接在浏览器中打开 `index.html` 即可运行。

Simply open `index.html` in your browser.

### 在线部署 / Online Deployment
可以部署到任何静态网站托管服务：

Can be deployed to any static website hosting service:

- GitHub Pages
- Netlify
- Vercel
- 阿里云 OSS / Alibaba Cloud OSS
- 腾讯云 COS / Tencent Cloud COS

只需将 `index.html` 上传即可。

Just upload the `index.html` file.

## 🎨 界面预览 / UI Preview

- 渐变背景：紫色到蓝色的优雅渐变效果
- 圆点纹理：增加视觉层次感
- 转盘设计：每个扇区使用不同的 HSL 颜色，自动分布
- 指针设计：红色三角形指针，带阴影效果
- 文字自适应：长文本自动换行，保持美观

---

- Gradient Background: Elegant gradient from purple to blue
- Dotted Texture: Adds visual depth
- Wheel Design: Each sector uses different HSL colors, automatically distributed
- Pointer Design: Red triangle pointer with shadow effect
- Adaptive Text: Long text automatically wraps for better appearance

## 📝 许可证 / License

本项目采用 MIT 许可证。

This project is licensed under the MIT License.

## 🤝 贡献 / Contributing

欢迎提交 Issue 和 Pull Request！

Issues and Pull Requests are welcome!

## 👨‍💻 作者 / Author

kinglitang

---

**Note**: 此项目为娱乐用途，请勿用于商业博彩活动。

**Note**: This project is for entertainment purposes only. Do not use it for commercial gambling activities.
