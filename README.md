# esp32-firmware（只放产物）

公网 OTA 用的人工产物仓库：设备从 GitHub Pages 直接拉取 `latest.json` 和 `xiaozhi.bin`，
不使用 Release 资产（Release 会 302 到 objects.githubusercontent.com，设备端 HTTP 客户端不跟随跳转）。

## 目录

| 路径 | 板子 |
|---|---|
| `4b/` | Waveshare ESP32-S3-Touch-LCD-4B |
| `s3-2.16/` | Waveshare ESP32-S3-Touch-AMOLED-2.16 |

每个目录两个文件：

```
latest.json    # {"firmware":{"version":"x.y.z","url":"https://<user>.github.io/esp32-firmware/<board>/xiaozhi.bin"}}
xiaozhi.bin    # 4 MB 左右的应用镜像
```

## 发布

不要手改这里，用对应固件工程里的脚本：

```bash
projects/4b/push.sh          # 版本号 +1 → 编译 → 更新 4b/ → git push
projects/s3-2.16/push.sh     # 同上，s3-2.16/
```

Pages 生效有 30～60 秒延迟；设备端「设置 → 检查更新」会按 `version` 判断是否需要下载。

## 注意

- 仓库必须是 **public**，否则设备（没有 token）下载不了。
- Pages 需要打开：Settings → Pages → Deploy from a branch → `main` / `(root)`。
- 这里只放编译产物，源码仓库继续私有。
