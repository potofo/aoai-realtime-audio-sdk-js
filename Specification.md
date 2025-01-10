# Azure OpenAIリアルタイム音声チャットアプリケーション仕様書

## 1. プロジェクト概要

### 1.1 目的
- Azure OpenAIのリアルタイム音声チャット機能のデモンストレーション
- ブラウザベースのインタラクティブな音声対話システムの実装

### 1.2 主要機能
- リアルタイム音声入力と認識
- Azure OpenAIとのリアルタイム双方向通信
- リアルタイム音声出力
- カスタマイズ可能なシステムメッセージ
- 応答温度の調整機能
- 環境変数による設定管理

## 2. 技術仕様

### 2.1 開発環境
- Node.js
- TypeScript
- Vite開発サーバー

### 2.2 主要依存関係
- rt-client: Azure OpenAIのリアルタイムオーディオSDK
- @azure/identity: Azure認証ライブラリ
- AudioWorklet API: 低遅延音声処理

### 2.3 音声処理仕様
- サンプルレート: 24000Hz
- 入力処理: Web Audio API
- 出力処理: AudioWorklet
- 音声認識: Whisper-1モデル
- VAD (Voice Activity Detection): サーバーサイド実装

## 3. システムアーキテクチャ

### 3.1 コアコンポーネント
1. メインアプリケーション（main.ts）
   - UIコントロール
   - セッション管理
   - メッセージ処理
   - 音声ストリーム制御
   - 環境変数からの設定読み込み

2. 音声録音システム（recorder.ts）
   - マイク入力処理
   - 音声バッファ管理
   - AudioWorklet処理

3. 音声再生システム（player.ts）
   - 音声出力制御
   - バッファ再生管理
   - リアルタイム音声合成

### 3.2 通信プロトコル
- WebSocketベースの双方向通信
- バイナリ音声データのBase64エンコード
- JSONベースのメッセージング

## 4. ユーザーインターフェース

### 4.1 設定項目
- エンドポイントURL（環境変数: VITE_AZURE_OPENAI_ENDPOINT）
- APIキー（環境変数: VITE_AZURE_OPENAI_KEY）
- デプロイメント/モデル選択（環境変数: VITE_AZURE_OPENAI_DEPLOYMENT）
- システムメッセージ（環境変数: VITE_AZURE_OPENAI_SYSTEM_MESSAGE）
- 温度パラメータ（環境変数: VITE_AZURE_OPENAI_TEMPERATURE）
- 音声選択（環境変数: VITE_AZURE_OPENAI_VOICE）
- Azure OpenAI使用フラグ（環境変数: VITE_USE_AZURE_OPENAI）

### 4.2 操作機能
- 録音開始/停止
- テキスト表示クリア
- Azure/OpenAI切り替え

## 5. 既知の制限事項
1. 接続エラーの優雅な処理が未実装
2. ~~音声選択機能が未実装~~ （実装済み）
3. Entraを使用したキーレス認証は将来のアップデートで対応予定

## 6. セットアップと実行

### 6.1 前提条件
1. Node.jsのインストール
2. ローカルホストWebサーバーが実行可能な環境

### 6.2 実行手順
1. 依存パッケージのインストール: `npm install`
2. .envファイルの設定
3. 開発サーバーの起動: `npm run dev`
4. ブラウザでアクセス: `http://localhost:5173/`

### 6.3 環境変数の設定
1. プロジェクトルートに`.env`ファイルを作成
2. 以下の環境変数を設定：
   ```
   VITE_AZURE_OPENAI_ENDPOINT=https://your-resource-name.openai.azure.com/
   VITE_AZURE_OPENAI_KEY=your-api-key
   VITE_AZURE_OPENAI_DEPLOYMENT=your-deployment-name
   VITE_AZURE_OPENAI_SYSTEM_MESSAGE="AIアシスタントの指示"
   VITE_AZURE_OPENAI_TEMPERATURE=0.8
   VITE_AZURE_OPENAI_VOICE=en-US-JennyMultilingualNeural
   VITE_USE_AZURE_OPENAI=true
   ```

### 6.4 操作手順
1. 環境変数が正しく設定されていることを確認
2. フォームフィールドに自動的に設定値が読み込まれる
3. 必要に応じて設定値を調整
4. 「Record」ボタンでセッション開始