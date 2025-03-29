

---

# MT7981 固件炼丹炉：一键成砖大师2

🎉 **欢迎体验 MT7981 固件炼丹炉！** 🎉  
这是一个基于 GitHub Actions 的自动化固件编译工具，支持 MT7981 平台的 OpenWrt 固件编译，覆盖多个版本和机型。无论是新手还是老手，都能一键生成属于你的专属固件！

## 项目简介

本项目通过 GitHub Actions 自动化编译 MT7981 平台的 OpenWrt 固件，支持以下版本：
- **OpenWrt 23.05**（基于 [padavanonly/immortalwrt-mt798x-23.05](https://github.com/padavanonly/immortalwrt-mt798x-23.05)）
- **OpenWrt 24.10**（基于 [padavanonly/immortalwrt-mt798x-24.10](https://github.com/padavanonly/immortalwrt-mt798x-24.10)）
- **Lede**（基于 [coolsnowwolf/lede](https://github.com/coolsnowwolf/lede)）

编译完成后，固件会发布到 GitHub Releases（仅包含 `sysupgrade.bin` 和 `factory.bin`），并可选上传到私有 WebDAV（包含所有 `.zip` 文件）。

## 功能特点

- **一键编译**：通过 GitHub Actions 自动化编译，无需本地环境。
- **多版本支持**：支持 OpenWrt 23.05、24.10 和 Lede 版本。
- **机型适配**：支持多种 MT7981 机型，自动适配源码和机型转换。
- **默认 IP 修改**：将默认管理地址设置为 `192.168.2.1`。
- **灵活发布**：
  - GitHub Releases：仅发布 `sysupgrade.bin` 和 `factory.bin`。
  - WebDAV（可选）：上传所有固件的 `.zip` 压缩包。

## 使用说明

### 1. 准备工作
- **Fork 本仓库**：将本仓库 Fork 到您的 GitHub 账户。
- **配置 WebDAV（可选）**：
  如果需要将固件上传到私有 WebDAV，请在 `Settings > Secrets and variables > Actions > Secrets` 中添加以下 Secrets：
  - `WEBDAV_URL`：例如 `http://<您的VPS_IP>/firmware`
  - `WEBDAV_USER`：WebDAV 用户名
  - `WEBDAV_PASSWORD`：WebDAV 密码
  如果不配置 WebDAV，上传步骤会自动跳过。

### 2. 触发编译
1. 进入仓库的 `Actions` 页面。
2. 选择 `MT7981固件炼丹炉：一键成砖大师2` 工作流。
3. 点击 `Run workflow`，选择以下参数：
   - **OpenWrt 版本**：`23.05`、`24.10` 或 `lede`。
   - **机型**：从支持的机型列表中选择（详见下文）。
4. 点击 `Run workflow` 启动编译。

### 3. 获取固件
- **GitHub Releases**：
  - 编译完成后，固件会发布到 `Releases` 页面。
  - 仅包含 `sysupgrade.bin` 和 `factory.bin` 文件，可直接下载。
- **WebDAV（如果配置）**：
  - 所有固件（包括 `kernel.bin`）会以 `.zip` 格式上传到 WebDAV。
  - 路径格式：`<WEBDAV_URL>/<版本>/<机型>/<文件名>.zip`

### 4. 刷机建议
- **管理地址**：`192.168.2.1`
- **默认密码**：
  - Lede 版本：`password`
  - 23.05 和 24.10 版本：无密码
- **刷机前**：请备份原固件，以防变砖。
- **刷机后**：如果路由器变砖，请尝试恢复，或在 Issues 中反馈（附上日志）。

## 支持的版本和机型

### 支持的版本
- **23.05**：基于 padavanonly 的 ImmortalWrt 分支。
- **24.10**：基于 padavanonly 的 ImmortalWrt 分支，支持更多新机型。
- **Lede**：基于 coolsnowwolf 的 Lede 分支，支持最广泛的机型。

### 支持的机型

#### 23.05 和 24.10 通用机型
| 机型                        | 说明                     |
|-----------------------------|--------------------------|
| abt_asr3000                | -                        |
| cetron_ct3003              | -                        |
| cmcc_a10                   | -                        |
| cmcc_rax3000m-emmc         | -                        |
| cmcc_rax3000m              | -                        |
| h3c_nx30pro                | -                        |
| imou_lc-hx3001             | -                        |
| jcg_q30                    | -                        |
| konka_komi-a31             | -                        |
| livinet_zr-3020            | -                        |
| mt7981-360-t7-108M         | -                        |
| mt7981-clt-r30b1           | -                        |
| mt7981-clt-r30b1-112M      | -                        |
| xiaomi_mi-router-ax3000t   | -                        |
| xiaomi_mi-router-ax3000t-stock | -                    |
| xiaomi_mi-router-wr30u-112m | -                       |
| xiaomi_mi-router-wr30u-stock | -                     |

#### 24.10 独有机型
| 机型                        | 说明                     |
|-----------------------------|--------------------------|
| huasifei_wh3000-emmc       | 24.10 新增机型           |
| cmcc_rax3000m-emmc-usboffload | 24.10 新增机型        |
| cmcc_rax3000m-usboffload   | 24.10 新增机型           |

#### Lede 独有机型
| 机型                        | 说明                     |
|-----------------------------|--------------------------|
| asus_tuf-ax4200            | -                        |
| asus_tuf-ax6000            | -                        |
| bananapi_bpi-r3            | -                        |
| bananapi_bpi-r3-mini-emmc  | -                        |
| bananapi_bpi-r3-mini-nand  | -                        |
| bananapi_bpi-r4            | -                        |
| bananapi_bpi-r4-poe        | -                        |
| cetron_ct3003-mod          | -                        |
| cmcc_a10-mod               | -                        |
| cmcc_rax3000m-nand         | -                        |
| cmcc_xr30-nand             | -                        |
| cudy_tr3000-mod            | -                        |
| cudy_tr3000-v1             | -                        |
| fzs_5gcpe-p3               | -                        |
| glinet_gl-mt2500           | -                        |
| glinet_gl-mt3000           | -                        |
| glinet_gl-mt6000           | -                        |
| glinet_gl-x3000            | -                        |
| glinet_gl-xe3000           | -                        |
| h3c_magic-nx30-pro         | -                        |
| hf_m7986r1-emmc            | -                        |
| hf_m7986r1-nand            | -                        |
| jcg_q30-pro                | -                        |
| jdcloud_re-cs-05           | -                        |
| mediatek_mt7986a-rfb       | -                        |
| mediatek_mt7986b-rfb       | -                        |
| mediatek_mt7988a-rfb       | -                        |
| netcore_n60                | -                        |
| netcore_n60-pro            | -                        |
| nokia_ea0326gmp            | -                        |
| openembed_som7981          | -                        |
| qihoo_360t7                | -                        |
| ruijie_rg-x60-pro          | -                        |
| tenbay_wr3000k             | -                        |
| tplink_tl-xdr4288          | -                        |
| tplink_tl-xdr6086          | -                        |
| tplink_tl-xdr6088          | -                        |
| tplink_tl-xtr8488          | -                        |
| xiaomi_redmi-router-ax6000 | -                        |

### 机型适配说明
- **23.05**：
  - `cmcc_rax3000m-usboffload` 和 `cmcc_rax3000m-emmc-usboffload` 会自动切换到 24.10 源码。
  - 部分机型（如 `cudy_tr3000-v1`）会自动切换到 Lede 源码。
- **24.10**：
  - 部分机型会自动转换，例如 `cmcc_rax3000m-nand` 转换为 `cmcc_rax3000m`。
  - 部分机型（如 `cudy_tr3000-v1`）会自动切换到 Lede 源码。
- **Lede**：
  - 部分机型会自动转换，例如 `cmcc_rax3000m` 转换为 `cmcc_rax3000m-nand`。

## 注意事项

- **编译时间**：视机型和版本不同，编译可能需要 1-2 小时，请耐心等待。
- **磁盘空间**：GitHub Actions 提供约 14GB 磁盘空间，建议定期清理旧的 Releases。
- **变砖风险**：刷机有风险，请谨慎操作。作者不对变砖负责，但欢迎反馈问题。
- **自定义配置**：
  - 自定义 Feeds 和配置需修改 `scripts/diy-part1.sh` 和 `scripts/diy-part2.sh`。
  - 配置文件（如 `2305.config`、`2410.config`、`Lede.config`）需放置在仓库根目录。

## 致谢

- 感谢 [padavanonly](https://github.com/padavanonly) 提供的 ImmortalWrt 分支。
- 感谢 [coolsnowwolf](https://github.com/coolsnowwolf) 提供的 Lede 分支。
- 感谢所有 OpenWrt 社区的贡献者！

## 问题反馈

如果遇到问题，请在 [Issues](https://github.com/<您的用户名>/<仓库名>/issues) 中提交，附上以下信息：
- 选择的版本和机型
- GitHub Actions 的日志（可从 Actions 页面下载）
- 问题的详细描述

---

**刷机有风险，操作需谨慎！如果变砖了，点个 Star 安慰一下吧！** 😄

---
