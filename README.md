# Claude Code 安全導入テンプレート

w.f&s（池田宜史）がClaude Code導入時に使うセキュリティ設定テンプレートです。

## 含まれるファイル

| ファイル | 説明 |
|---|---|
| `CLAUDE.md` | Claude Codeへのルール指示。プロジェクト名を変えて使う |
| `.claudeignore` | `.env`等の機密ファイルをClaude Codeから物理的に隠す |

## 使い方

クライアントのプロジェクトルートに2ファイルをコピーするだけです。

```bash
# このリポジトリをダウンロード
git clone https://github.com/wfs-aiweb/claude-code-setup

# ファイルをプロジェクトにコピー
cp claude-code-setup/CLAUDE.md   your-project/
cp claude-code-setup/.claudeignore your-project/
```

その後、`CLAUDE.md` の `[プロジェクト名]` をクライアントのプロジェクト名に書き換えてください。

## この設定で防げる事故

- Claude Codeが`.env`を読んでAPIキーがログに漏れる
- `rm -rf`や`DROP TABLE`を誤って実行してデータが消える
- `git push --force`で他人のコミットを上書きする
- APIの無限リトライで高額請求が発生する

---

by [w.f&s](https://wfs-aiweb.com)
