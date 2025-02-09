# Markdownの基本

Zettlrは他の多くのアプリケーションと同様に、[John Gruber](https://daringfireball.net/)によって発明された`Markdown`を利用しています。もちろん、最新のMarkdownアプリケーションの可能性は、長い時間をかけた膨大な量の開発の末に生まれました。

1. [Markdownの簡単な歴史](#a-brief-history)
2. [Markdownの方言](#markdown-dialects)
3. [ZettlrにおけるMarkdownの実装](#zettlr-and-markdown)
4. [Markdown入門: 見出し, ブロック要素, インライン要素, リンク, 画像, 脚注](#markdown-101-the-most-important-codes)
5. [その他のリソース](#resources-on-markdown)

***

## 簡単な歴史

1990年代にパソコンが普及して以来、ファイルフォーマットは2つのグループに分かれています。一つは`.doc`や`.odt`のようなワードプロセッサードキュメント、もう一つは`.js`、`.cpp`、`.py`のようなコードドキュメントです。それぞれのグループのドキュメントは人間が読むためのテキストを含んでいますが、一つの大きな違いがあります。JavascriptファイルやC++ファイルがプレーンテキストのみを含む   (つまり、これらのファイルを開いたときに表示されるテキストのみを含んでいる)のに対し、ワードプロセッサードキュメントは、**もっと多くの**情報を含んでいます。ワードプロセッサードキュメントは、用紙サイズ(A4やレターサイズ)、ブロックごとの書式(見出しのフォントや引用のインデント幅)といった情報を必ず含んでいます。ワード/オフィスドキュメントをPCで開いてみるとその意味が分かりますが、フォントサイズや太さによって見出しがすぐわかるようになっています。

長らく、これらの文書フォーマットの違いは、ユーザの違いと一致していました。ほとんどのオフィスワーカーはMicrosoft WordやExcel(もしかするとLibreOfficeによる実装も)の使い方しか知りません。一方で、STEM分野から来た人々が自発的にWordやExcelなどのソフトウェアを使うことはほとんどありません。科学者たちは他の道を選択してきました。LaTeXと呼ばれる言語が開発され、大量のコードから整ったPDFファイルを生成することが可能になりました。彼らは、芸術や人文科学の研究者や行政職員などと同じワークフローに従いますが、異なるドキュメント形式を用いるのです。

Markdownの開発がJohn Gruberによって2004年に開始されたとき、それは要するに「いいとこどりできないの？」というものでした。Markdownはワープロ文書の読みやすさと、ソフトウェアコード文書の多目的で使いやすいという利点をあわせ持っています。それは、WordやWriterしか使ったことのない人にも使いやすいものです。簡単な例として、ワープロソフトで見出しを作る場合、"some text"と入力してからそれを選択し、メニューから「見出し1」を選択して書式設定します。一方Markdownでは、`# some text`と入力するだけです。ハッシュ記号が「これは見出しレベル1です」ということを表しています。

最初Markdownは、これらの利点を得るためにJohn Gruberによって書かれた小さなスクリプトでした。そして、それは多くの仕様上の矛盾を含んでおり、サポートしていない要素も多くありました。しかし、長年にわたり進歩を重ねてきました。次の2つの日付が注目に値します。

- 2004: [John Gruber](https://daringfireball.net/projects/markdown/)が最初にMarkdownを公開した
- 2012: [CommonMark](https://spec.commonmark.org/)の開発者たちがMarkdownを、国際的に受け入れられている方法で標準化した。

## Markdownの方言

今日では、Markdownの文法にはいくつかの実装が併存しています。特筆すべきものは、

- **Pandoc Markdown**: [Pandoc Markdown](https://pandoc.org/MANUAL.html#pandocs-markdown)は、テーブル、脚注、メタデータなどの文法を追加しました。アカデミックな文章を書く場合に有用なMarkdownの変種です。
- **MultiMarkdown**: 脚注、テーブル、いくつかのメタデータに関する拡張を行いました。
- **Markdown Extra**: いくつかの文法を再び拡張しました。
- **GitHub Flavoured Markdown**: ホスティングプラットフォームであるGitHub(Zettlrも、ここにホスティングされています)によって作られた方言であり、最もよく使われている方言の一つです。
- **CommonMark**: 可能な限り多くの要素を、あいまいさを回避して取り入れようとしています。注目すべきは、CommonMarkは未だに脚注の仕様を含んでいないことです。

## ZettlrとMarkdown

Zettlr自体は複数の方言の混合で実装されています。エディタでハイライトされるのはGitHub flavoured Markdownのみです。加えて、Zettelkasten要素に関してMarkdownを拡張した、追加の要素があります。これについては、[Zettelkastenメソッドについての章](../academic/zkn-method.md)に記述してあります。pandocがインストールされていない状態でHTMLへのエクスポートを行うと、Zettlrは**GitHub flavoured Markdownの文法**を使って変換を行います。可能であればpandocを使用し、その場合は**Pandoc Markdownの文法**を使ってMarkdown文書が読み込まれます。

しかし、ZettlrはMarkdownしか書けないわけではありません。使いたければ、`LaTeX`コマンドを使用することができます。これらのコマンドはPDFにエクスポートする際に正しく変換されますが、DOCXやODTに変換する場合には無視されます。HTMLに変換する場合には、そのまま残ります。もちろん、任意の個所でプレーンHTMLコードを使用することもできます。

## Markdown入門(重要な要素)

Markdownは数多くのことができますが、この章では最も重要でよく使う要素について説明し、Zettlrでの使い方を見ていきます。

### 見出し

見出しは単純です。見出し用の行を用意し、先頭にハッシュ記号を置きます。6階層までの見出しを作ることができます。

- `# Heading text` — 1段階目の見出しを作成します
- `## Heading text` — 2段階目の見出しを作成します
- `### Heading text` — 3段階目の見出しを作成します
- `#### Heading text` — 4段階目の見出しを作成します
- `##### Heading text` — 5段階目の見出しを作成します
- `###### Heading text` — 6段階目の見出しを作成します

### インライン書式

もちろん、ワープロと同じようにインラインの書式設定を行うことができます。例えば、**太字**、_斜体_、`monospaced`(コード)などです。

- `**your text**` — 太字にします
- `_your text_` — 斜体にします
- \`your text\` — 等幅フォントにします

### ブロック要素

長い引用やリストなど、テキストブロック全体を強調したい場合があります。これもMarkdownではとても簡単にできます。

- 番号無しリストを作るには各行頭に`-`か`*`か`+`を置きます。これらの文字を混ぜて使うことも可能です。
- 番号付きリストを作るには各行頭に`1.`などを置きます。

> **注意**: 番号が順番通りになっている必要はありません。エクスポートする度に、コンバーターが自動的に正しい番号を振ってくれます。なので、1, 6, 14, 2という番号を持ったリストでも、1, 2, 3, 4の番号を持ったリストとして出力されます。

### リンクと画像

リンクはインライン要素で、画像はブロック要素です。つまり、これらも上で説明した要素と同じセマンティクスにしたがいます。しかし、これらには追加の設定項目があるため注目に値します。

リンクの書き方は次の通りです。`[このテキストが最終的な文書に表示される](http://this-is-your-actual-link.tld)` Zettlrはこの文法で書かれたテキストを自動的にクリック可能なリンクに変換し、アクセスしやすくします。(そして、長いリンクを短くします) リンク先に移動するには`Alt`または`Ctrl`を押しながらクリックします。

画像もエクスクラメーションマーク(!)を頭につけることを除くと、リンクによく似ています。画像もプレーンテキストの文書に含めるわけではないので、もちろんパスが必要となります。文書に画像をリンクする方法は3種類あります。

1. ウェブURLを使用する。例えば、https://upload.wikimedia.org/wikipedia/commons/thumb/4/48/Markdown-mark.svg/1000px-Markdown-mark.svg.pngMarkdown。
2. コンピュータ内の絶対パスを使用する。例えば、`C:\Users\user-name\Pictures\my-image.jpg`。
3. コンピュータ内の相対パスを使用する。例えば、`../img/my-image.png`。

> **ヒント**: 設定ダイアログの「エディタ」タブで、画像のデフォルトパスを設定することができます。このパスは、エディタに画像を貼り付けた際に使用されます。

相対パスは、画像を貼り付けた文書からの相対パスとなります。`..`は親ディレクトリ(一つ上の階層のディレクトリ)から探すようにZettlrに指定します。文書をクラウドに保存していて複数のデバイスからアクセスする場合には、絶対パスがそれぞれ異なるはずなので(とくにOSが異なる場合)、必然的に相対パスを使用することになるでしょう。

> **ヒント**: リンクは`Cmd/Ctrl+K`、画像は`Cmd/Ctrl+Shift+I`のショートカットを使って挿入してみてください。クリップボードに有効なパスが入っている場合には、それが自動的に挿入されます。例えばリンクを作るなら、まずURLをクリップボードにコピーして、リンクにしたいテキストを選択して、それから`Cmd/Ctrl+K`を押すのがベストな方法です。すると、選択していたテキストがリンクに変わり、クリップボードに入っていたリンク先にリンクされます。

### 脚注

脚注は、芸術や人文科学の多くの研究者が関心を持っているものです。ここでは、脚注を挿入する基本的なルールと、Zettlrでそれらを取り扱う方法について学びましょう。標準的なMarkdown文法では、脚注は2つの要素を必要とします。一つ目はテキスト中に現れる参照`[^x]`です。`x`は一意な識別子です。基本的には、重複しない限り好きなものを使うことができます。しかし普通は連番を付けようとするはずです。(番号は順番通りになっている必要はありません。Markdown文書をエクスポートすれば、Pandocが自動的に脚注の番号を振りなおしてくれます。なので、後から脚注を削除することになっても番号がきちんとあっているかを気にする必要がありません。)

脚注の二つ目の要素はブロック要素である、脚注の**参照テキスト**です。これは、`[^x]: 参照テキスト。`のようなフォーマットです。見ての通り、テキスト中の参照と同じ識別子を使い、その後にコロンを置きます。常識的には、文書の一番最後のリストに参照テキストを書きます。しかし、参照テキストと脚注参照を行ったり来たりするのは面倒なので、Zettlrはその対策を用意しています。マウスカーソルを脚注参照に合わせると参照テキストが表示されます。`Cmd`または`Ctrl`を押しながらそれをクリックすると、脚注を編集することができます。`Shift+Enter`で変更を保存します。

### フェンスコードブロック

Zettlrは「フェンスコードブロック」と呼ばれるものもサポートしています。これは、インラインコード要素のブロック要素版です。空の行に三つのバックティック"\`"を書くとブロックを開始します。もう一度、空の行に三つのバックティックを書くとブロックを終了します。この2つの「フェンス」に囲まれた部分は、コードであることを示すために等幅フォントで表示されます。

Zettlrはいくつかのスクリプトとプログラム言語について、シンタックスハイライトを提供します。言語の種類を指定するには、それぞれの識別子を**開始フェンスのすぐ後に**書きます。つまり、コードフェンスでJavaScriptのハイライトを行うように指定するには、三つのバックティックのすぐ後に「javascript」の文字を書いて、コードブロックを開始します。

今のところ、以下の言語をサポートしています。（括弧の中はZettlrで使用する識別子です。混乱を防ぐため特殊文字を含まないようにしています。）

- C (`c`)
- C# (`c#`; `csharp`; `cs`)
- C++ ( `c++`; `cpp`)
- Clojure ( `clojure` )
- Common Lisp (`clisp`; `commonlisp`)
- CSS (`css`)
- Elm (`elm`)
- F# (`f#`; `fsharp`)
- Go (`go`)
- Haskell (`haskell`; `hs`)
- HTML (`html`)
- Java (`java`)
- JavaScript (`javascript`; `js`; `node`)
- JSON (`json`)
- Julia (`julia`; `jl`)
- Kotlin (`kotlin`; `kt`)
- LESS (`less`)
- Markdown (`markdown`; `md`)
- Objective C (`objective-c`; `objectivec`, `objc`)
- PHP (`php`)
- Python (`python`; `py`)
- R (`r`)
- Ruby (`ruby`; `rb`)
- Rust (`rust`; `rs`)
- Scala (`scala`)
- Scheme (`scheme`)
- Shell (`shell`; `sh`; `bash`)
- SparQL (`sparql`)
- SQL (`sql`)
- Swift (`swift`)
- SystemVerilog (`systemverilog`; `sv`)
- Tcl (`tcl`)
- Turtle (`turtle`; `ttl`)
- TypeScript (`typescript`; `ts`)
- Verilog (`verilog`; `v`)
- VHDL (`vhdl`; `vhd`)
- Visual Basic (`vb.net`; `vb`; `visualbasic`)
- XML (`xml`)
- YAML (`yaml`; `yml`)

要望に応じて追加の言語を実装します。必要なものがあれば、[利用可能な言語かどうか確認して](https://codemirror.net/mode/)GitHubにイシューをあげて、追加すべきものを知らせてください。

## ZettlrのMarkdown追加機能

GitHub flavored Markdownの拡張([仕様](https://github.github.com/gfm/)に「(extension)」と書かれているもの)に加えて、Zettlrでは次の機能を追加しています:

 - `<iframe src="https://example.com"></iframe>`要素のサポート

   > **警告**: iframe内のページからは、ローカルファイルシステムに制限なくアクセスされる恐れがあります。Frame Bustingという技術を使用すると、iframeから[Electronのバックエンドに直接干渉する](https://www.electronjs.org/docs/tutorial/security#isolation-for-untrusted-content)ことができてしまいます。iframe内のページ(および、そのページに対する攻撃者)は、コンピュータ内のすべてのデータにアクセス可能であると考えたほうが良いでしょう。

 - インライン(`$`)、およびブロック(`$$`)形式のKaTeX数式の表示: `$x/y$`、または、

        $$
        x / y
        $$

 - コードブロック内に記述した[mermaid.js](https://mermaid-js.github.io/mermaid/)図表の表示:

        ```mermaid
        graph TD
            A[Client] --> B[Load Balancer]
            B --> C[Server01]
            B --> D[Server02]
        ```

## Markdownについてのリソース

Markdownの**すべて**を学びたいですか？それは素晴らしい！すべての要素について書かれた資料が、[Learn X in Y minutes](https://learnxinyminutes.com/docs/markdown/)にあります。クリーンであいまいさのないMarkdownを書きたいなら、[CommonMarkの仕様](https://spec.commonmark.org/current/)を参照してください。また、GitHub Flavoured Markdownについての「本」を、[ここで読むことができます](https://gitbookio.gitbooks.io/markdown/content/)。 For those engaged in scholarly writing, the [Pandoc manual's section on it's extended Markdown](https://pandoc.org/MANUAL.html#pandocs-markdown) is worth reading.

