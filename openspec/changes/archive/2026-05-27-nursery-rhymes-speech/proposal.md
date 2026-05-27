## Why

经典童谣页面（`jingdian-tongyao.html`）目前只有文字展示，缺少语音朗读功能。少儿用户（及其家长）需要能听每首童谣的普通话朗读，以辅助识字、培养语感、提升学习体验。使用浏览器原生 Web Speech API（SpeechSynthesis）实现零依赖、零成本的语音朗读能力。

## What Changes

- 在每张童谣卡片（`.poem-card`）上新增一个朗读按钮（扬声器图标）
- 点击按钮调用 `window.speechSynthesis` 朗读该卡片的童谣文本
- 朗读中按钮显示"停止"状态，再次点击可停止朗读
- 同一时刻只允许一个朗读任务（播放新卡片自动停止前一个）
- 页面加载时预加载中文语音引擎
- 自动选择中文普通话语音（`zh-CN`），提供语速控制

## Capabilities

### New Capabilities
- `tts-playback`: 使用浏览器 Web Speech API 实现卡片级普通话语音朗读，包含播放/停止控制、语音选择、语速调节

### Modified Capabilities

（无现有 spec 需要修改）

## Impact

- **代码变更**：仅修改 `h5/jingdian-tongyao.html`（内联 CSS + 内联 JS）
- **新增依赖**：无（使用浏览器原生 `SpeechSynthesis` API）
- **浏览器兼容性**：所有现代浏览器均支持 Web Speech API（Chrome/Safari/Edge/Firefox），移动端 Safari/iOS Chrome 同样支持
- **性能影响**：极小（仅在用户点击时触发，无后台运行）
- **离线支持**：需要网络连接加载语音引擎（部分浏览器首次使用时下载语音包）
