# 作成時メモ

## 構成要素(XMLレベルの話)

- `ThingDef`
  - `BasePawn` を親とする必要がありそう
  - `BaseMechanoid` を親とした場合、メカクラスターやら何やらに混ざる可能性がある？
- `PawnKindDef`
  - これについては、`LightMechanoidKind` のような定義済みの親を参照させて良さそう
- `BodyDef`
  - 構成パーツ(身体部位)の組み合わせ、というか位置の定義？
  - `//ThingDef/race/body` から参照される
- `BodyPartDef`
  - 構成パーツそのものの定義
  - `//BodyDef/corePart/def` であったり `/Defs/BodyDef/corePart/parts/li/parts/li/def` から参照される
- `RecipeDef`
  - 単純に培養器のレシピなので新設が必要

## 体の構成 `BodyDef` について

- `corePart` を根とし、 `Part` をノードとした木構造
  - 枝については `parts` として保持する
  - ※`corePart` 自身も `Part` である
- 各 `Part` は対応するボディーパーツの情報 `BodyPartDef` を必ず持つ
- `parts` を持たない(==要素なし)場合がある
  - 手先とか足先といった、それより先に体がない部位の場合など
  - 要するに末端ノード
- `group` については 子要素が2以上 (== `parts` が複数)の場合のみ必要っぽい

## メカノイドのできる仕事・作業について

### 前提概念

- 仕事
  - 優先順位タブにのヘッダに並んでる各項目のこと
    - 「消火」とか「運搬」とか
  - XML上だと `WorkTypeDef`
- 作業
  - 優先順位タブのヘッダにマウスオーバーしたさいにズラッと表示される項目のこと
    - 仕事「運搬」の場合は、作業としては「タレットの再装填」「燃料補給」等がある
  - XML上だと `WorkGiverDef`

### 主題

- メカノイドが出来る仕事は増やせる
- 仕事の優先順位も指定できる
- ただし、作業側がメカを拒否しているパターンがある
- 拒否されている作業もメカに行わせたい場合はパッチが必要
  - ただし、他のメカノイドにも影響が出る

#### 仕事の増やし方

- `/Defs/ThingDef/race/mechEnabledWorkTypes` に `/Defs/WorkTypeDef/defName` を足す
  - 運搬させたいなら `<li>Hauling</li>`

#### 優先順位の指定

- `/Defs/ThingDef/race/mechWorkTypePriorities` に設定を加える
  - 運搬の優先度を1にしたいなら `<Hauling>1</Hauling>`

#### 拒否されている作業

- `/Defs/WorkGiverDef/canBeDoneByMechs` が拒否しているかどうかに対応
  - 例として「患者に給仕」`DoctorFeedHumanlikes` は false 指定
- `canBeDoneByMechs` が未指定の場合の挙動は不明
  - ただし、他Modの実装を見る限り、基本的には `false` っぽい

#### 拒否されている仕事を行わせる

こんな具合のパッチを当てる

```xml
<Operation Class="PatchOperationReplace">
  <xpath>Defs/WorkGiverDef[defName="DoctorFeedHumanlikes"]/canBeDoneByMechs</xpath>
  <value>
    <canBeDoneByMechs>True</canBeDoneByMechs>
  </value>
</Operation>
```

他Modによるパッチの可能性なども加味すると、実際には `PatchOperationConditional` で項目の有無チェックを行う必要がある。
