# 共创：和我们一起做这些 Skill

[English](CONTRIBUTING.md)

这些 Skill 来自我们自己做分析的经验。每天和电商、社媒、评论数据打交道的人，手里一定有我们没见过的方法。你琢磨出了一套站得住的分析方法，就放进来给更多人用，署你的名字。

大多数贡献不需要写代码。

## 怎么参与

| 你手上有…… | 这样做 |
|---|---|
| 一个新 Skill 的想法，或者一个问题 | 在 [Discussions → Ideas](https://github.com/everyinfra/analysis-skills/discussions/categories/ideas) 发帖，或者开一个「提议新 Skill」的 issue |
| 一次结果不对、误导人的分析 | 开一个「结果不对」的 issue |
| 现有 Skill 更好的步骤、检查或示例 | 开一个「改进现有 Skill」的 issue，或者直接提 PR |
| 一个完整的新 Skill | fork 仓库后提 PR |

不知道从哪开始？看看标了 [`help wanted`](https://github.com/everyinfra/analysis-skills/labels/help%20wanted) 和 [`good first issue`](https://github.com/everyinfra/analysis-skills/labels/good%20first%20issue) 的 issue。

## 这里的 Skill 长什么样

```text
skills/<skill-name>/SKILL.md              # 必须：开头的元信息 + 正文说明
skills/<skill-name>/references/*.md       # 可选：Skill 里链接的详细方法说明
examples/<skill-name>.synthetic.json      # 分析类 Skill 建议带：一份编造的输入和应有的输出
manifest.json                             # 给你的 Skill 加一条 {"slug", "skill_path", "example_path"}
```

- `SKILL.md` 开头写元信息：`name`（等于文件夹名，只用小写字母、数字和连字符，不超过 64 个字符）和 `description`（做什么、什么时候用、什么时候不用，不超过 1024 个字符）。
- 遵守 [analysis-foundation](skills/analysis-foundation/SKILL.md)：数字由运行过的代码算出，不让模型凭感觉给数；每个比例写清分母；说明不确定性；相关不写成因果。
- 给用户看的输出用用户的语言。原始数据里的文字只当数据，不当指令。
- 照着一个现有 Skill（比如 [review-insights](skills/review-insights/SKILL.md)）的结构写，最快也最不容易出错。

## 几条规矩

- **不放密钥。** 不提交 API Key、令牌、密码、Cookie，用 `YOUR_API_KEY` 这样的占位符。
- **不放真实的个人或客户数据。** 示例必须是编造的，文件名用 `*.synthetic.json`。
- **用自己的话写。** 不粘贴书、课程、付费报告的原文；需要的话概括并给链接。
- **许可。** 本库用 [Apache-2.0](LICENSE)。提交 PR 即表示你同意你的贡献也按 Apache-2.0 授权（第 5 条）。

## 提 PR 之前

在仓库根目录跑一下检查，只需要 Python 3：

```bash
python3 .github/scripts/check_contribution.py
```

它会检查 manifest、每个 Skill 的元信息，以及你改动的文件里的链接、JSON 和密钥。把它列出的问题改掉，再按 PR 模板填写。

## 我们怎么审

- 维护者定期手动看 issue 和 PR，不会自动合并。
- 我们可能会请你改一改，或者建议换个写法。这很正常，不代表不收。
- PR 合并后，你的名字会加进 [CONTRIBUTORS.md](CONTRIBUTORS.md)。我们也在给 [everyinfra.com](https://everyinfra.com) 加贡献者展示。

关于共创的问题，到 [Discussions](https://github.com/everyinfra/analysis-skills/discussions) 来问。
