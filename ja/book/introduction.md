# はじめに

こんにちは、Nushell プロジェクトへようこそ。このプロジェクトのゴールは、シンプルなコマンドをパイプでつなぎ合わせるというシェルの Unix 哲学を現代の開発スタイルにもちこむことです。

Nu は Bash のような伝統的なシェル、PowerShell などの高度なシェル、関数型プログラミング、システムプログラミングなど、多くの分野からヒントを得ています。しかし Nu は何でもこなせることを目指すのではなく、いくつかのことをうまくこなせることに注力しています。

- モダンな雰囲気をもつ柔軟なクロスプラットフォームシェルを作ること
- データ構造を理解するコマンドラインアプリケーションを組みあわせることができること
- 現代的な CLI アプリケーションが提供する UX をそなえること

Nu になにができるかをみるには、実際に使ってみることが一番です。

`ls`コマンドを実行して最初に気づくことは、テキストブロックではなく、構造化されたテーブルデータが返ってくることです。

<<< @/snippets/introduction/ls_example.sh

このテーブルはディレクトリの内容を別の方法で表示しているだけではありません。このテーブルを利用するとスプレッドシートと同じように、よりインタラクティブにデータを操作できます。

最初に行うことはテーブルをサイズでソートすることです。これを行うには`ls`の出力を取得して、カラムの内容に基づいてテーブルをソートするコマンドに入力します。

<<< @/snippets/introduction/ls_sort_by_reverse_example.sh

この作業をおこなうために、`ls`にコマンドライン引数を渡していないことがわかります。代わりに、Nu が提供する`sort-by`コマンドを利用して、`ls`コマンドの出力をソートしています。また、一番大きなファイルを表示するために逆順に並び替えています。

Nu にはテーブルを扱うための多くのコマンドが用意されています。例えば、1 キロバイトを超えるファイルのみを表示するように`ls`コマンドの出力をフィルターできます。

<<< @/snippets/introduction/ls_where_example.sh

Unix 哲学にあるように、コマンドをつなぎ合わせることで様々な組み合わせを作り出すことができます。別のコマンドをみてみましょう。

<<< @/snippets/introduction/ps_example.sh

もしあなたが Linux を利用しているなら`ps`コマンドには馴染みがあるでしょう。これを使うと、現在システムが実行しているすべてのプロセスの状態や名前の一覧を取得することができます。プロセスの CPU 負荷も確認することができます。

CPU をアクティブに利用しているプロセスを表示したい場合はどうでしょうか。さきほどの`ls`コマンドと同じように、`ps`コマンドが返すテーブルを利用することができます。

<<< @/snippets/introduction/ps_where_example.sh

これまで、`ls`と`ps`を利用してファイルやプロセスの一覧を表示しました。Nu はこの他にも便利なテーブルを作り出すコマンドを提供します。次に`date`と`sys`をみてみましょう。

`date now`を実行すると、現在の日時と時間に関する情報が得られます。

<<< @/snippets/introduction/date_example.sh

`sys`は Nu が実行されているシステムに関する情報を提供します。

<<< @/snippets/introduction/sys_example.sh

これはさきほどまでのテーブルと少し異なります。`sys`コマンドは単純な値ではなくセルに構造化されたテーブルを含むテーブルを提供します。このデータを見るには表示する列を選択する必要があります。

<<< @/snippets/introduction/sys_get_example.sh

`get`コマンドを利用するとテーブルのカラムの内容を調べることができます。ここでは、Nu が実行されているホストに関する情報を含む"host"列を調べています。OS の名前、ホスト名、CPU などです。システム上のユーザーの名前を取得してみましょう。

<<< @/snippets/introduction/sys_get_nested_example.sh

現在、システムには"jonathan"という名前のユーザが１人だけいます。列の名前だけではなくパスも渡せることに気づくでしょう。Nu はパスを受け取るとテーブルの対応するデータを取得します。

テーブルデータではなく、文字列"jonathan"を取得したことに気づかれたかもしれません。Nu はテーブルだけでなく文字列も扱います。文字列は Nu 以外のコマンドを扱う上で重要な役割をはたします。

実際に Nu の外で文字列がどのように機能するか見てみましょう。先ほどの例で外部の`echo`コマンドを実行します。(`^`は組込みの`echo`コマンドを使用しないよう指示しています)。

<<< @/snippets/introduction/sys_get_external_echo_example.sh

するどい読者にはこれが以前ものと似ていると思われるでしょう。しかし、さきほどの出力で`echo`を呼び出しているという重要な違いがあります。このように、Nu からデータを`echo`(または`git`のような Nu 以外の任意のコマンド)にわたすことができるのです。

注：Nu の組み込みコマンドのヘルプテキストは、`help`コマンドで検出できます。

<<< @/snippets/introduction/help_example.sh
