# Claude Code への引き継ぎプロンプト

以下をそのままClaude Codeのチャット欄に貼り付けてください。

---

## プロジェクト概要

小学3年生（青ちゃん）向けの週間学習チェックリストアプリです。
HTMLファイル1枚で動くシンプルなWebアプリで、Firebase Realtime Database でチェック状態を複数デバイスにリアルタイム同期しています。

---

## ファイル情報

- **ローカルファイル**: `/Volumes/Extreme SSD/案件フォルダ/羽深家のツール作成/青用/曜日別学習リスト/ao/index.html`
- **GitHub リポジトリ**: `https://github.com/sayurihabuka/habu-tools`
- **公開URL**: `https://sayurihabuka.github.io/habu-tools/ao/`
- **元デザイン参考**: `old/study-checklist-weekly5.html`（デザイン・構造の正解ファイル）

---

## Firebase 設定情報

```javascript
const firebaseConfig = {
  apiKey: "AIzaSyADUL3Zu7ZkguKuz7LUSarfAj7JFkteTMw",
  authDomain: "hahuka-tools.firebaseapp.com",
  databaseURL: "https://hahuka-tools-default-rtdb.firebaseio.com",
  projectId: "hahuka-tools",
  storageBucket: "hahuka-tools.firebasestorage.app",
  messagingSenderId: "1097903942252",
  appId: "1:1097903942252:web:f5713546094f3b4f55c649"
};
```

- **Firebase SDK バージョン**: 10.12.2（ESモジュール形式）
- **APIキー制限**: `sayurihabuka.github.io/*` のみ許可済み
- **Security Rules**: `.read: true, .write: true`（全公開、チェックデータのみのため許容）

---

## 現在の実装状況（完了済み）

- [x] Firebase Realtime Database でリアルタイム同期
- [x] `<script type="module">` でFirebase SDKをインポート
- [x] `window.toggleWeekItem` / `window.toggleDay` をグローバル公開
- [x] `localChangeTimes`（5秒グレース）で先祖返り防止
- [x] リセット書き込みを `update()` でバッチ化（onValue連鎖を抑制）
- [x] Firebase接続失敗時もUIを表示するエラーハンドリング
- [x] ファビコン設置（`ao/favicon.png` / `ao/favicon.ico`）

---

## Firebase データ構造

```
checklist/study_v2_kokugo  → { checked: [bool×8], lastResetTs: number }
checklist/study_v2_sansu   → { checked: [bool×5], lastResetTs: number }
checklist/study_v2_saile   → { checked: [bool×4], lastResetTs: number }
checklist/study_v2_eigo    → { checked: [bool×3], lastResetTs: number }
checklist/study_v2_daily_<dayId>_keisan/goi/piano/kumon → { checked: [bool], lastResetTs: number }
```

---

## カテゴリリセット設定

- kokugo / sansu: 水曜18:00
- saile: 土曜18:00
- eigo: 木曜18:00
- 毎日系（piano/keisan/goi/kumon）: 月曜00:00

---

## デザイン仕様

- 曜日カラー: 月=ピンク、火=オレンジ、水=ブルー、木=グリーン、金=黄、土=紫、日=赤
- 全曜日の背景: `#ffffff`（白）
- セクション順（各曜日）: 毎朝 → 学習 → 毎日
- item-rowのpadding: `11px 18px 11px 40px`（左40px）

---

## リポジトリ構成

```
habu-tools/
├── ao/
│   ├── index.html       ← メインアプリ
│   ├── favicon.png
│   └── favicon.ico
├── old/
│   └── study-checklist-weekly5.html  ← 元デザイン参考
├── claude_code_prompt.md             ← このファイル
└── README.md
```
