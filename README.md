# Auto-WOW

> 魔兽世界无限服自动建号 Agent Skill：不可修改项与姓名由用户指定，可改项默认/随机，真实桌面 `main` 操作、禁止豆包/pip 虚拟桌面，逐帧视觉状态机 + 备选名容错重试。

## 优先下载（夸克网盘）

**推荐从网盘下载完整技能包**，国内速度更稳，解压后即可使用：

- 链接：https://pan.quark.cn/s/e31630eb502f
- 分享码：`/~e32e3cPSSn~:/`
- 用法：点击链接或复制整段内容，打开「夸克网盘 APP」即可获取。

GitHub Release 里的附件仅作备用；两个渠道内容一致。

## 这个技能做什么

`Auto-WOW` 是一个给 Agent 加载的技能定义（不是独立程序），在用户真实桌面上用鼠标键盘完成《魔兽世界：无限服》的角色创建闭环：

规则集 → 阵营 → 种族 → 职业 → 外观/体型 → 姓名 → 提交，遇到「阵营人口不平衡」弹窗自动后退重来，名称不可用则依次尝试备选名。

## 决策分层

| 类别 | 项目 | 谁来决定 |
|------|------|----------|
| 创建后不可修改 | 规则集、阵营、种族、职业、天裔分支 | **必须用户指定**，技能会列全选项校验 |
| 实际锁定 | 姓名（主名 + 副名 + 1–2 备选名） | **必须用户提供**，无限服没有改名服务 |
| 创建后可修改 | 体型（性别）、外观、HD/SD 模型 | Agent 默认或随机，用户可覆盖 |

如果用户第一句话已明确给出全部不可修改项和姓名，走快速路径：只做合法性校验和复述确认，不再逐层询问。

## 安装与触发

把技能包解压到 Agent 的技能目录，例如：

```
C:\Users\Administrator\.codebuddy\skills\Auto-WOW\
    SKILL.md
    references\flow-states.md
```

刷新后说「魔兽世界建号」「无限服建号」「魔兽自动创建角色」即可触发。

> 运行环境要求：Agent 需具备 `computer_use_tool`（`plane="cu"`）与 `seed_computer_use` 能力。本仓库不含独立脚本，也不会自行启动游戏客户端。

## 执行约定（提高成功率、防止卡死）

- 启动前先截屏确认处于真实桌面 `main`、游戏客户端可操作；**不切豆包/pip 虚拟桌面**，只点游戏窗口，不点右上角关闭按钮。
- 每步执行「点前截屏 → 动作 → 点后校验」三段式；同一动作最多重试 3 次。
- 等待按界面状态判断：重连/规则页超 10 秒、回退超 40 秒无变化即停；连续 60 秒无推进主动报告；单次建号总时限 15 分钟。
- 不平衡弹窗：确定 → 后退两次 → 第三次后退下移一点点击 → 等 20 秒 → 回登录页重来；只要每轮有推进就继续，连续 5 轮无进展停下报告。

各界面识别特征、坐标坑与异常处理见 [references/flow-states.md](references/flow-states.md)。

## 其他

- GitHub Release（备用下载）：https://github.com/FEFKNCQ/Auto-WOW/releases/latest
- 流程思路源自 [`DKCMJD51/moshou`](https://github.com/DKCMJD51/moshou)；角色选项信息参考 [Tabbit 分享会话](https://web.tabbit.com/share/chat/tLvz7YAXwMht) 与 [EndgameTools](https://endgametools.com/zh-CN/wow-forever/news/wow-forever-race-class-combinations)。
- 原仓库未提供 LICENSE；本项目仅供个人学习与桌面自动化研究，使用时请遵守所涉游戏服务条款。
