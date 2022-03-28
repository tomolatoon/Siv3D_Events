# Siv3D勉強会 2022/3/28
Siv3D勉強会 2022/3/28 の補足資料です。

## See Also
下を読んで興味が湧いたものは、Googleで検索してもいいですが、リファレンスサイトを見るのが早いです。

C++23になっているものは、基本的にcpprefjpでは情報がないので、en.cppreference.comを参照しましょう。

- ranges - cpprefjp C++日本語リファレンス（C++23のものはほとんどない）
  - https://cpprefjp.github.io/reference/ranges.html
- Ranges library (C++20) - cppreference.com（C++23のものも割とある）
  - https://en.cppreference.com/w/cpp/ranges
- Draft C++ Standard: Contents（規格書のDraft）
  - http://eel.is/c++draft/#ranges
- Sy BrandさんのTweet（adjacent、zip系の解説アリ）
  - https://twitter.com/TartanLlama/status/1505934067023368197?s=20&t=sxBKAM4cAxg4oGH4wIvitA

## Range-v3
C++の「Ranges Library」は、Range-v3というライブラリを元にして作られています。

つまりRange-v3には、標準ライブラリに入る機能が既に実装されています！
今すぐ試したい人は、Range-v3を使ってみるのもいいでしょうね！

- Range-v3
  - https://github.com/ericniebler/range-v3

## Range Adaptor Objects
スライドで `v | views::take(5)` とかしていたんですが、このように `|` で繋げられるものは「Range Adaptor Object」と言います。

また、`std::views`以下に定義されていて、Range Adaptor Objectと呼ばないものは特別な呼び名がないので、純粋に「CPO（Customaization Point Object）」と呼びます。

Range Adaptor ObjectとCPOたちについて、

- 基本的なもの
- 大体の一覧

を掲載しておくので、興味があるものを調べてみるといいかもしれません。

## 基本的なもの
|名前|C++20か？|効果|
|:-:|:-:|:-:|
|views::filter(Function)|〇|Function が true を返す要素だけ残した View を返す|
|views::transform(Function)|〇|Range のそれぞれの要素に Function を適用した結果を要素とする View を返す|
|views::take(Integer)|〇|Range の先頭 Integer だけを取り出した View を返す|
|views::drop(Integer)|〇|Range の先頭 Integer だけを取り除いた View を返す|
|views::join|〇|Range が ネストしていればそれを平坦にした View を返す|
|views::split(Range, Delimiter)|〇|文字列に関して、Delimiter ごとに Range を分割した View を返す|
|views::reverse|〇|Range を逆順にした View を返す|
|views::elements&lt;Integer&gt;|〇|Range の各要素について、std::get&lt;Integer&gt; を適用した結果を要素とする View を返す|
|views::adjacent&lt;Integer&gt;|×|Range の先頭から末端の Integer – 1 個前までの要素について、その要素を起点とした Integer 個の要素の参照をタプルとして要素に持つ View を返す|
|views::slide(Integer)|×|Range の先頭から末端の Integer – 1 個前までの要素について、その要素を起点とした Integer 個の要素の参照をタプルとして要素に持つ View を返す|
|views::chunk(Integer)|×|Range の先頭から Integer 個ごとに分割した Range を View とした要素として持つ View を返す|
|views::zip(Ranges...)|×|複数の Range のインデックスが同じ要素への参照をタプルとして要素に持つ View を返す|

## 大体一覧

|名前|C++20か？|効果|
|:-:|:-:|:-:|
|views::all|〇|Range の参照ラッパーな Viewを返す|
|views::filter(Function)|〇|Function が true を返す要素だけ残した View を返す|
|views::transform(Function)|〇|Range のそれぞれの要素に Function を適用した結果を要素とする View を返す|
|views::take(Integer)|〇|Range の先頭 Integer だけを取り出した View を返す|
|views::take_while(Function)|〇|Range の先頭から Function が false を返す前までを取り出した View を返す|
|views::drop(Integer)|〇|Range の先頭 Integer だけを取り除いた View を返す|
|views::drop_while(Function)|〇|Range の先頭から Function が false を返す前までを取り出した View を返す|
|views::join|〇|Range が ネストしていればそれを平坦にした View を返す|
|views::join_with(Delimiter)|×|トップレベルのネストを平坦にした時 Delimiter を挿入した上で、join のように平坦にした View を返す|
|views::split(Range, Delimiter)|〇|文字列に関して、Delimiter ごとに Range を分割した View を返す|
|views::lazy_split(Range, Delimiter)|〇|任意の Range に関して、Delimiter ごとに Range を分割した View を返す|
|views::common|〇|Iterator と Sentinel が同じ型になるような View を返す|
|views::reverse|〇|Range を逆順にした View を返す|
|views::elements&lt;Integer&gt;|〇|Range の各要素について、std::get&lt;Integer&gt; を適用した結果を要素とする View を返す|
|views::adjacent&lt;Integer&gt;|×|Range の先頭から末端の Integer – 1 個前までの要素について、その要素を起点とした Integer 個の要素の参照をタプルとして要素に持つ View を返す|
|views::adjacent_transform&lt;Integer&gt;(Function)|×|Range の先頭から末端の Integer – 1 個前までの要素について、その要素を起点とした Integer 個の要素を引数にとる Function を適用した結果を要素とする View を返す|
|views::slide(Integer)|×|Range の先頭から末端の Integer – 1 個前までの要素について、その要素を起点とした Integer 個の要素の参照をタプルとして要素に持つ View を返す|
|views::chunk(Integer)|×|Range の先頭から Integer 個ごとに分割した Range を View とした要素として持つ View を返す|
|views::chunk_by(Function)|×|Range の先頭から末端の 1 個前までの要素について、その要素と次の要素を引数に取る Function が false を返した所を切れ目として分割した Range を View とした要素として持つ View を返す|
|views::counted(Iterator, Integer)|〇|Iterator を起点とした長さ Integer の View を返す|
|views::zip(Ranges...)|×|複数の Range のインデックスが同じ要素への参照をタプルとして要素に持つ View を返す|
|views::zip_transform(Function, Ranges…)|×|複数の Range のインデックスが同じ要素を引数に取る Function を適用した結果のオブジェクトを要素とする View を返す|