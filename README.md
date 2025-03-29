

---

# MT798X 固件炼丹炉：一键成砖大师

🎉 **欢迎体验 MT798X 固件炼丹炉！** 🎉  
这是一个基于 GitHub Actions 的自动化固件编译工具，支持 MT798X 平台的 OpenWrt 固件编译，覆盖 OpenWrt 23.05、24.10 和 Lede 版本，适配多种机型。无论是新手还是老手，都能一键生成专属固件！

## 项目简介

本项目通过 GitHub Actions 自动化编译 MT798X 平台的 OpenWrt 固件，支持以下版本：
- **OpenWrt 23.05**（基于 [padavanonly/immortalwrt-mt798x-23.05](https://github.com/padavanonly/immortalwrt-mt798x-23.05)）
- **OpenWrt 24.10**（基于 [padavanonly/immortalwrt-mt798x-24.10](https://github.com/padavanonly/immortalwrt-mt798x-24.10)）
- **Lede**（基于 [coolsnowwolf/lede](https://github.com/coolsnowwolf/lede)）

编译完成后，固件会发布到 GitHub Releases（仅包含 `sysupgrade.bin` 和 `factory.bin`），并可选上传到私有 WebDAV（包含所有 `.zip` 文件）。

## 功能特点

- **一键编译**：通过 GitHub Actions 自动化编译，无需本地环境。
- **多版本支持**：支持 OpenWrt 23.05、24.10 和 Lede 版本。
- **机型适配**：支持多种 MT798X 机型，自动适配源码和机型转换。
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
2. 选择 `MT798X固件炼丹炉：一键成砖大师` 工作流。
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
- **默认用户名**：`root`
- **默认密码**：
  - Lede 版本：`password`
  - 23.05 和 24.10 版本：无密码
- **刷机前**：请备份原固件，以防变砖。
- **刷机后**：如果路由器变砖，请尝试恢复，或在 Issues 中反馈（附上日志）。

## OpenWrt 23.05、24.10 与 Lede 支持的机型及配置对比

| **属性**           | **OpenWrt 23.05**                                      | **OpenWrt 24.10**                                      | **Lede**                                               |
|--------------------|-------------------------------------------------------|-------------------------------------------------------|-------------------------------------------------------|
| **管理地址**       | 192.168.2.1                                           | 192.168.2.1                                           | 192.168.2.1                                           |
| **默认用户名**     | root                                                  | root                                                  | root                                                  |
| **默认密码**       | 留空（无密码）                                        | 留空（无密码）                                        | password                                              |
| **固件来源**       | 基于 padavanonly 的 OpenWrt 23.05 源码编译            | 基于 padavanonly 的 OpenWrt 24.10 源码编译            | 基于 coolsnowwolf 的 Lede 源码编译                    |
| **内核版本**       | 5.4.255                                               | 5.4.284                                               | 6.x（具体版本可能随 Lede 更新而变化）                |
| **支持机型数量**   | 17                                                    | 20                                                    | 41                                                    |
| **支持的机型**     | 1. abt_asr3000<br>2. cetron_ct3003<br>3. cmcc_a10<br>4. cmcc_rax3000m-emmc<br>5. cmcc_rax3000m<br>6. h3c_nx30pro<br>7. imou_lc-hx3001<br>8. jcg_q30<br>9. konka_komi-a31<br>10. livinet_zr-3020<br>11. mt7981-360-t7-108M<br>12. mt7981-clt-r30b1<br>13. mt7981-clt-r30b1-112M<br>14. xiaomi_mi-router-ax3000t<br>15. xiaomi_mi-router-ax3000t-stock<br>16. xiaomi_mi-router-wr30u-112m<br>17. xiaomi_mi-router-wr30u-stock | 1. huasifei_wh3000-emmc（新增）<br>2. abt_asr3000<br>3. cetron_ct3003<br>4. cmcc_a10<br>5. cmcc_rax3000m-emmc<br>6. cmcc_rax3000m<br>7. cmcc_rax3000m-emmc-usboffload（新增）<br>8. cmcc_rax3000m-usboffload（新增）<br>9. h3c_nx30pro<br>10. imou_lc-hx3001<br>11. jcg_q30<br>12. konka_komi-a31<br>13. livinet_zr-3020<br>14. mt7981-360-t7-108M<br>15. mt7981-clt-r30b1<br>16. mt7981-clt-r30b1-112M<br>17. xiaomi_mi-router-ax3000t<br>18. xiaomi_mi-router-ax3000t-stock<br>19. xiaomi_mi-router-wr30u-112m<br>20. xiaomi_mi-router-wr30u-stock | 1. abt_asr3000<br>2. asus_tuf-ax4200（新增）<br>3. asus_tuf-ax6000（新增）<br>4. bananapi_bpi-r3（新增）<br>5. bananapi_bpi-r3-mini-emmc（新增）<br>6. bananapi_bpi-r3-mini-nand（新增）<br>7. bananapi_bpi-r4（新增）<br>8. bananapi_bpi-r4-poe（新增）<br>9. cetron_ct3003<br>10. cetron_ct3003-mod（新增）<br>11. cmcc_a10<br>12. cmcc_a10-mod（新增）<br>13. cmcc_rax3000m-emmc<br>14. cmcc_rax3000m-nand（新增）<br>15. cmcc_xr30-nand（新增）<br>16. cudy_tr3000-mod（新增）<br>17. cudy_tr3000-v1（新增）<br>18. fzs_5gcpe-p3（新增）<br>19. glinet_gl-mt2500（新增）<br>20. glinet_gl-mt3000（新增）<br>21. glinet_gl-mt6000（新增）<br>22. glinet_gl-x3000（新增）<br>23. glinet_gl-xe3000（新增）<br>24. h3c_magic-nx30-pro（新增）<br>25. huasifei_wh3000-emmc<br>26. hf_m7986r1-emmc（新增）<br>27. hf_m7986r1-nand（新增）<br>28. imou_lc-hx3001<br>29. jcg_q30-pro（新增）<br>30. jdcloud_re-cs-05（新增）<br>31. konka_komi-a31<br>32. livinet_zr-3020<br>33. mediatek_mt7986a-rfb（新增）<br>34. mediatek_mt7986b-rfb（新增）<br>35. mediatek_mt7988a-rfb（新增）<br>36. netcore_n60（新增）<br>37. netcore_n60-pro（新增）<br>38. nokia_ea0326gmp（新增）<br>39. openembed_som7981（新增）<br>40. qihoo_360t7（新增）<br>41. ruijie_rg-x60-pro（新增）<br>（更多机型请查看工作流配置文件） |
| **独有机型**       | 无                                                    | 1. cmcc_rax3000m-emmc-usboffload<br>2. cmcc_rax3000m-usboffload | 1. asus_tuf-ax4200<br>2. asus_tuf-ax6000<br>3. bananapi_bpi-r3<br>4. bananapi_bpi-r3-mini-emmc<br>5. bananapi_bpi-r3-mini-nand<br>6. bananapi_bpi-r4<br>7. bananapi_bpi-r4-poe<br>8. cetron_ct3003-mod<br>9. cmcc_a10-mod<br>10. cmcc_rax3000m-nand<br>11. cmcc_xr30-nand<br>12. cudy_tr3000-mod<br>13. cudy_tr3000-v1<br>14. fzs_5gcpe-p3<br>15. glinet_gl-mt2500<br>16. glinet_gl-mt3000<br>17. glinet_gl-mt6000<br>18. glinet_gl-x3000<br>19. glinet_gl-xe3000<br>20. h3c_magic-nx30-pro<br>21. hf_m7986r1-emmc<br>22. hf_m7986r1-nand<br>23. jcg_q30-pro<br>24. jdcloud_re-cs-05<br>25. mediatek_mt7986a-rfb<br>26. mediatek_mt7986b-rfb<br>27. mediatek_mt7988a-rfb<br>28. netcore_n60<br>29. netcore_n60-pro<br>30. nokia_ea0326gmp<br>31. openembed_som7981<br>32. qihoo_360t7<br>33. ruijie_rg-x60-pro<br>（更多机型请查看工作流配置文件） |

---

### 详细说明

#### OpenWrt 23.05
- **概述**：基于 padavanonly 的 OpenWrt 23.05 源码编译，内核版本为 5.4.255，支持 17 款 MT798X 平台的机型。
- **特点**：提供稳定的固件支持，适用于多种常见路由器型号，未包含 `usboffload` 功能的机型。
- **使用方式**：通过管理地址 `192.168.2.1` 访问，默认用户名为 `root`，密码留空。

#### OpenWrt 24.10
- **概述**：基于 padavanonly 的 OpenWrt 24.10 源码编译，内核版本升级至 5.4.284，支持 20 款 MT798X 平台的机型。
- **特点**：在 23.05 的基础上新增了 3 款机型（`huasifei_wh3000-emmc`、`cmcc_rax3000m-emmc-usboffload`、`cmcc_rax3000m-usboffload`），提供更广泛的设备支持和可能的性能优化。
- **使用方式**：同样通过管理地址 `192.168.2.1` 访问，默认用户名为 `root`，密码留空。

#### Lede
- **概述**：基于 coolsnowwolf 的 Lede 源码编译，内核版本为 6.x（具体版本可能随 Lede 更新而变化），支持 41 款 MT798X 平台的机型。
- **特点**：支持最广泛的机型，包含许多 23.05 和 24.10 不支持的设备，适合追求最新特性和更多机型支持的用户。
- **使用方式**：通过管理地址 `192.168.2.1` 访问，默认用户名为 `root`，默认密码为 `password`。

---

### 版本对比
- **内核升级**：
  - 从 23.05 的 5.4.255 升级到 24.10 的 5.4.284，可能带来 bug 修复和性能改进。
  - Lede 使用更新的 6.x 内核，支持更多新功能，但可能稳定性略低于 5.4 系列。
- **机型扩展**：
  - 24.10 比 23.05 多支持 3 款机型，尤其是增加了带 `usboffload` 功能的型号。
  - Lede 支持 41 款机型，远超 23.05 和 24.10，覆盖更多实验性设备。
- **默认密码**：
  - 23.05 和 24.10 无密码，Lede 默认密码为 `password`，需注意登录差异。
- **一致性**：
  - 三个版本的管理地址和默认用户名保持一致（`192.168.2.1` 和 `root`），便于用户迁移。

## 机型适配说明

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
