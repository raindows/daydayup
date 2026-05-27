## 1. CSS 样式

- [x] 1.1 添加 `.speak-btn` 按钮基础样式（圆形按钮，border 与主题变量一致，与 `.poem-form` 标签尺寸协调）
- [x] 1.2 添加 `.speak-btn.playing` 朗读中状态样式（accent 色填充/高亮）
- [x] 1.3 添加深色模式适配（`[data-theme="dark"] .speak-btn` 图标和边框颜色）
- [x] 1.4 添加 `@media(max-width:768px)` 移动端响应式适配

## 2. HTML 结构

- [x] 2.1 在每个 `.poem-card-header` 中的 `.poem-form` 标签后面添加朗读按钮，包含扬声器 SVG 图标和停止 SVG 图标（切换显示）

## 3. JavaScript 功能

- [x] 3.1 实现 `initTTS()` 函数：页面加载时调用 `speechSynthesis.getVoices()` 预热语音引擎，监听 `voiceschanged` 事件
- [x] 3.2 实现 `getChineseVoice()` 函数：从语音列表中选择 `zh-CN` 普通话语音
- [x] 3.3 实现 `toggleSpeak(btn)` 函数：点击按钮时提取卡片 `.poem-text` 文本，创建 `SpeechSynthesisUtterance` 并朗读
- [x] 3.4 实现单例控制：播放新卡片前先 `cancel()` 当前朗读，重置前一个按钮状态
- [x] 3.5 实现 `onend` 回调：朗读自然结束时自动恢复按钮为播放状态
- [x] 3.6 添加浏览器兼容检测：不支持 `speechSynthesis` 时隐藏所有朗读按钮
- [x] 3.7 在页面 `<script>` 末尾调用 `initTTS()`，并为所有朗读按钮绑定 `onclick` 事件

## 4. 验证

- [x] 4.1 本地预览确认 60 张卡片均显示朗读按钮
- [x] 4.2 测试点击播放、点击停止、切换卡片朗读功能
- [x] 4.3 测试深色模式下按钮样式正确
- [x] 4.4 测试移动端（768px 以下）按钮显示和交互正常
