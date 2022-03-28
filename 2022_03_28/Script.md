# LT 原稿
LT 原稿です。

## 1
「C++のRanges Library」という題名で、最近のC++標準についての話をさせていただきます。tomolatoonと申します。

## 2
さて、まずは題名にも、また、この勉強会の始めで「Range関数」が出てきたりしていましたね。
それとは少し違うものですが、「Ranges Library」というものについて、概要を簡単にお話ししたいと思います。

「Ranges Library」はC++20、つまりC++の2020年のバージョンから追加された標準ライブラリです。
この「Ranges」というのは日本語で「範囲」のことで、C++では「値の集まり」として解釈することが出来ます。

「値の集まり」とは、具体的には「配列やコンテナ」など物理的に値が集まっているものや、
競技プログラミングなどをしている人は親しみ深いであろう「IOストリーム」や「ジェネレータ」などは時間軸をとって見れば値の集まりとして見ることが出来ます。

ここまで聞いて、少しC++プログラミングをしたことがある人は、先の2例は扱い方が少し違うことが思い出されるかと思います。
ですが「Ranges Library」を使うと、これらは全て全く同じ書き方で扱うことが出来るようになります。

## 3
ここからは3つ例を挙げて「Ranges Library」の凄さをお伝えしようと思います。

ところで、競技プログラミングをしている人はvectorをソートする時に、「sort関数」に「.beginと.end」を渡さないといけないことに、うざったく感じた人も居るかもしれません。
vectorをそのまま渡せないのか、と。「Ranges Library」はその期待に応えてくれます。

「Ranges Library」は、既存のものと名前が衝突しないように「ranges::」を付けた名前になっているので、「ranges::sort」という名前になりますが、
それにvectorをそのまま渡してあげることでsortをすることが出来ることになります。

## 4
次の例に行きましょう。これも競技プログラミングをした人は、「1からnまで1ずつ増えるvector」、必要になったことがあると思います。

従来では少しテクニカルなことをしない限り、スライドにあるように、まずvectorを作ってから値を埋めることになります。
左上のは「iota関数」で後から値を埋めています。この関数も従来のものなので「.beginと.end」を渡す必要があります。
左下は一番古典的にインデックスループを用いて値を埋めています。

しかし、「Ranges Library」ではもうそんな面倒なことはしません。
C++の2023年に完成する予定のバージョンである「ranges::to関数」と「views::iota」という、Rangeを作る関数を使えば、もはや初期化ですべてを完結することが出来ます。ワンライナーです！

## 5
最後の例です。何かテキトーに準備されたvectorがあった時に、そのvectorの先頭から3つ、偶数の値を取って来ることを考えます。
下準備として、「偶数の値が渡されるとtrueとなるIsEven関数」を用意しておいたと考えておいてください。

さて従来では、変数を1つ増やす必要があったり、ループの中が何だかごちゃごちゃしています。

対して、「Ranges Library」では、「偶数の要素だけ取り出す」と「先頭から3つだけ取り出す」という操作をvectorに適用することで完結してしまいます。
もはや条件はforのかっこの中に押し込まれ、forの本体では条件を満たすものに対しての処理だけに集中することができ、行数も減って、超見やすくなりました。

## 6
ここまで3例見てきましたが、どれもより簡潔に直感的なコードが書けるようになったと思います。

では最後に、3点で「Range Library」の特徴を振り返りましょう。（スライドの3点を読み上げる）
これらの特徴を組み合わせることで、より短く、直感的でわかりやすいコードを書くことが出来るようになるわけです。

## 7
「是非便利にお使いください！」
ただ、ここ数年で標準化されたライブラリなので、まだ対応していない環境が多く、使える場所が少ないのが玉に瑕です…が、早く色々な場所で使えるようになることを願っています！
標準ライブラリとしてではなければ、Range-v3というライブラリが同じことを出来るので、そちらを使ってみるのも手です。補足資料に書いておきました。