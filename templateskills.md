---
name: make-skill-template
description: "GitHub Copilot 用の新しい Agent Skill を作成するときに使う。ユーザーが skill 作成、skill 追加、skill scaffold、定型作業の Skill 化を依頼した場合に、.github/skills/<skill-name>/SKILL.md を作る。"
---

# Make Skill Template

## 目的

新しい Agent Skill を最小構成で作る。

## 不足情報があれば質問する

- Skill 名
- 何を定型化するか
- どんな依頼や場面で使うか
- 出力先。指定がなければ `.github/skills/<skill-name>/SKILL.md`
- 必ず守る手順、参照ファイル、確認コマンド

## 作成ルール

- フォルダ名と `name` は一致させる。
- `name` は小文字、数字、ハイフンのみ。
- `description` には「何をするか」と「いつ使うか」を書く。
- 本文は短くし、実際に守る手順だけを書く。
- `scripts/`, `references/`, `assets/`, `templates/` は必要な場合だけ作る。

## 最小テンプレート

```md
---
name: <skill-name>
description: "<何をするか>。<いつ使うか> のときに使う。"
---

# <Skill Title>

## 目的

<この skill の目的>

## 手順

1. <最初にやること>
2. <実装または生成すること>
3. <確認すること>
```
