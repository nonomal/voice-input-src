**Language / 语言**: [English](#source-code-english) | [中文](#source-code-中文)

---

## Source Code (English)

```bash
claude \
  --dangerously-skip-permissions \
  --output-format=stream-json \
  --verbose \
  -p "Please implement a macOS menu-bar voice input app (Swift, macOS 14+) with the following requirements:

1. Hold the Fn key to record, release to inject the transcribed text into the currently focused input field. Use streaming transcription (Apple Speech Recognition framework) as preferred approach. Monitor Fn key globally via CGEvent tap, suppressing the Fn event to prevent triggering the emoji picker.
2. Default language must be Simplified Chinese (zh-CN), ensuring Chinese input recognition works out of the box. Also provide language switching options in the menu bar (English, Simplified Chinese, Traditional Chinese, Japanese, Korean). Language selection is stored in UserDefaults.
3. While recording, display an elegant frameless capsule-shaped floating window centered at the bottom of the screen — no traffic lights or titlebar. Use NSPanel (nonactivatingPanel) + NSVisualEffectView (.hudWindow material), sufficient height (56px, corner radius 28px), containing:
   - 5 vertical bar waveform animation on the left (44×32px), driven by real-time audio RMS levels (no hardcoded fake animations) — louder speech produces larger waveforms, quiet moments produce smaller ones. Bar weights are [0.5, 0.8, 1.0, 0.75, 0.55] creating a natural center-high, sides-low effect. Smooth envelope (attack 40%, release 15%), add ±4% random jitter per bar for organic feel. Waveforms should be large enough to be clearly visible.
   - Text label on the right (elastic width 160-560px) showing real-time transcription, capsule elastically widens as text grows
   - Entry spring animation (0.35s), text width smooth transition (0.25s), exit scale animation (0.22s)
4. Text injection uses clipboard + simulated Cmd+V paste. Before injection, detect the current input method: if it is a CJK input method, temporarily switch to an ASCII input source (ABC/US keyboard) before pasting, then restore the original input method after paste completes — this prevents CJK input methods from intercepting Cmd+V. Restore original clipboard contents after injection.
5. Integrate LLM to improve speech recognition accuracy, especially for mixed Chinese-English scenarios. Use an OpenAI-compatible API (configurable API Base URL, API Key, Model) to refine transcribed text. The LLM system prompt must be very conservative in corrections: only fix obvious speech recognition errors (e.g., Chinese homophone errors, English technical terms mistakenly converted to Chinese like 配森→Python, 杰森→JSON). Never rewrite, polish, or remove any content that appears correct — if the input looks correct, return it as-is.
6. Provide an LLM Refinement submenu in the menu bar with an enable/disable toggle and a Settings entry. The Settings window contains three input fields: API Base URL, API Key, Model — the API Key field must support being fully cleared — plus Test and Save buttons. After releasing Fn, if LLM is enabled and configured, the floating window shows a Refining... status, waiting for the LLM response before injecting the final text.
7. The app runs in LSUIElement mode (menu bar icon only, no Dock icon). Build with Swift Package Manager, provide a Makefile (build/run/install/clean), build output is a signed .app bundle."
```

---

## Source Code (中文)

```bash
claude \
  --dangerously-skip-permissions \
  --output-format=stream-json \
  --verbose \
  -p "请实现一个 macOS menu-bar 语音输入法应用（Swift，macOS 14+），具体要求：

1. 按住 Fn 键录音，松开后将转录文字注入当前聚焦的输入框。优先使用流式转录（Apple Speech Recognition framework）。Fn 键通过 CGEvent tap 全局监听，需抑制 Fn 事件传递以防止触发 emoji 选择器。
2. 默认语言必须为简体中文（zh-CN），确保开箱即用就能识别中文输入。同时在菜单栏提供语言切换选项（英语、简体中文、繁体中文、日语、韩语）。语言选择存储在 UserDefaults 中。
3. 录音时在屏幕底部居中显示一个特别优雅精致的无边框胶囊状悬浮窗，不要有红绿灯和 titlebar。使用 NSPanel（nonactivatingPanel）+ NSVisualEffectView（.hudWindow 材质），高度足够（56px，圆角半径 28px），包含：
   - 左侧 5 根竖条波形动画（44×32px），必须由实时音频 RMS 电平驱动（不要用写死的假动画），说话声音大波形就大、安静时波形就小。各竖条权重为 [0.5, 0.8, 1.0, 0.75, 0.55] 形成自然的中间高两侧低效果，平滑包络（attack 40%、release 15%），每根竖条添加 ±4% 随机抖动增加有机感。波形要足够大，清晰可见。
   - 右侧文字标签（弹性宽度 160-560px）实时显示转录文本，胶囊随文字变多而弹性变宽
   - 入场弹簧动画（0.35s）、文字宽度平滑过渡（0.25s）、退场缩放动画（0.22s）
4. 文字注入使用剪贴板 + 模拟 Cmd+V 粘贴方式，注入前需检测当前输入法：如果是 CJK 输入法，先临时切换到 ASCII 输入源（ABC/US 键盘）再粘贴，粘贴完成后恢复原输入法，防止中文输入法拦截 Cmd+V。注入完成后恢复原剪贴板内容。
5. 接入 LLM 来提升语音识别的准确率，尤其是中英文混杂的情况下。通过 OpenAI 兼容 API（可配置 API Base URL、API Key、Model）对转录文本进行 refine。LLM 的 system prompt 要求非常保守地纠错：只修复明显的语音识别错误（如中文谐音错误、英文技术术语被错误转为中文如「配森」→「Python」、「杰森」→「JSON」），绝对不要改写、润色或删除任何看起来正确的内容，如果输入看起来正确则必须原样返回。
6. 在菜单栏提供 LLM Refinement 子菜单，包含启用/禁用开关和 Settings 入口。Settings 窗口包含 API Base URL、API Key、Model 三个输入框，API Key 输入框要能完全清空，以及 Test 和 Save 按钮。松开 Fn 键后如果 LLM 已启用且已配置，悬浮窗显示 Refining... 状态，等 LLM 返回后再注入最终文本。
7. 应用以 LSUIElement 模式运行（仅菜单栏图标，无 Dock 图标）。使用 Swift Package Manager 构建，提供 Makefile（build/run/install/clean），构建产物为签名的 .app bundle。"
```

---

## Dist

https://github.com/yetone/voice-input-dist
