# Chenxing 安装发布入口

本仓库公开提供 Yuchen Panel 的安装脚本、版本清单和 Release 安装包，供客户自行部署。

当前镜像版本：**1.0.3**。软件名称、安装目录和管理命令仍为 `yuchen-panel`。

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

现有 1.0.3 命令行更新助手默认地址仍指向原仓库。使用它检查本仓库版本时，请显式指定：

```bash
YC_UPDATE_MANIFEST_URL=https://raw.githubusercontent.com/sle58083/chenxing/main/version.json yuchen-panel update
```

更新助手用于查看更新信息；实际安装或升级推荐执行上面的 Chenxing 一键命令。

## 发布说明

- 安装包从上游已发布的 1.0.3 原样镜像，校验值一致；不对软件功能进行改动。
- 原 `sle58083/yuchen-panel` 仓库内容未因本发布入口而修改。
- 本仓库不自动同步上游新版本；后续版本需单独发布。
- 本次仅建立公开下载入口，尚未新增企业授权系统。
- 安装包保留上游已有源码、文档和许可材料；本仓库不宣称安装包为无源码版本。

详细来源与校验值见 [PROVENANCE.md](PROVENANCE.md)。
