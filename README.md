# ai-skills

Claude Code 用スキル集。AIコミュニティ運営の自動化を目的としたスキルを配布しています。

## 収録スキル

| スキル | 説明 |
|---|---|
| `trending-ai-topics` | 実行時点でネット上で話題になっているAIトピックを収集し、読者層別（初学者向け / 開発者向け / 業界動向）に整形してSlackに投稿する |

## インストール

### Claude Code（推奨）

```
/plugin marketplace add Masaki0423/ai-skills
/plugin install ai-community-tools@ai-skills
```

### 手動インストール

このリポジトリをcloneし、使いたいスキルのディレクトリを `~/.claude/skills/` にコピーしてください。

```bash
git clone https://github.com/Masaki0423/ai-skills.git
cp -r ai-skills/plugins/ai-community-tools/skills/trending-ai-topics ~/.claude/skills/
```

claude.ai（Web / デスクトップ）の場合は、スキルのディレクトリをzipにして
「設定 → Capabilities → Skills」からアップロードできます。

## セットアップ

`trending-ai-topics` はSlackの Incoming Webhook で投稿します。
Webhook URLを環境変数に設定してください（コミット厳禁）。

`.claude/settings.local.json` の例:

```json
{
  "env": {
    "SLACK_WEBHOOK_URL": "https://hooks.slack.com/services/..."
  }
}
```

## 使い方

```
/trending-ai-topics --dry-run   # 投稿せずプレビューのみ
/trending-ai-topics             # 収集してSlackに投稿
/trending-ai-topics --count 6   # トピック数を指定
```

定期実行したい場合は、Claude Code のスケジュール実行（routine）から
`/trending-ai-topics` を呼び出すよう登録してください。

## 注意事項

- スキルは機密情報を扱いません。収集対象は一般公開されているWeb上の情報のみです
- Webhook URL は「知っていれば誰でも投稿できる」準機密です。リポジトリにコミットしないでください

## License

MIT
