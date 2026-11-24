<div align="center">

<img src="https://github.com/user-attachments/assets/026417b7-2f71-4ea7-a203-c2b3b82096f9"
     width="120"
     alt="OneDash App Icon"
     style="border-radius: 22px;" />

# OneDash

**A lightweight, native macOS menu bar utility with a Liquid Glass interface — combining real-time system monitoring, window management, keyboard lock, quick mirror, and smart clipboard history.**

<p align="center">
  <img src="https://img.shields.io/badge/macOS-14.0+-000000?style=for-the-badge&logo=apple&logoColor=white" alt="macOS 14.0+" />
  <img src="https://img.shields.io/badge/Swift-6-F05138?style=for-the-badge&logo=swift&logoColor=white" alt="Swift 6" />
  <img src="https://img.shields.io/badge/UI-SwiftUI%20%2B%20AppKit-0A84FF?style=for-the-badge" alt="SwiftUI + AppKit" />
  <img src="https://img.shields.io/badge/License-MIT-34C759?style=for-the-badge" alt="MIT License" />
  <a href="https://ko-fi.com/A0A72B59US"><img src="https://img.shields.io/badge/Ko--fi-FF5E5B?style=for-the-badge&logo=ko-fi&logoColor=white" alt="Ko-fi" /></a>
</p>

[Download Latest Release](https://github.com/NguyenThanhDat2004/OneDash/releases/latest) •
[Features](#-features) •
[Installation](#-installation) •
[Permissions](#-permissions) •
[Architecture](#️-architecture--tech-stack) •
[Support](#-support)

</div>

---

## ✨ Features

### 📊 System Monitor
Real-time telemetry powered by low-level Mach/BSD system APIs with minimal overhead:
- **CPU Usage** — Accurate tick sampling with 32-bit wraparound protection.
- **Memory (RAM)** — Live active memory tracking.
- **Disk Storage** — Periodically refreshed storage utilization with fallback capacity checks.

### 🎥 Quick Mirror
- One-click instant camera preview directly from the menu bar — ideal for quick checks before meetings.

### ⌨️ Clean Mode (Keyboard Lock)
- Hardware-level keyboard lock so you can safely wipe down your MacBook keyboard without triggering accidental keystrokes.
- Displays an animated lock overlay; click the OneDash menu bar icon to unlock.

### 🪟 Window Management
Snap the frontmost window cleanly without leaving your workflow:

| Layout | Description |
| :--- | :--- |
| **Left Half** | Snap active window to the left half of the screen |
| **Center** | Center the active window |
| **Maximize** | Expand the active window to fill the visible workspace |
| **Right Half** | Snap active window to the right half of the screen |

### 📋 Smart Clipboard History
- Stores up to **20 items** supporting both **text** and **images**.
- Built-in **Levenshtein similarity deduplication** to prevent near-duplicate text clutter.
- Instant popup preview, one-click copy, and **Clear All** support.

### 🫧 Native Liquid Glass UI
- Built on a custom borderless, transparent `NSPanel` (`GlassPanelController`) instead of a standard `NSPopover`.
- Adapts automatically with native `.glassEffect(.clear)` on **macOS 26+** and a clean transparent presentation on **macOS 14–15**.
- Closes automatically on outside click or `Esc`.

---

## 🎨 Interface Preview

<!-- Replace with a real screenshot of your Liquid Glass panel when ready:
<div align="center">
  <img src="path/to/screenshot.png" width="360" alt="OneDash Liquid Glass Preview" />
</div>
-->

```text
╭──────────────────────────────────────╮
│  ◉ OneDash                           │
│    System Tools                      │
├──────────────────────────────────────┤
│  ╭────────────────────────────────╮  │
│  │  System Monitor                │  │
│  │  CPU 24%   RAM 58%   DISK 71%  │  │
│  │  ████░░░   ██████░   ███████░  │  │
│  ╰────────────────────────────────╯  │
│  ╭────────────────────────────────╮  │
│  │  🎥 Quick Mirror            ▶  │  │
│  │     Click to Start             │  │
│  ╰────────────────────────────────╯  │
│  ╭────────────────────────────────╮  │
│  │  ⌨️ Clean Mode            [○ ] │  │
│  │     Lock keyboard              │  │
│  ╰────────────────────────────────╯  │
│  ╭────────────────────────────────╮  │
│  │  Window Management             │  │
│  │  [ ◧ ]   [ ⊡ ]   [ ■ ]   [ ◨ ] │  │
│  ╰────────────────────────────────╯  │
│  ╭────────────────────────────────╮  │
│  │  📋 Clipboard History  (12)  › │  │
│  ╰────────────────────────────────╯  │
├──────────────────────────────────────┤
│  Quit                         v1.0.0 │
╰──────────────────────────────────────╯
```

---

## 🚀 Installation

### Option 1: Direct Download (Recommended)
1. Download `OneDash.zip` from the [GitHub Releases](https://github.com/NguyenThanhDat2004/OneDash/releases/latest) page.
2. Unzip and move **OneDash.app** into `/Applications`.
3. If macOS Gatekeeper blocks the unsigned binary on first launch, clear the quarantine flag:
   ```bash
   xattr -dr com.apple.quarantine /Applications/OneDash.app
   open /Applications/OneDash.app
   ```

### Option 2: Build from Source
Requires **Xcode 15+** and **macOS 14.0+**.

```bash
git clone [https://github.com/NguyenThanhDat2004/One_Dash_for_MacOS.git](https://github.com/NguyenThanhDat2004/One_Dash_for_MacOS.git)
cd One_Dash_for_MacOS

# Open in Xcode
open OneDash.xcodeproj

# Or build Release via CLI
xcodebuild -project OneDash.xcodeproj -scheme OneDash -configuration Release build
```

---

## 🔐 Permissions

OneDash requests only the permissions required by the features you use:

| Permission | Used For | How to Enable |
| :--- | :--- | :--- |
| **Accessibility** | Window Management & Keyboard Lock (`CGEventTap`) | **System Settings → Privacy & Security → Accessibility** → Enable **OneDash** |
| **Camera** | Quick Mirror | **System Settings → Privacy & Security → Camera** → Enable **OneDash** |

---

## 🛠️ Architecture & Tech Stack

| Layer | Technology | Role |
| :--- | :--- | :--- |
| **Language** | Swift 6, Objective-C | High-performance native macOS logic & low-level hardware hooks |
| **UI & Windowing** | SwiftUI, AppKit (`NSPanel`, `NSHostingView`) | Borderless Liquid Glass menu bar panel & fluid animations |
| **Reactive State** | MVVM + Combine (`@MainActor`) | Lifecycle-aware system telemetry & memory-safe bindings |
| **System Layer** | XNU (Mach / BSD), CoreGraphics, Accessibility API | CPU/RAM/Disk metrics, keyboard event interception, window frames |

---

## 🤝 Contributing

Contributions, bug reports, and feature ideas are welcome:

1. Fork the repository.
2. Create a branch: `git checkout -b feat/your-feature`
3. Commit your changes: `git commit -m "feat: describe your change"`
4. Push to your fork and open a Pull Request.

Found a bug? Please [open an issue](https://github.com/NguyenThanhDat2004/One_Dash_for_MacOS/issues) with your macOS version, chip (Apple Silicon / Intel), and steps to reproduce.

---

## ☕ Support

If you find **OneDash** useful, consider supporting its development:

<a href='https://ko-fi.com/A0A72B59US' target='_blank'><img height='36' style='border:0px;height:36px;' src='https://storage.ko-fi.com/cdn/kofi6.png?v=6' border='0' alt='Buy Me a Coffee at ko-fi.com' /></a>

---

## 📜 License

Released under the [MIT License](LICENSE).  
Copyright © 2026 **Nguyễn Thành Đạt**.
