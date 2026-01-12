<div align="center">

# 🔍 FlowEye

**流量之眼 - 智能被动漏洞扫描平台**

[![Go Version](https://img.shields.io/badge/Go-1.21+-00ADD8?style=flat-square&logo=go)](https://golang.org)
[![License](https://img.shields.io/badge/License-MIT-blue?style=flat-square)](LICENSE)
[![Release](https://img.shields.io/github/v/release/YingxueSec/Floweye-yyyxxx.cc?style=flat-square)](https://github.com/YingxueSec/Floweye-yyyxxx.cc/releases)

[快速开始](#-快速开始) • [功能特性](#-功能特性) • [使用教程](#-使用教程) • [下载](#-下载)

</div>

---

## 📖 项目简介

**FlowEye（流量之眼）** 是一款专为安全测试人员打造的 Web 化被动漏洞扫描平台。通过与 Burp Suite 无缝集成，FlowEye 能够实时接收并分析 HTTP 流量，自动进行多维度漏洞检测，帮助安全研究人员高效发现 Web 应用安全风险。
<img width="3440" height="1918" alt="1768234128824" src="https://github.com/user-attachments/assets/d27f7ad4-9539-4349-9b47-2e8d3926a3c9" />

### 为什么选择 FlowEye？

| 特性 | 描述 |
|------|------|
| 🎯 **精准识别** | 内置 1000+ 指纹规则，自动识别目标技术栈 |
| 🧠 **智能调度** | 根据指纹结果智能选择扫描引擎，避免无效扫描 |
| ⚡ **高效扫描** | 多引擎并行，支持 Shiro/Struts2/SQL注入/XSS 等漏洞检测 |
| 🖥️ **现代界面** | React + TailwindCSS 构建的精美 Web UI |
| 📦 **开箱即用** | 单文件可执行，无需复杂配置 |

## ✨ 功能特性
<img width="3440" height="1918" alt="1768234200696" src="https://github.com/user-attachments/assets/244a9800-3e47-4ba4-8cb6-946ff6553352" />

### 核心功能

- ✅ **零配置启动** - 无需任何配置文件，开箱即用
- ✅ **完全嵌入** - 前端 UI + 字典 + 规则全部内置到二进制
- ✅ **智能指纹识别** - 自动识别 Spring/Shiro/Struts2 等框架（1000+ 规则）
- ✅ **多引擎扫描** - SQLi/XSS/RCE/目录扫描/反序列化等
- ✅ **实时监控** - WebSocket 实时推送扫描结果
- ✅ **漏洞去重** - 智能过滤重复漏洞
- ✅ **Webhook 告警** - 支持飞书/钉钉/企业微信/Slack

### 扫描引擎

| 引擎 | 功能 | 规则数 |
|------|------|--------|
| **fingerprint** | 指纹识别 | 1000+ |
| **dirscan** | 敏感路径扫描 | 内置字典 |
| **shiro** | Apache Shiro 反序列化 | 100+ keys |
| **spring** | Spring 框架漏洞 | CVE-2018-1273, CVE-2022-22965 |
| **struts2** | Struts2 RCE | 多个 CVE |
| **sqli-fuzz** | SQL 注入检测 | 100+ payloads |
| **xss-fuzz** | XSS 跨站脚本 | 80+ payloads |
| **lfi-fuzz** | 本地文件包含 | 50+ payloads |
| **nuclei** | Nuclei 模板引擎 | 可扩展 |
<img width="3424" height="1918" alt="1768234226410" src="https://github.com/user-attachments/assets/21cfaa43-913e-4e7f-b1e1-758e3f7aa392" />

## 🚀 快速开始

### 1. 下载

前往 [Releases](https://github.com/YingxueSec/Floweye-yyyxxx.cc/releases) 页面下载最新版本：

```
floweye-v0.1.0-final.tar.gz
```

解压后包含：
- 多平台可执行文件（macOS/Linux/Windows）
- Burp Suite 插件
- 使用文档

### 2. 启动服务

```bash
# macOS Apple Silicon
./floweye-darwin-arm64

# macOS Intel
./floweye-darwin-amd64

# Linux
./floweye-linux-amd64

# Windows
floweye-windows-amd64.exe
```

启动后访问：**http://localhost:8080**

### 3. Burp Suite 集成

1. 打开 Burp Suite
2. 进入 **Extensions** → **Installed**
3. 点击 **Add**，选择 `floweye-burp-plugin-1.0.0.jar`
4. 确认插件加载成功
5. 通过 Burp 浏览目标网站，FlowEye 自动接收流量并扫描

## 📚 使用教程

### 基础配置

FlowEye 支持零配置启动，如需自定义配置，在可执行文件同目录创建 `config.yaml`：

```yaml
server:
  port: 8080              # 服务端口
  host: "0.0.0.0"         # 监听地址

filter:
  domain_whitelist:       # 域名白名单
    - "*.example.com"
    - "api.target.com"
  enable_dedup: true      # 启用去重

webhook:
  enabled: true
  provider: feishu        # 飞书/钉钉/企业微信
  webhook_url: "https://open.feishu.cn/open-apis/bot/v2/hook/xxx"
  min_severity: high      # 最低告警级别
```

### Webhook 告警配置

支持多种告警平台：

**飞书**
```yaml
webhook:
  enabled: true
  provider: feishu
  webhook_url: "https://open.feishu.cn/open-apis/bot/v2/hook/xxx"
  secret: "your-secret"
  min_severity: high
```

**钉钉**
```yaml
webhook:
  enabled: true
  provider: dingtalk
  webhook_url: "https://oapi.dingtalk.com/robot/send?access_token=xxx"
  secret: "your-secret"
  min_severity: high
```

**企业微信**
```yaml
webhook:
  enabled: true
  provider: wecom
  webhook_url: "https://qyapi.weixin.qq.com/cgi-bin/webhook/send?key=xxx"
  min_severity: high
```

### 白名单配置

建议配置域名白名单，避免扫描无关目标：

```yaml
filter:
  domain_whitelist:
    - "*.target.com"      # 支持通配符
    - "api.example.com"   # 精确匹配
    - "192.168.1.*"       # IP 段
```

### 引擎管理

在 Web UI 的 **扫描引擎** 页面可以：
- 启用/禁用特定引擎
- 查看引擎统计信息
- 调整扫描参数

## 📊 界面预览

### 仪表盘
实时统计流量、漏洞、指纹识别结果

### 流量监控
查看所有 HTTP 流量，支持搜索和过滤

### 漏洞管理
漏洞列表、详情、复测、导出报告

### 指纹识别
查看识别到的技术栈和框架

### 系统设置
配置 Webhook、白名单、引擎参数

## 🔧 技术栈

| 组件 | 技术 |
|------|------|
| 后端框架 | Go 1.21+ / Gin |
| 数据库 | SQLite 3 |
| 前端框架 | React 18 / TypeScript |
| UI 库 | TailwindCSS / shadcn/ui |
| Burp 插件 | Java / Montoya API |

## 📝 使用建议

1. **白名单配置**: 建议配置域名白名单，避免扫描无关目标
2. **告警推送**: 配置 Webhook 实时接收高危漏洞通知
3. **定期清理**: 数据库默认保留 30 天，可在设置中调整
4. **资源限制**: 建议在测试环境使用，避免对生产环境造成影响

## ❓ 常见问题

### Q: 如何更新到最新版本？
A: 下载最新版本的可执行文件替换即可，数据库会自动迁移。

### Q: 支持哪些操作系统？
A: 支持 macOS (Intel/Apple Silicon)、Linux (x64)、Windows (x64)。

### Q: 数据存储在哪里？
A: 数据存储在 `./data/floweye.db` SQLite 数据库中。

### Q: 如何备份数据？
A: 直接复制 `data/floweye.db` 文件即可。

### Q: 可以在服务器上运行吗？
A: 可以，建议配置 `host: "0.0.0.0"` 允许远程访问，注意配置防火墙。

## 🐛 问题反馈

如遇到问题，请提供：
- 操作系统版本
- 错误日志（如有）
- 复现步骤

提交 Issue: [GitHub Issues](https://github.com/YingxueSec/Floweye-yyyxxx.cc/issues)

## 📄 开源协议与使用限制

本项目采用 [MIT License](LICENSE) 开源协议。

### ⚠️ 重要声明

**本项目仅供个人学习、研究和合法授权的安全测试使用。**

#### 禁止行为

- ❌ **禁止商业化使用** - 未经授权不得将本工具用于任何商业目的
- ❌ **禁止二次开发售卖** - 不得基于本项目进行二次开发后进行商业销售
- ❌ **禁止未授权扫描** - 不得对未经授权的目标进行扫描测试
- ❌ **禁止用于非法用途** - 不得用于任何违法违规活动

#### 免责声明

1. 使用本工具造成的任何后果由使用者自行承担
2. 开发者不对工具的误用、滥用承担任何责任
3. 使用前请确保已获得目标系统所有者的明确授权
4. 请遵守当地法律法规和网络安全相关规定

#### 合法使用场景

- ✅ 个人学习和安全研究
- ✅ 企业内部安全测试（需获得授权）
- ✅ 渗透测试项目（需签订合法合同）
- ✅ 漏洞赏金计划（需遵守平台规则）

**如需商业授权或定制开发，请联系作者。**

## 🙏 致谢

感谢以下开源项目：
- [Gin](https://github.com/gin-gonic/gin) - HTTP Web 框架
- [React](https://react.dev/) - 前端框架
- [TailwindCSS](https://tailwindcss.com/) - CSS 框架
- [Nuclei](https://github.com/projectdiscovery/nuclei) - 漏洞扫描引擎

---

<div align="center">

**FlowEye** - 让流量无处遁形 👁️

[下载使用](https://github.com/YingxueSec/Floweye-yyyxxx.cc/releases) • [问题反馈](https://github.com/YingxueSec/Floweye-yyyxxx.cc/issues)

</div>
