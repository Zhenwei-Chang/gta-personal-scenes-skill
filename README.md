# GTA Personal Scenes Skill

**用自己的照片，生成统一 GTA 游戏风格的个人生活图片。**

支持创建个人游戏人物与不同穿搭、生成新的生活场景、把已有场景主角换成自己，以及只修改书、服装、屏幕等局部内容。

默认效果是 **GTA San Andreas / 2004 PS2 低多边形实机截图感**：保留本人的脸和发型，人物与环境采用同一种旧游戏建模质感；每个场景独立输出 1:1，无画外标注。表情根据活动变化，换主角时沿用原场景的情绪与动作。

## 从这里开始

| 使用环境 | 使用文件 | 方式 |
| --- | --- | --- |
| 豆包工作 | [SKILL.md](skills/gta-personal-scenes/SKILL.md) 与同目录支持文件 | 本地导入或新建自定义技能 |
| 普通豆包图片创作 | [豆包独立指令](adapters/doubao-instructions.md) | 全文粘贴，再上传照片并写要求 |
| Codex 等支持 `SKILL.md` 的代理 | `skills/gta-personal-scenes/` | 放入宿主技能目录，再调用 |

Skill 负责组织身份参考、场景、服装、表情与出图工作流。实际图片由当前平台可用的图像工具生成；纯文本环境会交付提示词与参考图说明。

### 豆包工作

官方介绍确认支持自建技能、导入本地技能文件及图片生成编辑。[飞书官方说明](https://www.feishu.cn/content/article/7677519271848610746)

下载本仓库，在技能管理里按客户端支持格式导入 `skills/gta-personal-scenes/`，或使用 [Skill ZIP](dist/gta-personal-scenes.skill.zip)。如果导入器不接受标准 Skill 目录，就新建自定义技能：名称填“GTA 个人生活场景”，复制 `SKILL.md` 的描述和正文，再添加 `references/` 文档。不能读取支持文档时，使用完整的[豆包独立指令](adapters/doubao-instructions.md)。

官方未公布本地导入包的完整结构规范；此项目没有在你的豆包账号里完成安装与出图验证。详细兼容性及操作见 [豆包使用说明](skills/gta-personal-scenes/references/doubao.md)。

### 普通豆包

在支持图片创作的对话中粘贴[豆包独立指令](adapters/doubao-instructions.md)全文，上传自己的照片，然后发：

> 图 1 是我的本人照片。请先做我的 GTA San Andreas 风格游戏人物，休闲、篮球、夹克三套衣服，每套单独一张 1:1，不加标注。之后用这个人生成对应的假期生活场景，衣服和表情适配活动。

后续再发：

> 保持这个人物和画风，做我打篮球、吃涮肉、学英语、骑电动车的四个场景。每个单独一张，不要拼图，表情分别适配。

跨对话时重新上传认可的人物图，让新的对话也能参考同一身份。

### 支持 Skill 的本地代理

将整个 `skills/gta-personal-scenes/` 目录复制到宿主的技能目录。Codex 可放到 `~/.codex/skills/gta-personal-scenes/`；保留 `references/` 和 `agents/`。

调用示例：

> 使用 $gta-personal-scenes，根据我上传的照片生成个人游戏人物，再做篮球和夜间便利店两个场景。

## 换主角：传图顺序

建议按 **原场景 → 认可的人物 → 本人照片 → 可选服装或屏幕参考** 上传。输入：

> 图 1 是原场景，图 2 是我的游戏人物，图 3 是本人照片。把原主角完整换成我，保留场景构图、姿势、屏幕和道具，用我的五官表达原来惊讶的表情，保持全图旧游戏质感，1:1，无文字标注。

原场景控制构图与动作，人物基准控制身份；服装可以变化，表情不会被冻结成证件照状态。

## 文件结构

```text
skills/gta-personal-scenes/
  SKILL.md                         核心工作流
  agents/openai.yaml               Codex 界面信息
  references/
    identity-and-style.md          身份、服装与画风
    prompt-templates.md            四种模式的完整提示词
    scene-library.md               场景、表情与穿搭示例
    doubao.md                      豆包接入与兼容性
adapters/doubao-instructions.md    单文件中文指令
examples/requests.zh-CN.md         可复制的使用请求
dist/gta-personal-scenes.skill.zip 单独的 Skill 导入包
LICENSE                           MIT
```

更多例子见[请求示例](examples/requests.zh-CN.md)。本仓库不需要 API Key 或安装依赖；若要 API 自动化，支持文档提供火山方舟官方资料入口。

## 发布内容

仓库包含通用工作流和模板，不附带使用者真人照片或私人生成图片。自己使用的参考图可以存到被 Git 忽略的 `private/` 或 `photos/`，输出存到 `outputs/`；忽略规则不处理已被追踪的文件。

协议为 [MIT](LICENSE)，覆盖本仓库的指令和文档。GTA 名称用于描述视觉参考，本项目为独立创作。
