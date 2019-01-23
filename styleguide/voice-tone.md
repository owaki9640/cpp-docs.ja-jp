# <a name="voice-and-tone-guidelines"></a>スタイルとトーンのガイドライン

開発者は、.NET Core を学んで通常の作業に使用するためにドキュメントを読みます。
執筆者の目標は、読者の目的達成を助ける有益なドキュメントを作成することです。 このガイドラインはその役に立ちます。 このスタイル ガイドには、次の 4 つの推奨事項が含まれています。
- [会話調を使用する](#use-a-conversational-tone)
- [二人称で書く](#write-in-2nd-person)
- [能動態を使用する](#use-active-voice)
- [小学 5 年生の読解レベルを対象にする](#target-a-5th-grade-reading-level)

このスタイル ガイドには上記のそれぞれの例が示されています。 .NET Core のドキュメントを作成する際に例としてご使用いただけるよう、このガイドはここに示すガイドラインに従って書かれています。 ガイドラインに従わないと記事がどのようになるかがわかるよう、対照的なサンプルも示します。

## <a name="details-on-each-guideline"></a>各ガイドラインの詳細

### <a name="use-a-conversational-tone"></a>会話調を使用する
#### <a name="appropriate-style"></a>適切なスタイル:
私たちのドキュメントを会話的なトーンにしたいと考えています。 私たちのチュートリアルや説明は、読む人が執筆者と会話しているように感じられるものになっています。
読者は、堅苦しくない会話的な形式で多くの情報を得る経験ができるでしょう。 執筆者による概念の説明を聞いているかのように感じるはずです。

#### <a name="inappropriate-style"></a>不適切なスタイル:
会話型のスタイルと、技術的なトピックをより学術的に扱ったと判断されるスタイルとを、対照的に感じる向きもあるかもしれない。 それらのリソースは大変便利であるものの、執筆者がそれらの記事を書く際のスタイルは我々のドキュメントとは大いに異なるものである。 学術誌を読むなら、トーンや執筆スタイルに大いに異なるものがあることがわかる。
非常に無味乾燥なトピックの無味乾燥な説明を読んでいると感じられる。  

上記の最初の段落は、お勧めする会話スタイルに従っています。 2 番目の段落は、学術的なスタイルです。 違いは一目瞭然です。 

### <a name="write-in-second-person"></a>二人称で書く
#### <a name="appropriate-style"></a>適切なスタイル:
記事は、読者に直接話しているかのように書いてください。 二人称を頻繁に使用する必要があります (まさにこれらの 2 つのように)。 二人称は、必ず 'あなた' という単語を使用するとは限りません。 直接、読者に向けて書いてください。 命令形の文を書きます。
読者に学んでほしいものを伝えてください。

#### <a name="inappropriate-style"></a>不適切なスタイル: 
執筆者は、三人称で書くことも選択できます。 そのモデルに従う場合、執筆者は読者を指すために使用する代名詞または名詞を見つける必要があります。 読者はしばしば、この三人称のスタイルを魅力の乏しい、読んでつまらないものに感じます。

最初の段落は、お勧めのスタイルに従っています。 2 番目の段落では三人称を使用しています。 二人称で書いてください。 はるかに読みやすいことが分かったでしょう。

### <a name="use-active-voice"></a>能動態を使用する

記事は能動態で書きます。 能動態は、その文の主語がその文の動作 (動詞) を実行することを意味しています。 これは受動態とは対照的です。受動態では、文の主語が動作を受けるように文が配置されます。 次の 2 つの例を比較してください。

>コンパイラは、ソース コードを実行可能ファイルに変換しました。

>ソース コードは、コンパイラによって実行可能ファイルに変換されました。

最初の文は能動態を使用しています。 2 番目の文は受動態で書かれています。
(上の 2 つの文は、それぞれのスタイルの別の例になっています。)

能動態の方が読みやすいので、お勧めします。 受動態は読みにくい場合があります。

### <a name="target-a-fifth-grade-reading-level"></a>小学 5 年生の読解レベルを対象にする

読者の多くは英語のネイティブ スピーカーではないため、この最終ガイドラインを示します。
世界中の読者があなたの記事を読みます。 読者が英語で知らない語彙がある可能性を考慮に入れてください。

しかし、対象読者は技術担当者です。 読者がプログラミングの知識とプログラミング用語の特定の語彙を持っていると想定できます。 オブジェクト指向プログラミング、クラス、オブジェクト、関数、メソッドは、どれもなじみ深い用語です。 しかし、記事を読んでいる誰もが正式なコンピューター サイエンスの学位を持っているわけではありません。 'べき等' などの用語を使用するのであれば、恐らく定義が必要です。

>Close() メソッドはべき等です。つまり、複数回呼び出すことができ、効果は 1 回呼び出した場合と同じです。