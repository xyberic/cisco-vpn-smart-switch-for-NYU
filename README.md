# NYU/NYUSH VPN Smart Switch & Automator

🚀 本项目是一套专为纽约大学 (NYU/NYUSH) 同学打造的 **Cisco Secure Client (AnyConnect) VPN 全平台自动化智能切换工具**。

旨在解决大家每天上课、写代码、查文献时，频繁手动开启思科客户端、敲长密码、输入 `push` 以及应付 Duo 验证的繁琐痛点。通过本项目，你可以实现 **“无脑单入口控制：未连秒连，已连秒断”** 的极致网络体验。

---

## ✨ 核心特性 (Features)

* **🔄 智能双向切换 (Smart Switch)**：运行脚本时全自动检测网络状态。若 VPN 处于断开状态，则自动启动登录隧道；若已连接，则安全切断，全天候只需交互这一个入口。
* **🛠️ 强力路径探测**：地毯式兼容了 Windows (v4.x/v5.x 交叉路径)、macOS、Linux 下思科客户端的所有默认安装路径，免去手动配置环境变量的烦恼。
* **⚡ 彻底免疫闪退与乱码**：Windows 端强制 UTF-8 内核编码，移除了所有可能导致 CMD 编译器多字节对齐错位的特殊符号，稳定运行不闪退。

---

## 📥 下载与部署指南 (Installation & Usage)

为了保持代码仓库的整洁与安全，所有的功能脚本均已剥离并发布在 [GitHub Releases](../../releases) 页面中。请前往 Release 页面下载对应系统的最新脚本文件。

### 1. Windows 用户使用指南 (`.bat` 脚本)

#### ⚙️ 第一步：基础配置
1. 前往本仓库的 **Releases** 页面，下载最新的 `Cisco.shortcut.for.Windows.bat` 脚本文件。
2. 右键点击下载好的 `Cisco.shortcut.for.Windows.bat`，选择 **编辑**（或用记事本打开）。
3. 在脚本中段找到相应位置，将占位符替换为你自己的真实校园网凭据：
   * 将 [Your NetID] 修改为你自己的 NetID。
   * 将 [Your Password] 密码占位符修改为你自己的 NYU 密码。
4. 点击记事本左上角 **文件 ➔ 另存为**，确保窗口最下方的 **编码 (Encoding)** 务必选择为 **`UTF-8`**，然后保存覆盖。

#### 🎯 第二步：日常运行
* **管理员身份运行**：右键以管理员身份运行修改后的 `Cisco.shortcut.for.Windows.bat`。
  * **若处于未连接状态**：脚本会强行清理后台冲突进程并秒发验证请求。当看到黑色窗口提示 `Please approve DUO PUSH on your phone...` 时，**留意手机 Duo 弹窗并点击批准**。连接成功后，窗口会在 2 秒内静默自动关闭。
  * **若处于已连接状态**：再次双击，脚本会利落地切断校园网 VPN 连接，随后窗口自动蒸发。

---

### 2. MacOS & Linux 用户使用指南 (`.sh` 脚本)

#### ⚙️ 第一步：下载与权限解锁
1. 前往本仓库的 **Releases** 页面，下载最新的 `Cisco.shortcut.for.MacOS.sh` 或 `Cisco.shortcut.for.Linux.sh` 脚本文件。
2. 打开 **终端 (Terminal)**，使用 `cd` 命令切换到你下载该文件的目录下（例如：`cd ~/Downloads`）。
3. 执行以下命令，为脚本赋予系统级可执行权限：

   ```bash
   chmod +x Cisco.shortcut.for.MacOS.sh
   ```

   或

   ```bash
   chmod +x Cisco.shortcut.for.Linux.sh
   ```

#### 📝 第二步：凭据配置
1. 使用本地文本编辑器（如 `nano`、`vim` 或 VS Code）打开 `Cisco.shortcut.for.MacOS.sh` 或 `Cisco.shortcut.for.Linux.sh` 。
2. 在代码中段的 Here-Doc (`<<EOF`) 区域，将 [Your_NetID] 与 [Your_Password] 替换为你自己的真实 NetID 和密码。
3. 保存并关闭文件。

#### 🚀 第三步：终极偷懒技巧（命令行宏挂载）
为了让你连 `./Cisco.shortcut.for.MacOS.sh` 或 `./Cisco.shortcut.for.Linux.sh` 都不用输入，强烈建议将其挂载为系统全局别名（Alias）：
1. 在终端中根据你的 Shell 类型打开配置文件：
   * **Mac 用户**（默认 Zsh）：执行 `nano ~/.zshrc`
   * **Linux 用户**（默认 Bash）：执行 `nano ~/.bashrc`
2. 保存退出后，在终端执行 `source ~/.zshrc`（或 `source ~/.bashrc`）使其立刻生效。

**💡 日常使用体验**：此后你随时随地打开终端，**只需敲击 `vpn` 三个字母并回车**，即可全自动触发校园网连接或断开，并在 1秒 后自动干净地退出当前终端会话。

---

## 🔒 安全性与免责声明 (Security & Disclaimer)

1. **隐私安全警告**：本项目提供的脚本会以**明文形式**将你的校园网账户与密码保存在你本地的脚本文件中。**请务必妥善保管好你个人的本地文件！** 切勿将包含你真实密码的脚本上传至公开的 GitHub 仓库、公共代码网盘，或直接发送给不信任的人。
2. 本项目属于开源效率工具，仅用于学术交流与个人办公效率提升，未破坏、绕过或劫持任何远端多因子认证 (MFA) 的安全校验加固链。因使用者自身保管不当或误操作导致的账户安全风险，由使用者自行承担。
