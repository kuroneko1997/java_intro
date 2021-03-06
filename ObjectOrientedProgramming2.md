# オブジェクト指向2: 参照、継承

- ＜目次＞
  - <a href="#review">復習: クラスとインスタンス、コンストラクタ、カプセル化</a>
  - <a href="#refer">参照とは（教科書15章）</a>
    - <a href="#refer_1">コード例</a>
    - <a href="#refer_2">オブジェクトは参照で操作する（15.1節, pp.340-）</a>
    - <a href="#refer_3">nullはどこにもリンクしていない参照（15.2節, pp.346-）</a>
    - <a href="#refer_4">newを使って配列を作る（15.3節, pp.351-）</a>
    - <a href="#refer_5">オブジェクトの配列（15.4節, pp.358-）</a>
  - <a href="#extend">継承（教科書17章）</a>
    - <a href="#extend_1">継承とは（17.1節, pp.392-）</a>
    - <a href="#extend_2">継承ツリー（17.2節, pp.401-）</a>
    - <a href="#extend_3">protected修飾子（17.3節, pp.406-）</a>

<hr>

## <a name="review">復習: クラスとインスタンス、コンストラクタ、カプセル化</a>
- オブジェクト（モノ）中心に考える。
  - モノが所有するデータをフィールド変数とし、多くの場合、privateにする。（データ隠蔽、実装隠蔽）
  - モノが提供する機能をメソッドとし、public/(デフォルト)/privateいずれかの適切なアクセス修飾子を設定する。
    - アクセサメソッド（getter, setter）は慣習に習った名前にする。
  - オブジェクト生成時の初期化方法をコンストラクタとして用意する。
    - 戻り値を指定できない（オブジェクトへの参照を返す）。
    - 引数構成により異なるコンストラクタを用意できる（オーバーロード）。
- 実装上の流れ
  - クラスを用意する（設計する）。
  - クラスに基づきインスタンスを生成する。
  - 生成したインスタンスを介してオブジェクトを利用する。
    - インスタンスの持つフィールド変数やメソッドを利用するにはメンバ参照演算子(.)を使う。

<hr>

## <a name="refer">参照とは（教科書15章）</a>
### <a name="refer_1">コード例</a>
- Playerクラス: [Janken/Player.java](./Janken/Player.java)
  - report課題3に少しコードを追加したクラス。
- PoorPlayerクラス: [Janken/PoorPlayer.java](./Janken/PoorPlayer.java)
  - Playerクラスを継承して作成したクラス。
- Judgeクラス: [Janken/Judge.java](./Janken/Judge.java)
  - Player型オブジェクトを2つ用意して、対戦し、結果を出力するクラス。
- Mainクラス
  - [Janken/Main.java](./Janken/Main.java): Playerクラスを用いて実際にプレイするコード例。
  - [Janken/Main2.java](./Janken/Main2.java): PoorPlayerクラスを用いて実際にプレイするコード例。
- ポイント
  - 「PoorPlayerクラス」はPlayerクラスを継承している。親クラス（Playerクラス）を利用しているため、Playerクラスを想定して記述したJudgeクラスを変更せずとも利用できる。

- プログラム等のダウンロード、コンパイル、実行手順

```
# リポジトリの複製（ダウンロード）
git clone https://github.com/naltoma/java_intro.git
cd java_intro/Janken

# コンパイル
javac -d . *.java
# 実行
## package名を変更したら、実行時のパスが変わることに注意。
## ここでは変更・修正せずにコンパイル・実行している。
java Main
```

### <a name="refer_2">オブジェクトは参照で操作する（15.1節, pp.340-）</a>
- 参照型の変数で``a = b;``としても変数aには変数bを同じ参照がコピーされるだけ。（同一オブジェクトを参照している）
- Java言語では``new演算子``によってのみオブジェクトを新規作成できる。

### <a name="refer_3">nullはどこにもリンクしていない参照（15.2節, pp.346-）</a>
- 変数しただけの変数は、何も参照していない空の状態（初期化されていない）。
  - nullと参照していないとは意味が違う。

### <a name="refer_4">newを使って配列を作る（15.3節, pp.351-）</a>
- 配列の作り方
  - (1) 初期化リストによる方法。
  - (2) newでオブジェクトを作る方法。

### <a name="refer_5">オブジェクトの配列（15.4節, pp.358-）</a>

<hr>

## <a name="extend">継承（教科書17章）</a>
- 似たクラスを一つのクラスにまとめ、既存設計図を再利用して、差分だけを新たに作ることで類似クラスを作成する手法。
### <a name="extend_1">継承とは（17.1節, pp.392-）</a>
- 用語
  - スーパークラス (super class): 親クラス、基底クラス。継承元のクラスのこと。
    - **final修飾子** を付けられたクラスは、継承できない。（p.399）
      - final修飾子を付けられたメソッドは、オーバーロードできない。
      - final修飾子を付けられた変数は、定数になる（変更できない）。
  - サブクラス (sub class): 子クラス。extendsでスーパークラスを継承して作成したクラスのこと。
    - クラスメンバを新規に追加することも、オーバーロードすることもできる。
    - **クラスメンバではないコンクトラクタは、継承されない。**
      - ただし、親クラスのコンクトラクタを利用することはできる。: **super()**
    - 親クラスでprivate指定されてるクラスメンバにはアクセスできない。
    - **is-a関係: 「A is a B（AはBの一種）」** という関係を守ろう。(pp.398)

<hr>

### <a name="extend_2">継承ツリー（17.2節, pp.401-）</a>
- 継承ツリーの頂点にあるのは、（暗黙の内に継承される）Objectクラス。
  - p.401の表: Objectクラスのメソッド（全てのオブジェクトが持たねばならない機能）
  - 継承ツリー: 継承関係（クラス継承図）
    - Java言語では、クラスはスーパークラスを1つだけしか持てない。（単一継承）
      - 多重継承は、Java言語では禁止。（可能な言語もある）
        - 代替案としてインタフェース（19章）が用意されている。
  - 継承に寄るコンストラクタの連鎖
    - サブクラスのコンストラクタは、最初にスーパークラスのコンストラクタを実行して、スーパークラスのオブジェクトを初期化する必要がある。
    - サブクラスにてスーパークラスのコンストラクタ実行が省略されている場合、**引数なしのsuper()が省略されている** ものとして処理される。（super()が実行される）

<hr>

### <a name="extend_3">protected修飾子（17.3節, pp.406-）</a>
- protected修飾子の機能
  - (1) 同じパッケージのクラスからアクセスできるようにする（デフォルトアクセスと同じ）。
  - (2) サブクラスからアクセスできるようにする。
- p.409の表: アクセス修飾子の適用場所
