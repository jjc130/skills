# skills

个人 Agent Skills 汇总仓库。每个 skill 放在一个独立子目录下，目录内的 `SKILL.md` 是入口。

## 已收录

| Skill | 目录 | 说明 | 来源 |
| --- | --- | --- | --- |
| image-to-svg | [`image-to-svg/`](image-to-svg/) | 把 PNG / JPG / WebP / 截图等位图重建为干净、可编辑、透明背景的 SVG（图标、Logo、字形、字标、UI 图形），不包裹位图 | 上游 [zyipeng/image-to-svg](https://github.com/zyipeng/image-to-svg)，MIT License |

## 使用方式

把子目录放到你的 agent 的 skill 发现目录即可，例如：

```bash
git clone https://github.com/jjc130/skills.git
cp -r skills/image-to-svg ~/.claude/skills/     # 或 ~/.codex/skills/ 等
```

在会话里直接引用：

```text
Use $image-to-svg to turn this logo into a high-fidelity editable SVG with a transparent background.
```

## 目录结构

```text
skills/
└── image-to-svg/
    ├── SKILL.md
    ├── references/
    ├── scripts/
    ├── examples/
    ├── agents/
    ├── requirements.txt
    └── package.json
```

## 说明

- 各 skill 的许可证与署名见其自身目录内文件；`image-to-svg` 版权归原作者 zyipeng，本仓库仅做收录与分发。
- 核心流程不需要额外依赖；Pillow / NumPy / Playwright 为可选的增强质量检查组件。
