# 💻 驱动备份包 for R9000P2023

这是一个适用于 `[R9000P2023]` 的驱动备份包，来源于系统正常运行时导出的驱动，（该驱动是个人格式化电脑后，自行在微软官网下载ISO镜像系统，并重装微软WINDOWS11的驱动，所有驱动来自联想或Windows自动更新）
## 注意：非联想官方原装驱动
## 注意：非联想官方原装驱动
## 注意：非联想官方原装驱动
适用于：
- 重装 Windows 时出现找不到网络、触摸板、声音等设备的问题
- 使用 PE 系统安装 Windows 时需要预先加载驱动的场景

压缩包大小约为 **175MB**，包含大多数关键驱动（网卡、显卡、音频、I/O、热键功能等）。

---

## 📥 下载地址（Releases）

👉 [点击此处下载驱动压缩包](https://github.com/BXWX/Lenovo-AMD-Drivers-R9000P_2023/releases)

下载后请解压到U盘或PE系统可读目录。

---

## 🧰 使用方法一：用 DISM 手动导入驱动（适用于 WinPE 环境）

1. 进入 WinPE 系统
2. 将 `drivers` 文件夹放到如 `D:\drivers` 目录下（解压好的）
3. 打开命令提示符（管理员）窗口
4. 找到你要安装的系统所在的 Windows 分区（假设为 `C:`，如果是映像，可挂载后使用路径）
5. 运行以下命令导入所有驱动：

```cmd
dism /Image:C:\ /Add-Driver /Driver:D:\drivers /Recurse
```
C:\ 是目标系统的路径，D:\drivers 是驱动所在路径
如果你还没安装系统，可先挂载 install.wim 进行驱动注入（进阶见下）

---

## 🧰 使用方法二：在安装 Windows 时加载驱动（推荐给不会用命令行的用户）

用 U 盘制作好 Win11 安装盘（或用 WePE 自带安装器）

把解压好的 drivers 文件夹放到另一个 U 盘中（或同一个多分区U盘）

在安装 Windows 时，出现「请选择驱动器（硬盘）的位置」页面时：

如果你发现硬盘列表是空的，就需要加载驱动

点击左下角「加载驱动程序（Load Driver）」

浏览到你 U 盘上的 drivers 目录，选择其中一个 .inf 文件或整个文件夹

系统会自动识别驱动，点击「下一步」，继续安装系统

---

## 🎯 常见用途和适用人群

无网卡 → 无法联网安装驱动助手

键盘/触摸板/热键无响应 → 导入 IO/ACPI 驱动解决

显卡未识别 → 黑屏或低分辨率

安装时看不到硬盘 → 缺 NVMe/RAID 驱动

---

## 📌 注意事项
本驱动来源于实际运行系统 C:\Windows\System32\DriverStore，经过筛选、压缩

并非万能驱动，仅适用于特定机型（请勿在其他电脑上尝试）

如果使用 DISM 失败，请确认路径是否正确，或以管理员身份运行

---

## 🛠️ 高级用法（对 .wim 文件打驱动包）
如果你想提前把驱动注入到官方 Windows 镜像中（安装时自动生效）：
```
mkdir C:\mount
dism /Mount-Wim /WimFile:D:\sources\install.wim /Index:1 /MountDir:C:\mount
dism /Image:C:\mount /Add-Driver /Driver:D:\drivers /Recurse
dism /Unmount-Wim /MountDir:C:\mount /Commit
```
---

## 💬 联系方式 / 问题反馈
如驱动缺失、无法使用等问题，欢迎提交 issue 或 PR。
