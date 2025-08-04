# アーキテクチャ概要

## アプリケーション構造

### メインコンポーネント
- **`src/app/App.tsx`**: セッション状態、エージェント選択、UIを管理するメインコンポーネント
- **`src/app/page.tsx`**: コンテキストプロバイダー（TranscriptProvider, EventProvider）を含むNext.jsページラッパー
- **`src/app/hooks/useRealtimeSession.ts`**: WebRTC接続とセッションライフサイクルを管理するコアフック

### エージェント設定システム
- **`src/app/agentConfigs/index.ts`**: シナリオキーをエージェント配列にマッピングする中央レジストリ
- **エージェントシナリオ**:
  - `chatSupervisor/`: チャット-スーパーバイザーパターン実装
  - `customerServiceRetail/`: 認証、返品、販売を含む複雑なカスタマーサービスフロー
  - `simpleHandoff/`: グリーターと俳句ライター間の基本的なハンドオフデモ

### 主要コンポーネント
- **`BottomToolbar.tsx`**: 接続制御、PTTトグル、コーデック選択
- **`Transcript.tsx`**: メッセージ履歴とガードレール指標を含むチャットインターフェース
- **`Events.tsx`**: クライアント/サーバー通信を表示するリアルタイムイベントログ

### コンテキスト・状態管理
- **`TranscriptContext`**: 会話履歴とメッセージ状態の管理
- **`EventContext`**: デバッグ用のクライアント/サーバーイベントログ処理
- **セッション管理**: WebRTC接続、音声ストリーミング、エージェントハンドオフの処理

## 技術的詳細

### 音声・WebRTC
- オーパス48kHz vs PCMU/PCMA 8kHzのコーデック選択サポート
- `@openai/agents/realtime` SDKによる音声ストリーミング処理
- PTT（プッシュトゥトーク）モードでサーバーVADのオン/オフ切り替え

### セッション管理
- `/api/session` エンドポイントから一時的キーを取得
- `OpenAIRealtimeWebRTC` トランスポートでWebRTC接続確立
- エージェントハンドオフで再接続なしのセッション更新

### ガードレール
- `createModerationGuardrail()` による出力モデレーション実装
- ガードレール結果に基づくメッセージのIN_PROGRESS、PASS、FAIL マーキング
- トランスクリプト表示でのガードレールイベント処理

### URL ベース設定
- `?agentConfig=` パラメータによるエージェントシナリオ選択
- エージェントドロップダウンによる特定エージェント選択（再接続発生）
- `?codec=` パラメータによるコーデック設定