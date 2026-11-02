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

## データの検証

Python 3.12 の一時仮想環境に、パターン形式の検証を含む mc-blueprint の固定 commit をインストールして実行する。

様式の `roles` は generation-pipeline の生成役割名を使う。Palette の `stone_wall` は `wall_main`、`plaster` は `wall_secondary`、`timber`・柱は `frame`、窓枠は `window_frame`、`foundation`・`floor`・`roof` は同名の役割へ対応させる。庭石・砂利とデッキは `path` に対応させる。Modern の柱間は設計に明記がなく、スキーマで必須のため、記載された窓幅 3〜6 をグリッド幅として用いる。

```powershell
& 'C:\Users\<user>\AppData\Local\Python\pythoncore-3.12-64\python.exe' -m venv ..\.venv
..\.venv\Scripts\python.exe -m pip install "mc-blueprint @ git+https://github.com/mc-blueprint/mc-blueprint@9d4ec83d0306e4ec243b236d141226474ab01d0c"
..\.venv\Scripts\mcblueprint.exe check --strict .
```
