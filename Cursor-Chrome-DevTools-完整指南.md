# 🚀 Cursor Chrome DevTools 完整安装与使用指南

> **让 AI 助手直接控制浏览器，实现自动化测试、网页操作和调试的强大工具**
>
> ---
>
> ## 📋 目录
>
> - [简介](#简介)
> - - [系统要求](#系统要求)
>   - - [安装步骤](#安装步骤)
>     - - [配置方法](#配置方法)
>       - - [使用方法](#使用方法)
>         - - [实用技巧与妙用](#实用技巧与妙用)
>           - - [常见问题](#常见问题)
>             - - [总结](#总结)
>              
>               - ---
>
> ## 📖 简介
>
> **Cursor Chrome DevTools MCP** 是一个强大的工具，它允许 Cursor AI 助手通过 Chrome DevTools Protocol 直接控制 Chrome 浏览器。这意味着你可以：
>
> - 🤖 让 AI 自动操作网页
> - - 🧪 进行自动化测试
>   - - 🐛 调试网页问题
>     - - 📊 分析网页性能
>       - - 🎯 执行复杂的网页交互任务
>        
>         - ---
>
> ## ⚙️ 系统要求
>
> 在开始安装之前，请确保你的系统满足以下要求：
>
> ### 必需软件
>
> - **Node.js**: 版本要求 `^20.19.0` 或 `^22.12.0` 或 `>=23`
> -   - ⚠️ **重要**: Node.js v22.11.0 及以下版本**不支持**
>     -   - 推荐使用 Node.js 23.x 或 22.12.0 LTS
>         - - **npm**: 随 Node.js 一同安装
>           - - **Chrome/Chromium 浏览器**: 任何现代版本
>             - - **Cursor 编辑器**: 最新版本
>              
>               - ### 检查当前版本
>              
>               - ```bash
>                 # 检查 Node.js 版本
>                 node -v
>
>                 # 检查 npm 版本
>                 npm -v
>                 ```
>
> ---
>
> ## 🔧 安装步骤
>
> ### 步骤 1: 确保 Node.js 版本正确
>
> 如果你的 Node.js 版本不符合要求，需要先升级：
>
> #### Windows 用户（使用 nvm-windows）
>
> ```bash
> # 查看已安装的版本
> nvm list
>
> # 安装 Node.js 23.x（推荐）
> nvm install 23.11.1
>
> # 切换到新版本
> nvm use 23.11.1
>
> # 设置为默认版本（可选）
> # 编辑 C:\Users\你的用户名\AppData\Roaming\nvm\settings.txt
> # 添加: current: 23.11.1
> ```
>
> #### macOS/Linux 用户（使用 nvm）
>
> ```bash
> # 安装 Node.js 23.x
> nvm install 23.11.1
>
> # 设置为默认版本
> nvm alias default 23.11.1
>
> # 使用新版本
> nvm use 23.11.1
> ```
>
> ### 步骤 2: 安装 chrome-devtools-mcp
>
> ```bash
> # 全局安装（推荐）
> npm install -g chrome-devtools-mcp@latest
>
> # 或者使用 npx（无需全局安装）
> # npx chrome-devtools-mcp@latest
> ```
>
> ### 步骤 3: 验证安装
>
> ```bash
> # 检查是否安装成功
> npx chrome-devtools-mcp@latest --help
> ```
>
> ---
>
> ## ⚙️ 配置方法
>
> ### 1. 打开 Cursor MCP 配置
>
> 1. 打开 Cursor 编辑器
> 2. 2. 按 `Ctrl + Shift + P` (Windows/Linux) 或 `Cmd + Shift + P` (macOS)
>    3. 3. 输入 "MCP" 或 "Settings"
>       4. 4. 选择 **"Preferences: Open User Settings (JSON)"** 或找到 MCP 设置
>         
>          5. ### 2. 配置 MCP 服务器
>         
>          6. 编辑 `mcp.json` 文件（通常在 `~/.cursor/mcp.json` 或 `C:\Users\你的用户名\.cursor\mcp.json`）：
>         
>          7. ```json
> {
>   "mcpServers": {
>     "Chrome DevTools": {
>       "command": "npx",
>       "args": [
>         "chrome-devtools-mcp@latest"
>       ],
>       "env": {}
>     }
>   }
> }
> ```
>
> ### 3. 启动 Chrome 远程调试模式
>
> Chrome DevTools MCP 需要通过远程调试端口连接 Chrome。有两种方式：
>
> #### 方式 A: 手动启动 Chrome（推荐用于测试）
>
> ```bash
> # Windows
> chrome.exe --remote-debugging-port=9222
>
> # macOS
> /Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --remote-debugging-port=9222
>
> # Linux
> google-chrome --remote-debugging-port=9222
> ```
>
> #### 方式 B: 创建启动脚本（推荐用于日常使用）
>
> **Windows 批处理脚本** (`start-chrome-debug.bat`):
>
> ```batch
> @echo off
> taskkill /F /IM chrome.exe 2>nul
> start "" "C:\Program Files\Google\Chrome\Application\chrome.exe" --remote-debugging-port=9222 --user-data-dir="%TEMP%\chrome-debug"
> ```
>
> **macOS/Linux Shell 脚本** (`start-chrome-debug.sh`):
>
> ```bash
> #!/bin/bash
> pkill -f "chrome.*remote-debugging-port"
> /Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --remote-debugging-port=9222 --user-data-dir=/tmp/chrome-debug &
> ```
>
> 记得给脚本添加执行权限：
>
> ```bash
> chmod +x start-chrome-debug.sh
> ```
>
> ### 4. 重启 Cursor
>
> 配置完成后，**重启 Cursor 编辑器**使配置生效。
>
> ---
>
> ## 🎯 使用方法
>
> ### 基本使用流程
>
> 1. **启动 Chrome（远程调试模式）**
> 2.    ```bash
>          # 使用你创建的启动脚本
>          ./start-chrome-debug.sh
>          ```
>
> 2. **在 Cursor 中启用 Chrome DevTools**
> 3.    - 打开 Cursor Chat
>       -    - 确保 MCP 服务器已连接（检查状态栏）
>        
>            - 3. **开始使用**
>              4.    在 Chat 中输入指令，例如：
>              5.   ```
>                      使用 Chrome DevTools 打开 https://www.example.com
>                      ```
>
> ### 常用命令示例
>
> #### 1. 打开网页
>
> ```
> 请使用 Chrome DevTools 打开 https://github.com
> ```
>
> #### 2. 查找并点击元素
>
> ```
> 在页面上找到"Sign in"按钮并点击它
> ```
>
> #### 3. 填写表单
>
> ```
> 在登录表单中填写用户名和密码
> 用户名: testuser
> 密码: testpass
> ```
>
> #### 4. 截图
>
> ```
> 请截取当前页面的完整截图
> ```
>
> #### 5. 获取页面信息
>
> ```
> 分析当前页面的性能指标
> ```
>
> ---
>
> ## ✨ 实用技巧与妙用
>
> ### 🎨 1. 自动化网页测试
>
> **场景**: 测试网站功能是否正常
>
> ```
> 使用 Chrome DevTools 打开 https://example.com
> 然后执行以下操作：
> 1. 点击导航栏的"产品"链接
> 2. 滚动到页面底部
> 3. 填写联系表单
> 4. 截图保存结果
> ```
>
> ### 📊 2. 性能分析
>
> **场景**: 分析网页加载性能
>
> ```
> 打开 https://example.com
> 启动性能追踪
> 分析页面加载时间、LCP、FID 等核心指标
> 生成性能报告
> ```
>
> ### 🔍 3. 网页内容抓取
>
> **场景**: 批量获取网页信息
>
> ```
> 打开 https://example.com/products
> 提取所有产品名称和价格
> 以 JSON 格式返回结果
> ```
>
> ### 🎯 4. 自动化操作流程
>
> **场景**: 重复性任务自动化
>
> ```
> 每天自动执行：
> 1. 打开公司内部系统
> 2. 登录账户
> 3. 填写日报
> 4. 提交并截图确认
> ```
>
> ### 🐛 5. 调试网页问题
>
> **场景**: 快速定位问题
>
> ```
> 打开 https://example.com
> 检查控制台错误
> 分析网络请求
> 找出性能瓶颈
> ```
>
> ### 📱 6. 响应式设计测试
>
> **场景**: 测试不同设备尺寸
>
> ```
> 打开 https://example.com
> 将窗口调整为 iPhone 12 Pro 尺寸 (390x844)
> 截图保存
> 然后调整为 iPad Pro 尺寸 (1024x1366)
> 再次截图
> ```
>
> ### 🔐 7. 表单自动化填写
>
> **场景**: 快速填写复杂表单
>
> ```
> 打开注册页面
> 自动填写所有必填字段：
> - 姓名: 张三
> - 邮箱: zhangsan@example.com
> - 电话: 13800138000
> - 地址: 北京市朝阳区...
> 提交表单
> ```
>
> ### 📸 8. 批量截图
>
> **场景**: 为多个页面生成截图
>
> ```
> 依次打开以下页面并截图：
> 1. https://example.com/page1
> 2. https://example.com/page2
> 3. https://example.com/page3
> 保存所有截图到本地
> ```
>
> ---
>
> ## ❓ 常见问题
>
> ### Q1: 提示 "Node.js 版本不支持"
>
> **问题**:
> ```
> ERROR: chrome-devtools-mcp does not support Node v22.11.0
> ```
>
> **解决方案**:
> 1. 检查当前 Node.js 版本: `node -v`
> 2. 2. 升级到支持的版本（22.12.0+ 或 23.x）
>    3. 3. 使用 nvm 切换版本
>      
>       4. ### Q2: Chrome 无法连接
>      
>       5. **问题**: MCP 无法连接到 Chrome
>      
>       6. **解决方案**:
> 1. 确保 Chrome 以远程调试模式启动
> 2. 2. 检查端口 9222 是否被占用
>    3. 3. 确认防火墙没有阻止连接
>       4. 4. 尝试使用 `--user-data-dir` 参数启动独立的 Chrome 实例
>         
>          5. ### Q3: Cursor 中看不到 Chrome DevTools
>         
>          6. **问题**: MCP 服务器未显示
>         
>          7. **解决方案**:
> 1. 检查 `mcp.json` 配置是否正确
> 2. 2. 重启 Cursor 编辑器
>    3. 3. 查看 Cursor 的输出日志（Help > Toggle Developer Tools）
>       4. 4. 确认 `chrome-devtools-mcp` 已正确安装
>         
>          5. ### Q4: 操作网页时出现错误
>         
>          6. **问题**: 某些操作失败
>         
>          7. **解决方案**:
> 1. 确保页面已完全加载
> 2. 2. 等待动态内容加载完成
>    3. 3. 检查元素选择器是否正确
>       4. 4. 尝试使用更具体的元素定位方式
>         
>          5. ### Q5: 性能问题
>         
>          6. **问题**: 操作响应缓慢
>         
>          7. **解决方案**:
> 1. 关闭不必要的 Chrome 扩展
> 2. 2. 使用独立的用户数据目录
>    3. 3. 减少同时打开的标签页
>       4. 4. 检查系统资源使用情况
>         
>          5. ---
>         
>          6. ## 🎓 高级技巧
>         
>          7. ### 1. 自定义 Chrome 启动参数
>
> ```bash
> chrome --remote-debugging-port=9222 \
>        --user-data-dir=/tmp/chrome-debug \
>        --disable-extensions \
>        --disable-plugins \
>        --no-first-run \
>        --no-default-browser-check
> ```
>
> ### 2. 使用环境变量配置
>
> 在 `mcp.json` 中添加环境变量：
>
> ```json
> {
>   "mcpServers": {
>     "Chrome DevTools": {
>       "command": "npx",
>       "args": ["chrome-devtools-mcp@latest"],
>       "env": {
>         "CHROME_DEBUG_PORT": "9222"
>       }
>     }
>   }
> }
> ```
>
> ### 3. 多浏览器实例
>
> 可以同时启动多个 Chrome 实例，使用不同端口：
>
> ```bash
> # 实例 1
> chrome --remote-debugging-port=9222
>
> # 实例 2
> chrome --remote-debugging-port=9223
> ```
>
> ---
>
> ## 📚 相关资源
>
> - [Chrome DevTools Protocol 文档](https://chromedevtools.github.io/devtools-protocol/)
> - - [Cursor 官方文档](https://cursor.sh/docs)
>   - - [MCP 协议规范](https://modelcontextprotocol.io/)
>     - - [GitHub Issues](https://github.com/modelcontextprotocol/servers/issues)
>      
>       - ---
>
> ## 🎉 总结
>
> 通过 Cursor Chrome DevTools MCP，你可以：
>
> ✅ **自动化网页操作** - 让 AI 帮你完成重复性任务
> ✅ **快速调试问题** - 实时分析网页性能和错误
> ✅ **批量处理数据** - 自动提取和处理网页内容
> ✅ **提升开发效率** - 在编辑器中直接控制浏览器
>
> **开始使用吧！** 🚀
>
> ---
>
> ## 📝 更新日志
>
> - **2025-01-XX**: 初始版本发布
> -   - 支持基本的浏览器控制功能
>     -   - 支持页面导航、元素操作、截图等功能
>      
>         - ---
>
> **💡 提示**: 如果遇到问题，请查看 [常见问题](#常见问题) 部分，或提交 Issue 到项目仓库。
>
> **⭐ 如果这个工具对你有帮助，请给项目点个 Star！**
>
> ---
>
> *最后更新: 2025年1月*
