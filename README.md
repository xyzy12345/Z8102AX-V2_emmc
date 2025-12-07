# Z8102AX-V2_emmc

OpenWrt build configuration for ZBT-Z8102AX eMMC version router.

## Overview

This repository contains custom configurations and device tree files for building OpenWrt firmware for the ZBT-Z8102AX router with eMMC storage.

## Build Status

The automated build uses GitHub Actions to compile OpenWrt 24.10.4 firmware.

## Directory Structure

```
.
├── custom-configs/
│   ├── configs/          # Device-specific configuration files
│   ├── dts/             # Device tree source files
│   └── target/          # Target-specific build files
└── .github/
    └── workflows/       # GitHub Actions workflow definitions
```

## Building Firmware

### Automated Build (GitHub Actions)

1. Go to the "Actions" tab in the GitHub repository
2. Select "Build OpenWrt 24.10.4 for ZBT-Z8102AX-eMMC"
3. Click "Run workflow"
4. Choose build options:
   - **清除构建缓存** (Clean build cache): Optional, use for clean builds
   - **跳过下载阶段** (Skip download stage): Optional, speeds up subsequent builds

The workflow will automatically:
- Clone OpenWrt source code (version 24.10.4)
- Apply custom device tree and configuration files
- Build the firmware
- Upload artifacts upon completion

### Build Configuration

- **Target**: mediatek
- **Subtarget**: filogic
- **Device**: zbtlink_z8102ax-emmc
- **OpenWrt Version**: 24.10.4

## Troubleshooting

### "Error opening terminal: unknown"

This error occurs when the build system tries to use interactive configuration tools (like `menuconfig`) in a non-interactive CI/CD environment.

**Solution**: The workflow has been fixed to use non-interactive configuration methods:
- Set `TERM=linux` environment variable
- Use `yes '' | make oldconfig` instead of `make defconfig` for config validation
- This allows the build to proceed without requiring terminal interaction

## Custom Files

### Device Tree (DTS)
Location: `custom-configs/dts/mt7981b-zbt-z8102ax-emmc.dts`

Contains hardware definitions for the ZBT-Z8102AX router with eMMC storage.

### Device Configuration
Location: `custom-configs/configs/zbtlink_z8102ax-emmc.config`

Contains OpenWrt configuration options specific to this device.

### Build Target
Location: `custom-configs/target/linux/mediatek/image/filogic.mk`

Defines the build target for the Filogic MediaTek platform.

## Contributing

When modifying build configurations:
1. Test changes locally if possible
2. Commit changes with clear descriptions
3. Run the GitHub Actions workflow to validate
4. Check build logs for any errors

## License

This repository contains configuration files for OpenWrt. OpenWrt is licensed under GPL-2.0.

## References

- [OpenWrt Official Website](https://openwrt.org/)
- [OpenWrt Build System Documentation](https://openwrt.org/docs/guide-developer/toolchain/use-buildsystem)
- [MediaTek Filogic Platform](https://openwrt.org/docs/techref/hardware/soc/soc.mediatek.filogic)