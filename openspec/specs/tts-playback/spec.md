## ADDED Requirements

### Requirement: 朗读按钮可见性
每个 `.poem-card` 卡片的标题行 SHALL 包含一个朗读按钮（扬声器图标），与现有的 `.poem-form` 标签并列显示。

#### Scenario: 卡片显示朗读按钮
- **WHEN** 页面加载完成
- **THEN** 每张 `.poem-card` 的 `.poem-card-header` 区域 SHALL 包含一个朗读按钮，按钮使用内联 SVG 扬声器图标

#### Scenario: 深色模式下按钮样式
- **WHEN** 页面处于深色模式（`data-theme="dark"`）
- **THEN** 朗读按钮的图标和边框颜色 SHALL 适配深色主题变量

### Requirement: 点击朗读童谣
用户点击朗读按钮时，系统 SHALL 使用 `window.speechSynthesis` API 朗读该卡片 `.poem-text` 区域内的文本内容，使用中文普通话语音（`zh-CN`）。

#### Scenario: 成功朗读
- **WHEN** 用户点击某张卡片的朗读按钮
- **THEN** 系统 SHALL 提取该卡片 `.poem-text` 内所有文本
- **THEN** 系统 SHALL 使用 `SpeechSynthesisUtterance` 以 `zh-CN` 语言朗读该文本
- **THEN** 朗读按钮 SHALL 切换为"正在朗读"状态（停止图标）

#### Scenario: 浏览器不支持 Speech API
- **WHEN** 用户浏览器不支持 `window.speechSynthesis`
- **THEN** 朗读按钮 SHALL 隐藏或不显示

### Requirement: 停止朗读
用户在朗读过程中点击停止按钮时，系统 SHALL 立即停止当前朗读。

#### Scenario: 点击停止
- **WHEN** 朗读正在进行中（按钮显示停止状态）
- **THEN** 用户点击该按钮
- **THEN** 系统 SHALL 调用 `speechSynthesis.cancel()` 停止朗读
- **THEN** 按钮 SHALL 恢复为初始播放状态

### Requirement: 单例朗读控制
系统 SHALL 确保同一时刻仅有一个朗读任务在执行。

#### Scenario: 播放新卡片自动停止前一个
- **WHEN** 卡片 A 正在朗读
- **AND** 用户点击卡片 B 的朗读按钮
- **THEN** 系统 SHALL 先停止卡片 A 的朗读
- **AND** 卡片 A 的按钮 SHALL 恢复为播放状态
- **THEN** 系统 SHALL 开始朗读卡片 B 的文本
- **AND** 卡片 B 的按钮 SHALL 切换为停止状态

#### Scenario: 朗读自然结束
- **WHEN** 某首童谣朗读自然结束（非用户手动停止）
- **THEN** 对应卡片的朗读按钮 SHALL 自动恢复为播放状态

### Requirement: 语音引擎预热
页面加载时 SHALL 预加载语音列表以减少首次朗读的延迟。

#### Scenario: 页面加载时获取语音列表
- **WHEN** 页面 DOM 加载完成
- **THEN** 系统 SHALL 调用 `speechSynthesis.getVoices()` 获取可用语音列表
- **AND** 系统 SHALL 监听 `voiceschanged` 事件以处理异步加载的语音列表
