# mc-blueprint-patterns

[mc-blueprint](https://github.com/mc-blueprint/mc-blueprint) が使う建築パターンのライブラリ。

## 内容

- `styles/`：様式の規則（柱間・階高・壁面の奥行きの層・装飾密度・屋根・既定の材質）
- `modules/`：パラメータ付きのモジュール（外壁区画・窓・門・屋根・柱頭・街灯など）。ブロックは役割（frame・wall_main など）で書き、生成時に配色・材質が割り当てられる
- `layouts/`：敷地・街路の規則（街並み・城郭・地下都市）
- `sources.yaml`：パターンの出典と許諾

## 範囲

| 担当する | 担当しない |
|---|---|
| 様式・モジュール・敷地のデータと、その検証・見本画像 | モジュールを展開する処理（mc-blueprint） |
| 許諾のある作品からのパターン抽出の記録 | 様式の配色統計（mc-blueprint-color-stats） |
| | 許諾が不明な作品の取り込み |

## 状態

設計段階。データの形式は mc-blueprint が定める。
