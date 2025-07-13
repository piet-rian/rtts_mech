# Return to The Star - mech

- 高効率の産業用メカノイドの追加
- 特定用途向けの戦闘用メカノイドの追加
- 有毒廃棄物パックを無害化するためのレシピの追加
- [Return to The Star - core](https://github.com/piet-rian/rtts_core) が前提Modとして必要です
- [More versatile mechanoid](https://github.com/piet-rian/mvm) との併用を想定していますが、無くても機能します
  - ただし、一部の作業ができない可能性があります

## 詳細

### 仕事対応表

| 名称 | 役割 | 消火 | 料理 | 建築 | 栽培 | 採掘 | 採集伐採 | 運搬 | 掃除 |
|------|------|------|------|------|------|------|----------|------|------|
| ジェット | 近接戦闘 | 〇 |  |  |  |  |  | 〇 |  |
| ワーク | 作業用 | 〇 | 〇 | 〇 | 〇 | 〇 | 〇 | 〇 | 〇 |

### 諸元表

|名称|メカノイドとしてのサイズ|帯域幅|開放技術|移動速度|体格|資産価値|
|-|-|-|-|-|-|-|
|ワークスター|小|3|基礎|6.0|0.6|1500|
|ジェットスター|中|3|標準|8.0|1.2|5000|

### 備考

- ジェットスター
  - シールド持ち
  - 近接攻撃はEMP属性持ち
- 他Mod連携
  - VEFが入っている場合、移動時に足場や建造物による減速がなくなる

## MID-SAVE

- 途中追加
  - 問題ありません。
- 途中削除
  - やめたほうが良いでしょう。

## CONFLICT

今のところありません。

## NOTICE

本Modは [BSD 3-Clause “New” or “Revised” License](LICENSE) [(日本語参考訳)](https://licenses.opensource.jp/BSD-3-Clause/BSD-3-Clause.html) で提供されています。

謝辞および使用している素材・ライブラリは [NOTICE.md](NOTICE.md) に記載してあります。

プルリクエストおよびイシューについては [リポジトリに対する各種貢献についての指針](https://github.com/piet-rian/.github/blob/main/CONTRIBUTING.md) を参照した上でお願いします。
