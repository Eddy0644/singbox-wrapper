# singbox-wrapper

一个 sing-box 包装脚本，简化配置管理和服务部署流程。既保持了直接运行核心程序的灵活性，又尽量减少手改配置文件的不便。

本脚本会修改 sing-box 服务中的ExecStart字段，因此 sing-box 服务每次启动时都会调用本脚本重新生成配置文件再进入sing-box。

此外为了方便自建节点&手搓配置的用户，特设一机制，在配置文件的特定区域添加如下Flag `"▶️POST_Proxies_List"` `"▶️POST_Proxies_List_NoChain"`（包含双引号），脚本将会在运行时读取 `outbounds`列表并使用所有用户节点的 tags 列表替换掉上述Flag。（为了能够识别出用户的所有节点，您将需要在 `outbounds` 数组中、代理节点开始前添加顶格注释 `# User Proxies` 尾部添加 `# End User Proxies`）

```bash
curl -o singbox-wrapper https://testingcf.jsdelivr.net/gh/Eddy0644/singbox-wrapper/singbox-wrapper
```

（下方的部分文字由AI生成）

## ✨ 核心功能

### 🌐 快速开关
- **局域网访问切换**：快速在本地访问和局域网访问模式间切换
- **TUN 模式控制**
- **DNS 策略选择**：IPv4/IPv6 偏好、纯 IPv4 或纯 IPv6 模式

### ⚡ 用户体验
- **终端界面**：可直接通过命令行修改四个开关，无需打开编辑器
- **交互模式**：提供向导式配置更改提示界面
- **服务集成**：通过覆盖配置实现与 systemd 服务无缝集成

### 🛠️ 高级特性
- **用户代理处理**：提取并处理注释标记间的代理配置
- **模板替换**：自动将 `POST_Proxies_List` 占位符替换为实际的代理标签
- **链路检测**：为有链和直连代理分别生成代理列表
- **注释过滤**：智能移除注释行，同时保持配置完整性

## 📋 使用示例

```bash
# 交互式配置
./singbox-wrapper

# 快速设置
./singbox-wrapper set TUN=1
./singbox-wrapper set LAN=0  
./singbox-wrapper set dnsStrategy=prefer_ipv6

# 服务集成
sudo ./singbox-wrapper install
systemctl restart sing-box
```

## 🚀 快速开始

1. **安装**：将脚本放置在合适位置并（sudo）运行 `./singbox-wrapper i`
2. **配置**：调整脚本头部的一些设置
3. **部署**：重启 sing-box 服务 - 配置将自动生成


