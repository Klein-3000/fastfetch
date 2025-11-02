# 🎨 FastFetch Dynamic Logo Theme Pack

✨ 为 [FastFetch](https://github.com/LinusBorg/fastfetch) 打造的**动态 Logo 主题包**，支持随机切换静态图、GIF、WebP 动画，适用于 Windows + WezTerm + PowerShell 环境。

> 🌟 每次打开终端，都有新鲜感！支持一键随机、指定显示、动态徽记渲染！

---

## 🌟 特性概览

- ✅ 支持多种图像格式：PNG、JPG、GIF、WebP（含动画）
- ✅ 提供多套风格化配置文件（ASCII、静态图、动图）
- ✅ 集成 PowerShell 脚本 `ff.ps1` 实现高级功能封装
- ✅ 兼容 WezTerm 透明背景与动画渲染（推荐）


## 🚀 快速启动脚本 `ff.ps1`

通过 PowerShell 脚本封装，实现一键调用、随机切换 Logo：
```powershell
ff                  # 随机显示一个 logo
ff -name teresa.gif # 显示指定 logo
ff -width 40        # 设置 logo 宽度
ff -list            # 查看所有可用 logo
ff -help            # 查看帮助
```
### 🔱 Sigil 徽记模式（特色功能）

> 使用 `logos/sigils/` 中的图标 + `SigilModule/` 中的配置，打造专属视觉风格

```powershell
ff -sigil 真我.png                     # 使用指定徽记，加载默认 border.jsonc 配置
ff -sigil 救世.png -sigil-jsonc simple.jsonc  # 指定徽记 + 自定义配置
ff -rand-sigils                      # 随机选择徽记图片 + 随机配置文件
ff -list-sigils                      # 查看所有可用的 sigil 徽记
ff -list-sigils-jsonc                # 查看所有可用的 sigil 配置文件 (.jsonc)
```
---

## 🖼️ 预览效果

| 配置                          | 效果描述                | 预览图                          |
| --------------------------- | ------------------- | ---------------------------- |
| `ascii.jsonc` + `ascii.txt` | 使用 ASCII 艺术字作为 Logo | ![ASCII](Display/ascii.png)  |
| `gif.jsonc` + `kiana.webp`  | WebP 动画 Logo（推荐动效）  | ![WebP](Display/config.webp) |
| `img.jsonc` + `augusta.png` | 静态图片 Logo（简洁稳定）     | ![Image](Display/img.png)    |

### 注意
- 💡 **终端支持**：GIF/WebP 动画效果需终端支持透明背景和动画渲染，推荐使用 [WezTerm](https://wezfurlong.org/wezterm/)。

-  ⚠️ **配置加载**: FastFetch 默认只读取 `config.jsonc`，其他配置需通过 `fastfetch -c ~/.config/fastfetch/xxx.jsonc` 指定。
- 加载ff.ps1脚本,执行**ff**命令可以随机获取上面预览效果

---

## ⚙️ 配置文件说明

| 文件             | 作用                               |
| -------------- | -------------------------------- |
| `config.jsonc` | 默认配置（webp 动画 Logo）               |
| `img.jsonc`    | 使用静态图片作为 Logo                    |
| `gif.jsonc`    | 使用动图（GIF/WebP）作为 Logo            |
| `ascii.jsonc`  | 使用文本文件 `ascii.txt` 渲染 ASCII Logo |

---

## 🐱‍💻 使用方法

### 1. 安装依赖
确保已安装：
- [fastfetch](https://github.com/LinusBorg/fastfetch)
- PowerShell 5.1+
- [WezTerm（推荐， 可以参考我的配置）](https://github.com/Klein-3000/wezterm)

### 2. 安装配置
```powershell
# 克隆仓库
git clone https://github.com/Klein-3000/fastfetch.git
# 复制到配置目录
Copy-Item -Recurse fastfetch-config\* -Destination "$env:USERPROFILE\.config\fastfetch"
```

✅ 确保路径为：`C:\Users\<你的用户名>\.config\fastfetch\`
### 3. 注册 ff.ps1 到环境变量（可选）

为了让 `ff` 命令全局可用，可将脚本目录加入 PowerShell 的 `$PROFILE`：

```powershell
# 编辑你的 PowerShell 配置文件
notepad $PROFILE

# 在文件末尾添加：
$env:PATH += ";$env:USERPROFILE\.config\fastfetch"
```

---
## 📂 文件目录结构
```powershell
~/.config/fastfetch/
├── ascii.jsonc           # ASCII 文本配置
├── config.jsonc          # 默认主配置（动图）
├── Display/              # 预览图存放
├── ff.ps1                # 主控制脚本
├── gif.jsonc             # 动图专用配置
├── img.jsonc             # 静态图配置
├── logos/                # 所有 Logo 图片
│   ├── *.png/.jpg/.webp  # 支持多种格式
│   └── sigils/           # Sigil 徽记专用子目录
├── README.md             # 本文件
└── SigilModule/          # Sigil 模式配置
    ├── border.jsonc      # 默认边框样式
    └── simple.jsonc      # 简洁样式
```

## 📦 Logo 资源

所有 Logo 存放于 `%USERPROFILE%\.config\fastfetch\logos\` 目录，支持格式：

- `.png`, `.jpg`, `.jpeg`
- `.gif`（动图）
- `.webp`（动图）

你可以自由添加新图片！运行 `ff -list` 可查看当前可用 Logo。

## 🛡️ Sigil 徽记系统详解

> 一种结合「专属图标 + 特殊布局」的高级展示模式

- **图标路径**：`logos/sigils/`（仅此目录内图片可用于 `-sigil`）
- **配置路径**：`SigilModule/`（`.jsonc` 文件控制边框、文字位置等）
- **默认配置**：`border.jsonc`
- **随机模式**：`ff -rand-sigils` 会从 `sigils/` 和 `SigilModule/` 中随机选取组合

> 🎨 你可以创建自己的 `.jsonc` 配置文件放入 `SigilModule/`，并通过 `-sigil-jsonc` 调用。

---


## 📄 版权与免责声明

本项目中部分图像素材来源于《崩坏3》等二次元游戏及相关创作，版权归原作者所有。

本仓库为**个人非商业性质的开源爱好者项目**，仅用于分享终端美化配置，不涉及任何盈利行为。  
若涉及版权问题，请联系作者（通过 Issue 或邮件），我们将及时删除相关内容。

📌 请遵守相关法律法规，勿将本项目用于商业用途或未经授权的分发

❤️ 如果你喜欢这个项目，欢迎点个 Star 支持！
