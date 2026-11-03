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

## モジュール一覧

| 様式 | 分類 | モジュール | 寸法（X×Y×Z） |
|---|---|---|---|
| medieval | ベイ | `medieval.bay_recessed` | 5×5×2 |
| medieval | 入口 | `medieval.entry_portico` | 5×5×3 |
| medieval | cornice/庇 | `medieval.stone_cornice` | 5×2×2 |
| medieval | 屋根縁 | `medieval.gable_eave` | 7×3×2 |
| japanese | ベイ | `japanese.engawa_bay` | 5×5×3 |
| japanese | 入口 | `japanese.genkan_entry` | 5×4×3 |
| japanese | 庇 | `japanese.noki_eave` | 5×2×2 |
| japanese | 屋根縁 | `japanese.kawara_eave` | 7×3×2 |
| modern | ベイ | `modern.glazed_bay` | 5×5×2 |
| modern | 入口 | `modern.recessed_entry` | 5×4×3 |
| modern | cornice | `modern.flat_cornice` | 5×2×2 |
| modern | 屋根縁 | `modern.parapet_eave` | 5×2×2 |

## データの検証

Python 3.12 の一時仮想環境に、パターン形式の検証を含む mc-blueprint の固定 commit をインストールして実行する。

様式の `roles` は generation-pipeline の生成役割名を使う。Palette の `stone_wall` は `wall_main`、`plaster` は `wall_secondary`、`timber`・柱は `frame`、窓枠は `window_frame`、`foundation`・`floor`・`roof` は同名の役割へ対応させる。庭石・砂利とデッキは `path` に対応させる。Modern の柱間は設計に明記がなく、スキーマで必須のため、記載された窓幅 3〜6 をグリッド幅として用いる。

`depth_layers` は外壁の frame・opening・cornice の奥行きを表す。`decoration.density` は装飾密度の許容範囲、`band_course` と `cornice` は各装飾要素の有無を表す。`modules` は bay・window・entrance・cornice・roof_edge の役割から同梱モジュールを参照し、すべて `modules/` 内に実在する必要がある。柱間は両端の柱間の座標差で扱うため、部品の X 寸法から1を引いた値を `grid.bay` と照合する。`metadata.dimensions` は各部品の用途に応じて柱間・階高・奥行き層の規則と照合する。japanese の柱間4と modern の flat 屋根は維持する。

```powershell
& 'C:\Users\ryuma\AppData\Local\Python\pythoncore-3.12-64\python.exe' -m venv ..\.venv
..\.venv\Scripts\python.exe -m pip install "mc-blueprint @ git+https://github.com/mc-blueprint/mc-blueprint@9d4ec83d0306e4ec243b236d141226474ab01d0c"
..\.venv\Scripts\mcblueprint.exe check --strict .
```
