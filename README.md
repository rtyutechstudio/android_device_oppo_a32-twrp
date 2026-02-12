# android_device_oppo_a32-twrp
TWRP device tree for OPPO A32 (PDVM00)
TWRP Device Tree for OPPO PDVM00
适用于 OPPO PDVM00 的 TWRP 设备树，支持 FBE 解密与完整 Recovery 功能
✨ 特色亮点

• 原生 FBE 解密支持
已完整配置 TW_INCLUDE_FBE 与 BOARD_USES_QCOM_FBE_DECRYPTION，可直接解密 Android 11+ 文件级加密 /data 分区，无需格式化数据。

• 精准分区大小适配
内置 BOARD_RECOVERYIMAGE_PARTITION_SIZE := 100663296（96MB），编译后自动填充至分区大小，刷入无红字报错。

• 完整内核命令行配置
预置 BOARD_KERNEL_CMDLINE，适配骁龙平台串口与 Android Boot 协议，确保 TWRP 稳定引导与硬件交互。

• 文件系统兼容性
支持 ext4、F2FS 等主流文件系统，可直接挂载 /vendor、/product 分区，满足刷机与数据管理需求。
📱 设备信息

• 设备名称：OPPO PDVM00

• 平台：Qualcomm Snapdragon

• Android 版本：基于 Android 11+

• 加密方式：FBE (File-Based Encryption)
🚀 快速开始

1. 初始化 TWRP 源码
repo init -u https://github.com/minimal-manifest-twrp/platform_manifest.git -b twrp-11
repo sync
2. 克隆设备树
git clone https://github.com/[你的用户名]/device_oppo_PDVM00.git device/oppo/PDVM00
3. 编译 TWRP
source build/envsetup.sh
lunch twrp_PDVM00-eng
mka recoveryimage
编译完成后，镜像位于：out/target/product/PDVM00/recovery.img
🛠️ 关键配置说明

FBE 解密核心配置
# FBE
TW_INCLUDE_CRYPTO := true
TW_INCLUDE_FBE := true
BOARD_USES_METADATA_PARTITION := true
BOARD_USES_QCOM_FBE_DECRYPTION := true
TW_USE_FSCRYPT_POLICY := 1
分区与文件系统
BOARD_RECOVERYIMAGE_PARTITION_SIZE := 100663296
BOARD_VENDORIMAGE_FILE_SYSTEM_TYPE := ext4
BOARD_PRODUCTIMAGE_FILE_SYSTEM_TYPE := ext4
TARGET_USERIMAGES_USE_EXT4 := true
TARGET_USERIMAGES_USE_F2FS := true
⚠️ 注意事项

1. Blobs 依赖：为确保 FBE 解密正常，需从官方固件提取 keystore.qcom.so 等加密库，并放入 recovery/root/vendor/lib/hw 与 recovery/root/vendor/lib64/hw。

2. 内核要求：内核需开启 CONFIG_FS_ENCRYPTION、CONFIG_FS_ENCRYPTION_INLINE_CRYPT 等选项，否则无法解密。

3. 数据安全：首次使用前建议备份数据，避免意外格式化。
📄 许可证
本项目基于 Apache-2.0 许可证开源，详见 LICENSE 文件。
🤝 贡献
欢迎提交 Issue 与 Pull Request，共同完善设备树适配。
