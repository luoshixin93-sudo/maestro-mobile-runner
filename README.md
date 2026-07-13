# maestro-mobile-runner

**Fast UI test automation for Android, iOS, React Native, Flutter & Expo**

Open-source Maestro CLI runner — single binary, no JVM. 100% free, no features behind a paywall.

Supports real iOS devices, simulators, emulators, desktop browsers, and cloud providers.

[![License](https://img.shields.io/badge/license-Apache_2.0-blue.svg)](LICENSE)
[![Go Report Card](https://goreportcard.com/badge/github.com/luoshixin93-sudo/maestro-mobile-runner)](https://goreportcard.com/report/github.com/luoshixin93-sudo/maestro-mobile-runner)

---

## Overview

`maestro-mobile-runner` is a lightweight CLI tool that executes Maestro YAML flows on real devices, emulators, simulators, and desktop browsers. It is built from the same foundations as the popular Maestro framework, with cloud phone provider support and enhanced cross-platform compatibility.

- Runs Maestro YAML flows on real devices, emulators, simulators, and desktop browsers
- Supports Android (UIAutomator2), iOS (WebDriverAgent), Web (Chrome CDP), and cloud (Appium)
- Built-in parallel execution, HTML/JUnit/Allure reports, and JavaScript scripting
- Addresses [most of the top 100 most-discussed open issues](docs/maestro-issues-analysis.md) on Maestro's GitHub

## Install

```bash
curl -fsSL https://open.devicelab.dev/install/maestro-mobile-runner | bash

# Install a specific version
curl -fsSL https://open.devicelab.dev/install/maestro-mobile-runner | bash -s -- --version 1.0.9
```

## Run Tests

```bash
maestro-mobile-runner test flow.yaml                        # Android (default)
maestro-mobile-runner --platform ios test flow.yaml         # iOS
maestro-mobile-runner --platform web test flow.yaml         # Desktop browser (Chrome)
maestro-mobile-runner --app-file app.apk test flows/        # Install app and run
maestro-mobile-runner --driver appium --appium-url <server-url> test flow.yaml  # Appium
maestro-mobile-runner test --parallel 3 flows/             # Parallel on 3 devices
```

## Key Features

- **Zero migration** — Runs your existing Maestro YAML flows as-is, no changes needed
- **Real iOS device testing** — Supports physical iOS devices, not just simulators
- **Cloud testing** — BrowserStack, Sauce Labs, LambdaTest, TestingBot via Appium driver
- **Desktop browser testing** — Run Maestro flows on Chrome/Chromium via CDP
- **React Native & Flutter** — Smart element finding for RN testIDs and Flutter semantics
- **DeviceLab driver** — On-device Android driver via WebSocket, ~2x faster than UIAutomator2
- **Parallel execution** — Dynamic work distribution across devices
- **App install built-in** — `--app-file app.apk` installs the app before testing
- **Wide OS compatibility** — Android 5.0+ (API 21+) and iOS 12.0+, no version restrictions
- **Reports** — HTML, JUnit XML, and Allure-compatible reports out of the box
- **Clear error messages** — `element not found: text="Login"` instead of `io.grpc.StatusRuntimeException: UNKNOWN`
- **Pre-flight validation** — Catches flow errors, circular dependencies, and missing files before execution starts
- **Fast element finding** — Native selectors, clickable parent traversal, regex matching, smarter visibility
- **Reliable text input** — Direct ADB input with Unicode support, no dropped characters
- **scrollUntilVisible** — Native scroll implementation that reliably finds off-screen elements
- **Relative selectors** — Find elements by position: below, above, leftOf, rightOf, childOf
- **JavaScript scripting** — Embedded JS runtime with HTTP client for dynamic test logic
- **Configurable timeouts** — Per-command and per-flow timeouts, `--wait-for-idle-timeout 0` to disable
- **Lightweight** — Single binary, no JVM required

## Supported Platforms & Drivers

| Driver | Platform | Description |
|--------|----------|-------------|
| **UIAutomator2** | Android | Direct connection to device. Default driver, no external server needed. |
| **DeviceLab** | Android | `--driver devicelab`. On-device WebSocket driver, ~2x faster than UIAutomator2. |
| **WDA** (WebDriverAgent) | iOS | Auto-selected with `--platform ios`. Supports simulators and physical devices. |
| **Browser (CDP)** | Web | `--platform web`. Chrome/Chromium automation via Chrome DevTools Protocol. |
| **Appium** | Android & iOS | `--driver appium`. For cloud testing providers and existing Appium infrastructure. |

## Quick Start

### 1. Install dependencies

- **Android testing:** `adb` (Android SDK Platform-Tools)
- **iOS testing:** `xcrun` command-line tools (Xcode)
- **Web/Browser testing:** Chrome or Chromium
- **Cloud & Appium testing:** Appium 2.x or 3.x — works with local Appium servers and cloud providers (BrowserStack, Sauce Labs, LambdaTest, TestingBot)

### 2. Write a flow

```yaml
appId: com.example.app
---
- launchApp
- tapOn: "Login"
- inputText: "test@example.com"
- tapOn: "Submit"
- assertVisible: "Welcome"
```

### 3. Run

```bash
maestro-mobile-runner test flow.yaml
```

## Flow Config

`maestro-mobile-runner` extends the standard Maestro flow YAML with additional fields:

```yaml
commandTimeout: 10000       # Default per-command timeout (ms)
waitForIdleTimeout: 3000    # Device idle wait (ms), 0 to disable
---
- launchApp: com.example.app
- tapOn: "Login"
- assertVisible: "Welcome"
```

## CI/CD Integration

`maestro-mobile-runner` is built for CI/CD pipelines — single binary, no JVM startup, low memory footprint. Works with GitHub Actions, GitLab CI, Jenkins, CircleCI, and any CI system that supports Android emulators or iOS simulators.

```bash
# CI example: auto-start emulator, run tests, shutdown after
maestro-mobile-runner --auto-start-emulator --parallel 2 flows/
```

## Requirements

- **Android testing:** `adb` (Android SDK Platform-Tools)
- **iOS testing:** `xcrun` command-line tools (Xcode)
- **Web/Browser testing:** Chrome or Chromium
- **Cloud & Appium testing:** Appium 2.x or 3.x

## License

Apache License 2.0 — see [LICENSE](LICENSE).

---

*Made with ❤️ for cloud phone automation → [qtphone.com](https://www.qtphone.com/)*
