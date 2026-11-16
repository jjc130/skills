# skills

个人 Agent Skills 汇总仓库。每个 skill 放在一个独立子目录下，目录内的 `SKILL.md` 是入口。

## 已收录

| Skill | 目录 | 说明 | 来源 |
| --- | --- | --- | --- |
| image-to-svg | [`image-to-svg/`](image-to-svg/) | 把 PNG / JPG / WebP / 截图等位图重建为干净、可编辑、透明背景的 SVG（图标、Logo、字形、字标、UI 图形），不包裹位图 | 上游 [zyipeng/image-to-svg](https://github.com/zyipeng/image-to-svg)，MIT License |
| cell_su7 | [`cell_su7/`](cell_su7/) | 把科研插图类图片还原为可编辑的 PPT 或 Illustrator 图形：只去掉图上的文字、保留原有图形，再把文字以可编辑文本回填 | 本机安装的 cell_su7 skill 全量 1:1 复制（45 个文件，逐文件 SHA256 校验一致）；依赖 [yrui-cmd/cell_no_ai](https://github.com/yrui-cmd/cell_no_ai) |

## 使用方式

把子目录放到你的 agent 的 skill 发现目录即可，例如：

```bash
git clone https://github.com/jjc130/skills.git
cp -r skills/image-to-svg ~/.claude/skills/     # 或 ~/.codex/skills/ 等
cp -r skills/cell_su7  ~/.claude/skills/
```

在会话里直接引用：

```text
Use $image-to-svg to turn this logo into a high-fidelity editable SVG with a transparent background.
Use $cell_su7 to keep my figure graphics intact, restore the labels as live text, and draw in PowerPoint.
```

## 目录结构

```text
skills/
├── image-to-svg/
│   ├── SKILL.md
│   ├── references/
│   ├── scripts/
│   ├── examples/
│   ├── agents/
│   ├── requirements.txt
│   └── package.json
└── cell_su7/
    ├── SKILL.md
    ├── references/          # text-workflow / backends / optional-no-ai / 各后端流程
    ├── scripts/             # 图像入口、文字回填、OOXML 与 Illustrator Runtime、额度与同步脚本
    ├── agents/
    │   └── openai.yaml
    └── runtime-profile.json # configure_runtime.py 生成的本机运行档案，换机器会自动重建
```

## 说明

- 各 skill 的许可证与署名见其自身目录内文件；`image-to-svg` 版权归原作者 zyipeng，本仓库仅做收录与分发。
- 核心流程不需要额外依赖；Pillow / NumPy / Playwright 为可选的增强质量检查组件。
- `cell_su7` 为 1:1 复制收录：`SKILL.md`、`references/`、`scripts/`、`agents/` 与本机安装版本逐字节一致（45 个文件，SHA256 全部匹配）。
- `cell_su7` 依赖同级的 `cell_no_ai` skill，首次使用前需运行 `python scripts/sync_cell_no_ai.py` 同步上游；仓库内不含任何 API Key 或 DPAPI 凭据，密钥需按 `SKILL.md` 的“Credential setup”在本机自行配置。
- `runtime-profile.json` 只保存非机密的本机能力探测结果（Office/Illustrator 是否注册、Python 版本、缓存参数），由 `configure_runtime.py` 重新生成，不覆盖代码内的默认值。
