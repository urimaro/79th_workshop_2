### The Many Faces of Module

Rubyのパパ<br />
Matz

---

### RubyKaigiは…

---

世界で一番大きなRubyのカンファレンス<br />
RubyConfより大きい<br />
母国語で話すKeynoteを通訳付きで聴けるのは貴重

---

- concurrency: 2015
- type: 2016
- performance: 2017
    other keynote

---

天才ではない
実績のある言語デザイナー
言語好き

---

Matzにとってのプログラミング言語は<br />
「考えを伝える、まとめるもの」

---

客観的に良し悪しを語っているのに<br />
<br />
「Ruby↑多言語↓」と理解されてしまう

---

Lisp(Flavors): 多重継承<br />
左から右、下から上に並べて優先順位を決めた<br />
C3アルゴリズム

---

ユーザーからはわかりにくい

---

Mixin(Flavors)を開発

---

アイスクリームが発想の元

- バニラ: root class
- チョコチップ(Flavor)だけをインスタンス化することはできない

---

#### moduleの使われ方

---

#### 1. Mixin

---

Rubyのmodule = Flavor

---

moduleはclassクラスの親クラス

---

インスタンスを作れない
classから継承できない

---

moduleはincludeで受け継がせることができる

---

他の使い方をするようになった<br />
＜Matzのせい

---

#### 2. name space

入れ物として使う<br />
関連するclass、moduleを詰め込む<br />
ex. Net:HTTP

---

#### 3. singleton

singleton(唯一のオブジェクト)を実現するために使う<br />
ex. module FileUtils

---

#### 4. メソッドの集まり

メソッドの集合<br />
ex. module Math 

---

module_function
includeするとクラスメソッドのように使える

---

#### 5. メソッド結合

---

alias method chain

---

既存のメソッドを置き換えるテクニック

---

欠点

---

2度呼ぶと壊れる

---

Module#prependの登場<br />
安全に置き換えられるようになった

---

欠点

---

1度prependしたら外せない<br />
クラス構成はプログラムの中で<br />
簡単に変わってしまうべきではない<br />
という考え方にもとづいている

---

CLOSのmethod combinationが実現できる<br />
before/after hookを実現する機能<br />
<br />
- CLOS: common lisp object system

---

aspect指向プログラミングを<br />
module prependで実現できる

---

#### 6. Refinements

---

Rubyはopen class<br />
既存機能を書き換えることができる<br />
= monkey patch

active supportが生まれた
globalに影響がある＞＜
=> 特定の範囲内にとどめたい
=> scoped monkey patch欲しい

---

#### 使い方

---

#### 1. 既存のclassにメソッドを追加する

---

RSpecで使ってもらえればと思っているが…<br />
using書かないといけないので使われていない＞＜

---

改善したいけど、いいアイディアがない

---

#### 2. 既存のメソッドを置き換える

---

実行している場所ではrefineされるが<br />
呼び出した先ではrefineされない

---

予想外のところで置き換わることがない<br />
という見方もできる

---

#### 7. Structural signature

---

まだ提案段階<br />
構造をmoduleを使ってチェックする提案

---

```
module Str
  def to_s; end
  def to_str; end
end
obj.conform(Str)
# to_s, to_strが定義されていないと例外発生
```

---

```
is_a
```

で型チェックするべきでない

---

```
# メソッドを呼び出せるかどうかを調べる
obj.respond_to?(:method_name)
```

をまとめて行うイメージ

---

コミュニティがRubyを進めている

---

Rubyは私の言語から我々の言語となった<br />
実装することは少なくなったが、<br />
Rubyのデザイナーであることはかわらない