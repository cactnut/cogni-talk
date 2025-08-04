# プロジェクト概要

## プロジェクトの目的
OpenAI Realtime API と OpenAI Agents SDK を使用した音声エージェントの高度なパターンを実演するデモアプリケーション。

## 主要な機能・パターン
1. **チャット-スーパーバイザーパターン**: リアルタイムチャットエージェントが基本対話を処理し、複雑なタスクはテキストベースのスーパーバイザーモデル（gpt-4.1）に委任
2. **順次ハンドオフパターン**: 特化されたエージェント間でユーザーを転送し、特定のインテントを処理（OpenAI Swarmにインスパイア）

## テクノロジースタック
- **フレームワーク**: Next.js 15.3.1 (TypeScript)
- **スタイリング**: Tailwind CSS 3.4.1
- **主要ライブラリ**:
  - `@openai/agents` (^0.0.5) - OpenAI Agents SDK
  - `openai` (^4.77.3) - OpenAI API クライアント
  - `react-markdown` (^9.0.3) - Markdown レンダリング
  - `uuid` (^11.0.4) - ID生成
  - `zod` (^3.24.1) - スキーマ検証
- **開発ツール**: ESLint, TypeScript 5

## プロジェクト構造
- `src/app/`: メインアプリケーション
  - `App.tsx`: メインアプリケーションコンポーネント
  - `agentConfigs/`: エージェント設定とシナリオ
    - `chatSupervisor/`: チャット-スーパーバイザーパターン
    - `customerServiceRetail/`: 複雑なカスタマーサービスフロー
    - `simpleHandoff.ts`: 基本的なハンドオフデモ
  - `components/`: UI コンポーネント
  - `hooks/`: カスタムフック（`useRealtimeSession.ts`など）
  - `contexts/`: React コンテキスト（TranscriptContext, EventContext）
  - `api/`: Next.js API エンドポイント
  - `lib/`: ユーティリティ関数