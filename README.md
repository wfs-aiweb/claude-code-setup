# Claude Code 安全導入テンプレート

w.f&s（池田宜史）がClaude Code導入時に使うセキュリティ設定テンプレートです。

## 含まれるファイル

| ファイル | 説明 |
|---|---|
| `.claude/settings.json` | `.env`等の機密ファイルの読み取りを拒否（ハードブロック）＋公式の脆弱性チェックを有効化 |
| `CLAUDE.md` | Claude Codeへの行動ルール指示。プロジェクト名を変えて使う |

## 使い方

クライアントのプロジェクトルートに2点をコピーするだけです。

```bash
# このリポジトリをダウンロード
git clone https://github.com/wfs-aiweb/claude-code-setup

# ファイルをプロジェクトにコピー（.claude フォルダごと）
cp -r claude-code-setup/.claude     your-project/
cp    claude-code-setup/CLAUDE.md   your-project/
```

その後、`CLAUDE.md` の `[プロジェクト名]` をクライアントのプロジェクト名に書き換えてください。

## 環境変数ファイルのルール（重要）

- 読み取りブロックは**ファイル名の列挙式**です。`.env.example`（値が空のサンプル）はClaude Codeが読める設計にしています（変数名の一覧を伝えるのに便利なため）
- そのため **`.env.example` / `.env.sample` に本物の値を絶対に入れない**こと
- 本物のキーを入れるファイル名は `.env` `.env.local` `.env.development` `.env.production` `.env.staging` `.env.test`（＋`.env.*.local`）のみ使うこと。**独自名（`.env.hoge` など）はブロック対象外になるため作らない**

## コード脆弱性の自動チェック（Security Guidance）

`.claude/settings.json` には、Anthropic公式・無料のプラグイン
`security-guidance@claude-plugins-official` を有効化する設定が含まれています。
AIが書いたコードの脆弱性（インジェクション・XSS・SSRF 等）をその場で自動チェックします。

- 動作には **Python 3.8以上** が必要です（`python --version` で確認）
- 確実に入れたいときは Claude Code内で `/plugin install security-guidance@claude-plugins-official` →`/reload-plugins`

## この設定で防げる事故

- Claude Codeが`.env`を読んでAPIキーがログに漏れる
- `rm -rf`や`DROP TABLE`を誤って実行してデータが消える
- `git push --force`で他人のコミットを上書きする
- APIの無限リトライで高額請求が発生する
- AIが書いたコードに脆弱性（インジェクション・XSS等）が作り込まれる

---

by [w.f&s](https://wfs-aiweb.com)
