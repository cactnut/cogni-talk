# 推奨コマンド

## 開発コマンド

### プロジェクト起動・管理
```bash
# 依存関係のインストール
npm install

# 開発サーバー起動
npm run dev

# プロダクションビルド
npm run build

# プロダクションサーバー起動
npm start
```

### コード品質・検証
```bash
# ESLint実行
npm run lint

# TypeScript型チェック（package.jsonに明示的なスクリプトなし）
npx tsc --noEmit
```

### 環境設定
```bash
# 環境変数設定
cp .env.sample .env
# その後 OPENAI_API_KEY を設定
```

## システムコマンド（Darwin/macOS）
```bash
# ファイル一覧
ls -la

# ディレクトリ移動
cd <directory>

# ファイル検索
find . -name "*.ts" -type f

# テキスト検索
grep -r "pattern" src/

# Git操作
git status
git add .
git commit -m "message"
git push
```

## プロジェクト固有の操作
- ブラウザで http://localhost:3000 にアクセス
- URL パラメータ `?agentConfig=` でシナリオ選択
- URL パラメータ `?codec=` でコーデック選択
- 環境変数 `OPENAI_API_KEY` が必要