# Shadowsocks 一键安装脚本 - Debian 12/13 兼容性优化版

## 优化内容

### 1. 系统检测增强
- **原问题**: 原脚本仅依赖 `/etc/issue` 检测系统版本，在 Debian 12/13 中可能失效
- **优化方案**:
  - 优先使用 `/etc/os-release` 文件进行系统检测
  - 添加多层级版本检测机制
  - 支持 Debian 7-13 全版本检测

### 2. Python 环境适配
- **原问题**: 脚本硬编码使用 Python 2，但 Debian 12+ 默认只有 Python 3
- **优化方案**:
  - 自动检测 Python 3 和 Python 2 可用性
  - 动态选择合适的 Python 包和依赖
  - 优先使用 Python 3，兼容 Python 2

### 3. 依赖包安装优化
- **原问题**: 依赖包名在新版本中可能变更，安装失败时缺乏重试机制
- **优化方案**:
  - 增强错误检测和处理机制
  - Python 相关包自动尝试替代方案
  - 改进包索引更新流程

### 4. 版本兼容性检查
- **原问题**: 版本检测函数无法正确解析现代 Debian 版本信息
- **优化方案**:
  - 重写 `debianversion()` 函数支持新版本格式
  - 增加版本兼容性警告和提示
  - 扩展支持 Debian 12 和 13

### 5. 用户体验改进
- **新增功能**:
  - 安装前显示系统信息和兼容性状态
  - 增强错误提示和解决方案
  - 添加详细的版本支持说明

## 主要改动文件

### 核心函数优化
- `check_sys()` - 增强系统检测逻辑
- `getversion()` - 支持 `/etc/os-release` 版本解析
- `debianversion()` - 现代 Debian 版本检测
- `install_dependencies()` - 智能 Python 包选择
- `error_detect_depends()` - 错误处理和重试机制
- `install_check()` - 版本兼容性验证

## 测试结果

✅ **语法检查**: 通过 `bash -n` 语法验证
✅ **Debian 12**: 系统检测正常，Python 3 适配成功
✅ **依赖检测**: 所有关键依赖包检测正常
✅ **版本识别**: 正确识别 Debian 12.x 版本

## 使用方法

```bash
# 下载优化版脚本
wget --no-check-certificate -O shadowsocks-all.sh https://raw.githubusercontent.com/Fmmx/shadowsocks-libev-enhance/master/shadowsocks-libev-enhance.sh

# 设置执行权限
chmod +x shadowsocks-libev-enhance.sh

# 运行安装
./shadowsocks-libev-enhance.sh
```

## 兼容性支持

| 系统版本 | 支持状态 | 说明 |
|---------|---------|------|
| Debian 7-11 | ✅ 完全支持 | 保持原有兼容性 |
| Debian 12 | ✅ 新增支持 | 经过测试验证 |
| Debian 13 | ✅ 理论支持 | 基于 Debian 12 适配 |
| Ubuntu 12+ | ✅ 完全支持 | 保持原有兼容性 |
| CentOS 6+ | ✅ 完全支持 | 保持原有兼容性 |

## 注意事项

1. **Python 环境**: 脚本会自动选择最佳 Python 版本，无需手动配置
2. **依赖安装**: 如遇到包安装失败，脚本会自动尝试替代方案
3. **权限要求**: 需要 root 权限运行
4. **网络要求**: 需要能够访问 GitHub 和软件源

## 安全特性

- 保持原脚本的所有安全检查
- 增强了错误处理，避免部分安装失败
- 改进了权限和环境检测

这个优化版本解决了原脚本在 Debian 12/13 上的兼容性问题，同时保持了对旧版本系统的完全兼容。
