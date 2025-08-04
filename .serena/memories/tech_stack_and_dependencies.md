# テクノロジースタックと依存関係

## フレームワーク・ランタイム
- **Next.js**: 15.3.1 (React フレームワーク)
- **React**: 19.0.0
- **TypeScript**: 5

## 主要依存関係
- `@openai/agents`: ^0.0.5 - OpenAI Agents SDK
- `openai`: ^4.77.3 - OpenAI API クライアント
- `react-markdown`: ^9.0.3 - Markdown レンダリング
- `uuid`: ^11.0.4 - ユニークID生成
- `zod`: ^3.24.1 - スキーマ検証とバリデーション
- `@radix-ui/react-icons`: ^1.3.2 - アイコンコンポーネント
- `dotenv`: ^16.4.7 - 環境変数管理

## スタイリング・UI
- **Tailwind CSS**: 3.4.1
- **PostCSS**: 8

## 開発ツール
- **ESLint**: 9 (next/core-web-vitals, next/typescript)
- **TypeScript**: 厳密モード有効
- **@types**: Node, React, React-DOM

## 設定情報
- **TypeScript設定**: 
  - target: ES2017
  - strict mode: 有効
  - path mapping: `@/*` -> `./src/*`
- **ESLint設定**:
  - `@typescript-eslint/no-explicit-any`: off
  - `react-hooks/exhaustive-deps`: off