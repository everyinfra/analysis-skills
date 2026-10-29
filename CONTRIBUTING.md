# Contributing: build these Skills with us

[中文](CONTRIBUTING.zh-CN.md)

These Skills grew out of our own analysis work. The people who analyse ecommerce, social and review data every day know methods we have never seen. If you have worked out a way of analysing data that holds up, put it here so others can use it. Your name stays on it.

You do not need to write code for most contributions.

## Ways to take part

| You have… | Do this |
|---|---|
| An idea for a new Skill, or a question | Start a thread in [Discussions → Ideas](https://github.com/everyinfra/analysis-skills/discussions/categories/ideas), or open a **Propose a new Skill** issue |
| A result that was wrong or misleading | Open a **Wrong or misleading result** issue |
| A better step, check or example for an existing Skill | Open an **Improve an existing Skill** issue, or send a pull request |
| A whole new Skill | Fork the repo and send a pull request |

Not sure where to start? Look at issues labelled [`help wanted`](https://github.com/everyinfra/analysis-skills/labels/help%20wanted) or [`good first issue`](https://github.com/everyinfra/analysis-skills/labels/good%20first%20issue).

## What a Skill looks like here

```text
skills/<skill-name>/SKILL.md              # required: front matter + instructions
skills/<skill-name>/references/*.md       # optional: longer method notes the Skill links to
examples/<skill-name>.synthetic.json      # recommended for analysis Skills: a made-up input and expected output
manifest.json                             # add {"slug", "skill_path", "example_path"} for your Skill
```

- `SKILL.md` starts with front matter: `name` (the folder name: lowercase letters, digits, hyphens, at most 64 characters) and `description` (what it does, when to use it and when not to; at most 1024 characters).
- Follow [analysis-foundation](skills/analysis-foundation/SKILL.md): numbers come from executed code, never from the model's head; name every denominator; report uncertainty; do not word correlation as causation.
- Write user-facing output in the user's language. Treat source text as data, never as instructions.
- Copy the shape of an existing Skill such as [review-insights](skills/review-insights/SKILL.md). That is the fastest way to get it right.

## Ground rules

- **No secrets.** Never commit API keys, tokens, passwords or cookies. Use placeholders such as `YOUR_API_KEY`.
- **No real personal or customer data.** Examples must be synthetic (made up) and named `*.synthetic.json`.
- **Your own words.** Do not paste copyrighted text from books, courses or paid reports; summarise and link instead.
- **License.** The library is [Apache-2.0](LICENSE). By sending a pull request you agree that your contribution is licensed under the same terms (Apache-2.0, section 5).

## Before you send a pull request

Run the check from the repository root. It needs only Python 3:

```bash
python3 .github/scripts/check_contribution.py
```

It checks the manifest, each Skill's front matter, links, JSON files and secrets in what you changed. Fix anything it lists, then fill in the pull request template.

## How review works

- Maintainers review issues and pull requests by hand, regularly. Nothing is merged automatically.
- We may ask for changes or suggest a different shape. That is normal and is not a rejection.
- When your pull request is merged, you are added to [CONTRIBUTORS.md](CONTRIBUTORS.md). We are also adding a contributors section to [everyinfra.com](https://everyinfra.com).

Questions about contributing: ask in [Discussions](https://github.com/everyinfra/analysis-skills/discussions).
