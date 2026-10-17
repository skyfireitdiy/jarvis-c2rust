# Jarvis C2Rust

Jarvis C2Rust（`jarvis-c2rust` / `jc2r`）是 Jarvis 的 C/C++ → Rust 迁移套件，提供完整的自动化迁移流水线：扫描（scan）→ 库替代（lib-replace）→ 模块规划（prepare）→ 转译（transpile）→ 优化（optimize），支持渐进式迁移与断点续跑。

> **注意**：本工具是 Jarvis 的独立组件，以 `jarvis-ai-assistant` 为运行时依赖。安装后即可独立使用，无需安装完整 Jarvis 主包。

## 安装

```bash
pip install jarvis-c2rust
```

依赖要求：Python 3.12，运行时依赖 `jarvis-ai-assistant>=7.0.1`（提供 Agent、CodeAgent、配置与输出等基础能力）。

## 使用

```bash
# 查看帮助
jc2r --help
jarvis-c2rust --help

# 配置管理（根符号列表、禁用库列表、附加说明等）
jc2r config

# 执行完整转译流水线（scan -> lib-replace -> prepare -> transpile -> optimize），支持断点续跑
jc2r run

# 验证功能对齐
jc2r verify
```

或模块方式：

```bash
python -m jarvis.jarvis_c2rust.cli <subcommand>
```

## 核心数据

所有路径均推荐使用 `<project_root>/.jarvis/c2rust` 下的标准文件名，便于断点续跑与复用：

- 统一符号表（JSONL）：`<project_root>/.jarvis/c2rust/symbols.jsonl`（后续流程的主输入）
- 原始符号表（JSONL）：`<project_root>/.jarvis/c2rust/symbols_raw.jsonl`
- 其他产物：`translation_order.jsonl`、`library_replacements.jsonl`、`progress.json`、`config.json`、`symbol_map.jsonl` 等

## 开发

```bash
pip install -e ".[dev]"
pytest
```

## 许可证

MIT
