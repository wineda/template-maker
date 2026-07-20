# ひな形タスク（Template Tasks）

毎日の細かいタスクを、**再利用できるひな形（テンプレート）**として階層的に組み立て、
毎日それを**本日のタスク**へ展開して実行する、TODO 特化の PWA。

依存ゼロの単一 HTML（HTML/CSS/JS 一体）。バックエンドは不要で、データは端末内（localStorage）に保存されます。

## 使い方

- ローカル: 静的サーバで配信して開く（Service Worker のため `file://` ではなく http(s) 推奨）
  ```sh
  npx serve .    # など任意の静的サーバ
  ```
- 公開 / インストール: GitHub Pages 等でリポジトリ直下を配信 → ブラウザから「ホーム画面に追加」で PWA としてインストール（スタンドアロン起動・オフライン対応）。

## 主な機能

- 無制限にネストできる階層タスク（長押しドラッグで並べ替え、左右で階層の上げ下げ）
- テンプレート編集 ↔ 本日のタスクの 2 画面。ひな形をワンタップで当日へ展開
- 完了カスケード・進捗ロールアップ・達成率リング、ライト/ダークテーマ
- **自動保存（localStorage）** と **JSON エクスポート / インポート**（バックアップ・端末間移行）

## ファイル構成

| ファイル | 役割 |
|---|---|
| `index.html` | アプリ本体（UX の正） |
| `manifest.webmanifest` | PWA マニフェスト |
| `sw.js` | Service Worker（オフラインキャッシュ） |
| `icon-192.png` / `icon-512.png` | アプリアイコン（maskable 対応） |
| `.nojekyll` | GitHub Pages で静的ファイルをそのまま配信 |
| `docs/DESIGN.md` | 将来の実装（React + Java）に向けた設計書 |

## データ形式（エクスポート JSON）

```json
{ "app": "hinagata-tasks", "version": 1, "exportedAt": "...", "templates": [ ... ], "today": [ ... ] }
```
