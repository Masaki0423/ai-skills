# ai-skills

Claude Code 用スキル集。プラグインマーケットプレイス形式で配布しています。

## 収録スキル

| スキル | 説明 |
|---|---|
| [`trending-ai-topics`](plugins/ai-community-tools/skills/trending-ai-topics/SKILL.md) | 実行時点で話題になっているAIトピックを収集し、読者層別（初学者/開発者/業界動向）に整形してSlackに投稿する |

スキル固有の使い方・引数・必要な環境変数は、各スキルの `SKILL.md` に記載しています。

## インストール

### Claude Code（推奨）

```
/plugin marketplace add Masaki0423/ai-skills
/plugin install ai-community-tools@ai-skills
```

更新があった場合はプラグインのアップデートで追従できます。

### 手動インストール

使いたいスキルのディレクトリを `~/.claude/skills/`（全プロジェクト共通）または
プロジェクトの `.claude/skills/` にコピーしてください。

```bash
git clone https://github.com/Masaki0423/ai-skills.git
cp -r ai-skills/plugins/ai-community-tools/skills/<skill-name> ~/.claude/skills/
```

### claude.ai（Web / デスクトップ）

スキルのディレクトリをzipにして「設定 → Capabilities → Skills」からアップロードできます。

```bash
cd plugins/ai-community-tools/skills && zip -r <skill-name>.zip <skill-name>/
```

## リポジトリ構成

```
ai-skills/
├── .claude-plugin/
│   └── marketplace.json          # マーケットプレイス定義（プラグイン一覧）
└── plugins/
    └── ai-community-tools/       # プラグイン（スキルの束）
        ├── .claude-plugin/
        │   └── plugin.json       # プラグイン名・バージョン
        └── skills/
            └── <skill-name>/
                └── SKILL.md      # スキル本体（1スキル=1ディレクトリ）
```

## スキルの追加方法

### 1. スキルディレクトリを作る

`plugins/ai-community-tools/skills/<skill-name>/SKILL.md` を作成する。
最低限必要なのはこのファイル1つ。補助スクリプトや参照ファイルは同じディレクトリに置ける。

```markdown
---
name: my-new-skill
description: >
  何をするスキルかの説明。Claudeはこの説明文を見て
  「いつこのスキルを使うべきか」を判断するので、
  トリガーにしたいフレーズ（「〜して」など）を含めると発動しやすい。
---

# my-new-skill

## 引数
- `--dry-run` : 外部に影響する操作を行わず、結果のプレビューのみ表示

## 手順
1. （Claudeに実行させたい手順を番号付きで具体的に書く）
2. ...

## 禁止事項
- （やってはいけないことを明示する）
```

書き方のコツ:

- **description がトリガー条件**。曖昧だと発動しない・誤発動する
- 手順は「Claudeへの指示書」として書く。判断基準・出力フォーマット・失敗時の挙動まで具体的に
- 外部に影響する操作（投稿・送信・削除）があるスキルには `--dry-run` を必ず用意する
- シークレット（APIキー・Webhook URL等）は環境変数で受け取り、SKILL.md にもリポジトリにも書かない

### 2. 動作確認

プロジェクトの `.claude/skills/` にコピーして Claude Code を開き、
`/<skill-name> --dry-run` で発動と手順の動作を確認する。

### 3. バージョンを上げてコミット

1. `plugins/ai-community-tools/.claude-plugin/plugin.json` の `version` を上げる
2. この README の収録スキル表に1行追加する
3. commit して push する

新しいプラグインとして分けたい場合（用途が大きく異なるスキル群など）は、
`plugins/<new-plugin>/` を作り `.claude-plugin/marketplace.json` の `plugins` に追記する。

## License

MIT
