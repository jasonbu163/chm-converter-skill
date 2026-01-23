# CHM Converter

将 CHM 文件转换为 Markdown 格式，特别针对 Revit API 文档进行了优化。

## 项目来源

本项目基于 [DTDucas/chm-converter](https://github.com/DTDucas/chm-converter.git) 开发

## 功能特性

- 🔄 将 CHM 格式文件转换为 Markdown 格式
- 📚 特别优化用于 Revit API 文档转换
- 🎯 自动清理 HTML 元素和不必要的样式类
- 🔗 自动转换和更新 HTML 链接为 Markdown 格式
- 💾 支持自动编码检测（UTF-8、GB18030、GBK等）
- ⚡ 异步并发处理，提高转换效率
- 🛠️ 支持代码块识别和格式化
- 📝 自动提取页面标题和元数据

## 安装

### 环境要求

- Python 3.13+
- 7-Zip（用于提取 CHM 文件）

### 依赖包

```
aiofiles>=25.1.0
beautifulsoup4>=4.14.3
chardet>=5.2.0
html2text>=2025.4.15
py7zip>=0.6.2
```

### 快速开始

1. 克隆或下载此项目
2. 创建虚拟环境：
   ```bash
   python3 -m venv .venv
   source .venv/bin/activate  # macOS/Linux
   # 或
   .venv\Scripts\activate  # Windows
   ```

3. 安装依赖：
   ```bash
   pip install -r requirements.txt
   # 或使用 uv 包管理器
   uv pip install -r requirements.txt
   ```

4. 安装 7-Zip：
   - **macOS**: `brew install 7-zip`
   - **Linux**: `sudo apt install p7zip-full`
   - **Windows**: 从 [7-Zip 官网](https://www.7-zip.org/) 下载安装

## 使用方法

### 基本用法

```python
from scripts.chm_to_markdown import convert_html_to_markdown
import asyncio

# 转换 CHM 文件
async def convert_chm():
    # 你的转换代码
    pass

asyncio.run(convert_chm())
```

### 处理多个 CHM 文件

将 CHM 文件放在 `resources/` 文件夹中，脚本会自动检测并转换所有 CHM 文件。

支持的 CHM 文件：
- 2022.chm
- 2023.chm
- 2024.chm
- 2025.chm
- 2025.3.chm
- 2026.chm

## 项目结构

```
chm-converter-skill/
├── main.py                          # 主程序入口
├── pyproject.toml                   # 项目配置
├── README.md                        # 项目说明文档
├── resources/                       # CHM 文件存储目录
│   ├── 2022.chm
│   ├── 2023.chm
│   ├── 2024.chm
│   ├── 2025.chm
│   ├── 2025.3.chm
│   └── 2026.chm
└── scripts/
    └── chm_to_markdown.py           # CHM 转 Markdown 核心转换脚本
```

## 主要功能说明

### 编码检测
自动检测文件编码，支持多种字符集：
- UTF-8
- GB18030
- GBK
- GB2312

### HTML 清理
自动移除以下不必要的元素：
- 脚本标签、样式标签
- 导航和页眉页脚
- JavaScript 链接
- 邮件链接

### 链接转换
- 将 HTML 链接转换为 Markdown 格式
- 自动更新文件扩展名（`.htm` → `.md`）
- 保持链接的目标和标题信息

### 代码块处理
支持多种编程语言的代码块：
- C# (csharp)
- VB.NET (vb)
- C++ (cpp)
- F# (fsharp)
- XML/HTML
- JSON

### 表格处理
自动修复和格式化 Markdown 表格

## 许可证

本项目采用 **MIT License** 进行许可。

详见 [LICENSE](LICENSE) 文件。

### MIT 许可证说明

MIT License 允许你：
- ✅ 商业使用
- ✅ 修改代码
- ✅ 分发代码
- ✅ 个人使用

条件：
- 📋 包含许可证和版权声明

限制：
- ⚠️ 不提供担保
- ⚠️ 作者不承担责任

## 贡献

欢迎提交 Issue 和 Pull Request！

## 致谢

感谢 [Duong Tran Quang (DTDucas)](https://github.com/DTDucas) 创建了原始的 chm-converter 项目。

## 联系方式

如有问题或建议，欢迎提出 Issue。

---

**更新时间**: 2026年1月23日
