# Claude Code 安全導入テンプレート

w.f&s（池田宜史）がClaude Code導入時に使うセキュリティ設定テンプレートです。

## 含まれるファイル

| ファイル | 説明 |
|---|---|
| `.claude/settings.json` | `.env`等の機密ファイルの読み取りを拒否する（ハードブロック） |
| `CLAUDE.md` | Claude Codeへの行動ルール指示。プロジェクト名を変えて使う |
| `.claudeignore` | 文脈・検索から機密ファイルを除外する補助設定 |

## 使い方

クライアントのプロジェクトルートに2ファイルをコピーするだけです。

```bash
# このリポジトリをダウンロード
git clone https://github.com/wfs-aiweb/claude-code-setup

# ファイルをプロジェクトにコピー（.claude フォルダごと）
cp -r claude-code-setup/.claude     your-project/
cp    claude-code-setup/CLAUDE.md   your-project/
cp    claude-code-setup/.claudeignore your-project/
```

その後、`CLAUDE.md` の `[プロジェクト名]` をクライアントのプロジェクト名に書き換えてください。

## この設定で防げる事故

- Claude Codeが`.env`を読んでAPIキーがログに漏れる
- `rm -rf`や`DROP TABLE`を誤って実行してデータが消える
- `git push --force`で他人のコミットを上書きする
- APIの無限リトライで高額請求が発生する

---

by [w.f&s](https://wfs-aiweb.com)
