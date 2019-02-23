# APIの一覧

Project-VirtuousのスクリプティングシステムにおけるAPIの一覧です。

スクリプトの仕様については [スクリプトの仕様](ScriptSpecs.md) を参照してください。

以下の文書中でスクリプト例を書いている部分は、特記していない限り `init` 関数の中身です。

## 1. APIの使用方法

基本的なデータ構造を作成するAPI以外のほとんどのAPIは `V` テーブル中に格納されています。

```lua
-- APIを使用するスクリプトの例
-- 空のオブジェクトを作成し、プレイヤーの正面0.5mのところに移動させる
local obj = V:CreateEmptyGameObject()
V:PlaceGameObjectNearPlayer(obj, 0.5)
```

## 2. データ

各種APIの引数・戻り値として扱われるデータの一覧です。

### 2.1. Unityのデータ

UnityのデータはUnityの同名クラスと互換性があります。
Unity公式ドキュメント中で利用可能なメソッドはこのシステムでも利用できます。

```lua
-- Quaternion.Eulerを用いてオイラー角(10, 20, 30)の回転を表すQuaternionを作成する
-- 参考: https://docs.unity3d.com/ja/2018.3/ScriptReference/Quaternion.Euler.html
local rotation = Quaternion.Euler(10, 20, 30)
```

#### 2.1.1. Vector2

2次元ベクトルを表します。

https://docs.unity3d.com/ja/2018.3/ScriptReference/Vector2.html

```lua
-- (1, 2) を表す2次元ベクトルを作成する
local v = Vector2(1, 2)
```

#### 2.1.2. Vector3

3次元ベクトルを表します。

https://docs.unity3d.com/ja/2018.3/ScriptReference/Vector3.html

```lua
-- (1, 2, 3) を表す3次元ベクトルを作成する
local v = Vector3(1, 2, 3)
```

#### 2.1.3. Quaternion

クォータニオンを表します。

https://docs.unity3d.com/ja/2018.3/ScriptReference/Quaternion.html

```lua
-- オイラー角(45, 0, 45)を表すクォータニオンを作成する
local q = Quaternion:Euler(45, 0, 45)
```

#### 2.1.4. Color

色を表します。

https://docs.unity3d.com/ja/2018.3/ScriptReference/Color.html

```lua
-- #33ff99の色を作成する
local c = Color(0x33 / 0xff, 1, 0x99 / 0xff)

-- 赤色を作成する
local red = Color.red
```

#### 2.1.5. TextAnchor

テキストの揃え位置を表す列挙体です。

https://docs.unity3d.com/ja/2018.3/ScriptReference/TextAnchor.html

```lua
-- 左揃え
local a = TextAnchor.MiddleLeft

-- 右下揃え
local a2 = TextAnchor.LowerRight
```

### 2.2. Project-Virtuous独自のデータ

Project-Virtuous独自のデータについて

#### 2.2.1. HighlightState

ハイライトの状態を表す列挙体です。

- 以下の状態が存在します
    - HighlightState.None
    - HighlightState.Primary
    - HighlightState.Secondary
    - HighlightState.Disabled

```lua
-- ハイライトしていない状態
local s = HighlightState.None

-- 無効化状態のハイライトをしている状態
local s2 = HighlightState.Disabled
```

## 3. オブジェクトの操作を行うAPI

この章では仮想空間中のオブジェクトの操作を行うAPIを記述しています。

### 3.1. `V:CreateEmptyGameObject(name)`

空のオブジェクトを作成する。

- 引数
    - `name`: 作成したオブジェクトの名前 (`String`)
        - デフォルト値は `"GameObject"`
- 戻り値
    - 作成したオブジェクト (`GameObject`)

### 3.2. `V:PlaceGameObjectNearPlayer(obj, distance, angle, makeZPlusAxisLookingAtPlayer)`

オブジェクトをプレイヤーの近くに移動させる。

- 引数
    - `obj`: 移動させるオブジェクト (`GameObject` もしくは `Component`)
    - `distance`: プレイヤーからの距離 (`float`)
    - `angle`: プレイヤーの正面から時計回りに何度回転したところへ移動させるかを指定する。 (`float`)
        - デフォルト値は `0`
    - `makeZPlusAxisLookingAtPlayer`: `true` の時作成したオブジェクトのZ＋方向をプレイヤーに向ける。 `false` の時、作成したオブジェクトのZ－方向ををプレイヤーに向ける。 (bool)
        - デフォルト値は `false`
- 戻り値なし

