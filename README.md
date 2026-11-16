# weekday-hour-volatility-heatmap-indicator-pine

TradingView Pine v6 indicator: average range heatmap by weekday and hour

曜日×時間帯ごとの**値幅（高値 − 安値）の平均**を表にして表示するインジケーターです。「どの曜日のどの時間帯に、値動きが大きくなるか」を調べるために使います。

値動きの**方向**を調べるインジケーターは [weekday-hour-direction-heatmap-indicator-pine](https://github.com/stangler/weekday-hour-direction-heatmap-indicator-pine) です。

- ファイル名（推奨）: `weekday-hour-volatility-heatmap-indicator.pine`
- スクリプト名: `曜日×時間帯 ボラティリティ`
- 時刻: 日本時間（入力でタイムゾーンを変更できます）

## 表示内容

- 縦軸は時間（0〜23時）、横軸は曜日（月〜日）です。
- 各マスは、その曜日・時間帯の**1時間の値幅の平均**です。
- 色は、**青が小さい、赤が大きい**です。
- 平均は、読み込まれている全期間の足から計算されます。

### 単位の切り替え

| 単位 | 内容 |
|---|---|
| pips | 値幅 / (最小価格単位 × 10)（既定） |
| 価格幅 | 価格そのままの値幅 |
| % (終値比) | 値幅 / 終値 × 100 |

円ペア（小数3桁）では、1 pip = 0.01 円です。金（XAUUSD）など別の銘柄では、最小価格単位によって 1 pip の大きさが変わります。表示された数値の意味は、銘柄ごとに確認してください。

## 使い方

1. TradingView の Pine エディタで、**新規のインジケーター**を作成します。
2. `weekday-hour-volatility-heatmap-indicator.pine` の内容を貼り付けて、保存します。
3. **1時間足以下**のチャートに追加します。
4. 右中央に表が表示されます。

1時間足は、過去のデータを長く読み込めるため、各マスの標本が増えます。15分足は、過去のデータが短く、標本が少なくなります。

## 結果の例（ドル円・日本時間）

15分足、2026年6〜11月のデータで見た傾向です。

| 時間帯 | 特徴 |
|---|---|
| **21〜23時** | 最も大きい。特に木・金は 30 pips 以上（NY市場の開始と米指標の時間帯） |
| 9〜10時 | 東京の寄り付き。月曜 9 時は約 33 pips |
| 15〜17時 | 欧州勢の参入で拡大 |
| 3〜6時 | 静か（全体平均の約75%） |
| 12〜14時 | 静か |

金（XAUUSD）でも、21〜23時が最大で、10時台が全曜日で大きく、5〜8時台が静かでした。ドル円と違い、15〜17時の目立った拡大はありませんでした。

これらは1つの期間の傾向であり、将来も同じとは限りません。

## 見るときの注意（重要）

- **値幅が大きいことと、稼げることは別です。** このヒートマップは、「いつ動くか」を示すだけで、「どちらに動くか」は示しません。方向を調べるには、[方向性ヒートマップ](https://github.com/stangler/weekday-hour-direction-heatmap-indicator-pine)を使います。
- 値幅が大きい時間帯でも、方向の優位性がなければ、売買の成績は伸びません（金の検証で、同じ構造の戦略が優位性を示しませんでした）。
- 平均は、経済指標やFOMCなどのイベント日に引っ張られます。標本が少ないマスでは、特に影響が大きくなります。
- スプレッドは、値幅の大きい時間帯に広がりやすい傾向があります。

## 活用例

値幅が大きい時間帯は、方向を決めずに値動きに乗る手法（レンジブレイクなど）に向いています。ドル円では、このヒートマップで見つけた時間帯を使った戦略を、期間外で検証して残しています。

- [usdjpy-tokyo-range-breakout-strategy-pine](https://github.com/stangler/usdjpy-tokyo-range-breakout-strategy-pine)（東京レンジ→ロンドン、期間外 PF 1.304）

## 入力パラメータ

| 項目 | 既定値 |
|---|---|
| タイムゾーン | Asia/Tokyo |
| 単位 | pips |

## 表の曜日の見方

曜日は、**1時間の開始時刻の曜日**（日本時間）で数えます。たとえば、土曜の早朝（0〜6時）は、実際には金曜のNY市場の時間帯です。日曜の列は、通常は空欄になります。

## 関連リポジトリ

- [weekday-hour-direction-heatmap-indicator-pine](https://github.com/stangler/weekday-hour-direction-heatmap-indicator-pine): 曜日×時間帯の方向性ヒートマップ
- [usdjpy-tokyo-range-breakout-strategy-pine](https://github.com/stangler/usdjpy-tokyo-range-breakout-strategy-pine): バックテスト用ストラテジー
- [usdjpy-manual-trade-guide-indicator-pine](https://github.com/stangler/usdjpy-manual-trade-guide-indicator-pine): 手動運用ガイド

## 免責事項

このスクリプトは、検証と学習を目的としたものです。投資の助言ではありません。過去の成績は将来の成績を保証しません。売買は自己責任で行ってください。
