# MosaicFace

画像内の顔を自動検出し、モザイク・ぼかし・絵文字で隠すWebアプリ。
単一のHTMLファイルで動作し、サーバー不要・外部通信なしで完全にブラウザ上で処理します。

[![デモ動画](https://img.youtube.com/vi/Oc8OF9vtcB4/0.jpg)](https://youtube.com/shorts/Oc8OF9vtcB4)

## 特徴

- **顔の自動検出** — 画像読み込み時にTinyFaceDetectorで自動検出（タイル分割による小さい顔の検出にも対応）
- **3種類のエフェクト** — モザイク・ガウシアンぼかし・絵文字を切り替え可能
- **個別選択** — 検出された顔ごとにエフェクトの適用/除外をタップで切り替え
- **手動追加** — 検出漏れの顔をタップやドラッグで手動追加
- **適用/解除トグル** — エフェクトの適用と解除をボタンで切り替え、楕円の編集を再開可能
- **リアルタイムプレビュー** — エフェクト適用後もスライダーや種別変更で即時反映
- **楕円マスク+フェザリング** — 自然な境界で周囲に溶け込むエフェクト
- **完全自己完結** — face-api.jsライブラリとモデルの重みデータをHTML内に埋め込み済み。外部リソース不要
- **レスポンシブ対応** — PC・スマートフォンどちらでも操作可能（iOS Safari/Chrome対応）

## 使い方

1. `index.html` をブラウザで開く（またはローカルサーバー経由でアクセス）
2. 画像をドロップまたはタップして選択（自動で顔検出を実行）
3. 楕円をタップしてエフェクト対象を選択/解除（検出漏れはタップ/ドラッグで手動追加）
4. エフェクトと強さを選択し「適用」ボタンで実行
5. 「ダウンロード」で処理済み画像をPNG保存（iOSではシェアシートから保存）

## ローカルサーバーでの起動

`file://` プロトコルでも動作しますが、一部ブラウザ（iPhone Chromeなど）ではローカルサーバー経由が必要です。

```bash
cd MosaicFace
python3 -m http.server 8080
```

ブラウザで `http://localhost:8080` を開いてください。
同一ネットワーク上のスマートフォンからは `http://<PCのIPアドレス>:8080` でアクセスできます。

## 技術構成

| 要素 | 詳細 |
|---|---|
| 顔検出 | [face-api.js](https://github.com/vladmandic/face-api) (TinyFaceDetector) |
| モザイク | Canvas API ピクセル操作（ブロック平均色） |
| ぼかし | 3パスボックスブラー（ガウシアン近似、Safari/iOS対応） |
| 絵文字 | Canvas fillText |
| フェザリング | RadialGradient + globalCompositeOperation |
| モデル埋め込み | face-api.js本体 + TinyFaceDetector重みデータをインライン化 |

## ライセンス

MIT License — 詳細は [LICENSE](LICENSE) を参照してください。

### サードパーティライセンス

- **face-api.js** — MIT License ([Vladimir Mandic](https://github.com/vladmandic/face-api), [Vincent Mühler](https://github.com/justadudewhohacks/face-api.js))
  詳細は [THIRD_PARTY_LICENSES/face-api.js.LICENSE](THIRD_PARTY_LICENSES/face-api.js.LICENSE) を参照してください。
