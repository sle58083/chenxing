# Chenxing 安装发布入口

本仓库公开提供 Yuchen Panel 的安装脚本、版本清单和 Release 安装包，供客户自行部署。

当前镜像版本：**1.0.6**。软件名称、安装目录和管理命令仍为 `yuchen-panel`。

## 一键安装

在目标 Linux VPS 上以 root 身份执行（优先支持 Ubuntu 22.04 / Debian 12）：

```bash
bash <(curl -fsSL https://raw.githubusercontent.com/sle58083/chenxing/main/install.sh)
```

安装入口读取本仓库的 `version.json`，从本仓库 Release 下载 ZIP，并验证 SHA256 后执行安装。安装会配置面板、Nginx 和相应运行服务；请在准备部署的 VPS 上执行。

安装完成后按终端提示访问面板，并执行：

```bash
yuchen-panel info
yuchen-panel status
yuchen-panel doctor
```

## 升级与切换更新源

通过本发布入口升级，重新执行同一条安装命令：

```bash
bash <(curl -fsSL https://raw.githubusercontent.com/sle58083/chenxing/main/install.sh)
```

本入口会向部署脚本传入 Chenxing 的版本清单地址，并保存为面板的更新源。原先从其他地址安装的实例，需执行该入口完成更新源切换；仅创建本仓库不会自动修改旧实例。

现有命令行更新助手默认地址可能仍指向原仓库。使用它检查本仓库版本时，请显式指定：

```bash
YC_UPDATE_MANIFEST_URL=https://raw.githubusercontent.com/sle58083/chenxing/main/version.json yuchen-panel update
```

更新助手用于查看更新信息；实际安装或升级推荐执行上面的 Chenxing 一键命令。

## 发布说明（v1.0.6）

当前发布版本为 **1.0.6（stable）**，版本清单记录的发布时间为 **2026-10-31（UTC）**。安装包为 `yuchen-panel-v1.0.6.zip`，来自上游 `sle58083/yuchen-panel` 的 v1.0.6 Release。

### 上游 v1.0.6 包含的主要能力

- **客户流量管理**：按客户 ID 汇总 Xray 上传与下载用量，客户列表显示本周期用量，并定时刷新。
- **到期和超限控制**：客户到期或超出流量限额时停用；在线执行限额通常会有约 30–60 秒延迟，异常情况下可能更久。
- **续费规则**：延长已有到期日时执行续费处理，清零本周期用量并恢复启用；长期客户首次设置到期日则保留原有用量与启用状态。
- **协议配置安全性**：修复均衡预设覆盖随机 gRPC `serviceName` 的问题，新建 gRPC 入站生成随机 12 位 `serviceName`；未填写 SOCKS5 用户名时生成随机 12 位用户名，已有或手动填写的值保持不变。
- **稳定性**：处理用量统计在重启、重复上报时的计量问题；修正升级后启动日志中的旧版本号。上游版本清单说明升级会轮换 JWT 密钥，升级后需重新登录。

上述功能属于**上游 Yuchen Panel v1.0.6**。Chenxing 仅提供安装入口、版本清单和 Release 镜像，**没有单独开发或修改这些软件功能**，也没有新增企业授权系统。

### 发布与升级注意事项

- 当前 Chenxing 安装包按上游 v1.0.6 原样镜像，两个仓库版本清单记录的 SHA256 相同；实际部署前仍建议核验下载文件。
- 原 `sle58083/yuchen-panel` 仓库未因 Chenxing 发布入口而修改。
- Chenxing 不会自动同步上游后续版本；新版本需要单独镜像、校验并更新本仓库版本清单。
- 安装包保留上游已有源码、文档和许可材料，不属于无源码发行包。
- 已安装实例需要重新运行本仓库的一键安装入口，才能按说明切换更新源；仅创建或更新此仓库不会自动升级旧实例。

完整来源、版本和校验值见 [PROVENANCE.md](PROVENANCE.md)；实际发布版本以 [version.json](version.json) 为准。
