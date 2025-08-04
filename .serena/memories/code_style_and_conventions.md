# コードスタイルと規約

## TypeScript設定
- **厳密モード**: 有効（strict: true）
- **ターゲット**: ES2017
- **モジュール解決**: bundler
- **JSX**: preserve（Next.js用）
- **パスエイリアス**: `@/*` -> `./src/*`

## ESLint設定
- **ベース設定**: next/core-web-vitals, next/typescript
- **無効化されたルール**:
  - `@typescript-eslint/no-explicit-any`: off
  - `react-hooks/exhaustive-deps`: off

## コード規約

### ファイル命名
- **コンポーネント**: PascalCase (例: `BottomToolbar.tsx`)
- **フック**: camelCase + `use` プレフィックス (例: `useRealtimeSession.ts`)
- **ユーティリティ**: camelCase (例: `audioUtils.ts`)
- **設定ファイル**: camelCase (例: `index.ts`)

### ディレクトリ構造
- **コンポーネント**: `src/app/components/`
- **フック**: `src/app/hooks/`
- **コンテキスト**: `src/app/contexts/`
- **ライブラリ**: `src/app/lib/`
- **エージェント設定**: `src/app/agentConfigs/`

### インポート規約
- 絶対パス: `@/` エイリアス使用
- 相対パス: 同一ディレクトリ内での使用

### React パターン
- **関数コンポーネント**: デフォルトエクスポート
- **カスタムフック**: named export
- **コンテキスト**: Provider パターン使用
- **型定義**: `types.ts` ファイルで管理

### OpenAI Agents SDK パターン
- **エージェント定義**: `RealtimeAgent` クラス使用
- **設定分離**: シナリオ別ディレクトリ構造
- **ハンドオフ**: `handoffs` プロパティで定義