# 書籍『プロになるJava』を読んでこのように理解しました
## 第1部 Javaを始める準備
### 第1章 Javaってなんだろう
##### プログラミング言語とは<br>
- プログラム：コンピュータを動かす命令やデータをまとめたもの。<br>
- ソースコード：プログラムを人間に読み書きできる形にしたもの。<br>
- プログラミング言語：ソースコードの文法などの決めごとを定めた言語。<br>

##### Javaのプログラミング言語としての特徴<br>
Javaはオブジェクト指向言語だが、近年は関数型プログラミング手法を取り入れている。<br>
- オブジェクト指向言語：クラスという単位でプログラムをまとめて全体を構築する手法。<br>
- 関数型プログラミング：関数を単位にプログラムをまとめる手法。<br>

### 第2章 開発環境の準備と最初の一歩
第2章も引き続き環境設定に関する説明が多いのでメモを省略するが、注意点が1つ。<br>
JDKのインストールはインストーラーから行うこと。<br>
このとき、IntelliJ IDEA内でJDKを直接ダウンロードすると、OSの「パス」が設定されないため、あとで利用するjavacやjshellなどのコマンドが使えなくなる。<br>

##### プロジェクトの作成<br>
- IntelliJ IDEAではプログラムをプロジェクトとして管理する。<br>
- JavaでデファクトスタンダードとなっているのはMaven形式。<br>
- Maven形式プロジェクトではソースコードをクラスとしてプロジェクトディレクトリ内のsrc/main/java以下に置く。<br>

##### クラスの作成<br>
- Javaではソースコードを記述したファイルをクラスと呼ぶ。<br>

## 第2部Javaの基本
### 第3章値と計算
#### プログラムがうまく動かない3段階
構文エラー、例外、期待したのと違う結果、の3段階がある。<br>
下記、構文エラーと例外の違い。<br>

##### 構文エラー
- プログラムとして解釈できず実行できなかったことを示す。<br>
- 独立したプログラムを作るときには、「プログラムを作れなかった」ことを示す。<br>

##### 例外
- プログラムを動かしてみたら正しく動作できなかったことを示す。<br>
- 独立したプログラムを作るときには、「プログラムは作れたものの正しく動作できなかった」ことを示す。<br>

#### メソッド
- メソッドとは、処理をまとめて名前を付けたもの。<br>
`値.メソッド名()`
##### 引数
- 引数とは、メソッドに渡すパラメータ。
`値.メソッド名(引数)`
##### メソッドのシグネチャ
-	オーバーロード：名前が同じで引数が違うメソッドを用意すること。<br>
-	シグネチャ：	メソッドの名前と受け取る引数、戻り値の種類をあわせたもの<br>

#### 値と演算
##### 整数、実数の演算の注意点<br>
- Javaでは小数点のない数値は整数とみなされる。<br>
- 小数点以下までを気にする値を実数とよぶ。<br>
- 演算のどれかが実数であれば結果も実数になる。<br>

##### 文字列の連結にも+演算子を使う。注意点<br>
- 文字列リテラルと数値リテラルを連結することもできる。<br>
- +演算子の左右のどちらかが文字列の場合は文字列の連結が行われる。<br>
- 足し算は左から行われる。<br>
　文字列が一番左に書いてある場合は、下記コードで12と3が文字列として扱われて「test123」となる。<br>
	jshell> "test"+12+3
	$1 ==> "test123"
　文字列よりも左側にある数字は整数または実数として扱われて演算される。下記コードでは12と3は整数として扱われて演算されるので「15test」となる。<br>
	jshell> 12+3+"test"
	$2 ==> "15test"

##### 文字列の掛け算や引き算？
###### repeatメソッド
- 文字列を繰り返す。<br>
`“文字列”.repeat(n)`

###### replaceメソッド
- 文字列の一部を削除または置換する。<br>
`“文字列”.replace(“置換する文字列の一部”,  “置換された文字列の一部”)`

###### formattedメソッド
- 文字列の連結が複雑なときに使うと分かりやすくなる。<br>
`String String.formatted(Object...)`
- 書式指定子：書式指定子の部分が、formattedメソッドに渡した引数の値で置き換えられる。　例）%s<br>
- 書式指定子に対して引数が足りないとき：例外 MissingFormatArgumentExceptionが発生する。<br>
- 書式指定子に対して引数が多いとき：あふれた引数は無視され、エラーも例外も示されない。<br>


### 第4章変数と型
4.1	変数
-	変数の宣言：変数を用意すること。
	変数に値を割り当てるには「=」（代入演算子）を使う。値を割り当てなおすこともできる。
var 変数名 = 値
	シンボル：メソッドや変数にプログラマーがつける名前のこと。
4.1.1	複合代入演算子
-	複合代入演算子：演算と変数への割り当てを複合した演算子
	文字列にも使うことができる。
	変数の前に付けることも後ろに付けることもできる。
4.1.2	値に名前を付けるメリット
-	間違いを見つけてくれる、入力が楽になる、何を扱っているか分かりやすくなる、具体的な値を覚える必要がなくなる、変更を一箇所にまとめることができる、使う値の一覧を作ることができる。
2022/4/23現在、ここまで。
 
4.2	型
4.2.1	変数の型
4.2.2	基本型と参照型
4.2.3	変数の型を指定する
4.2.4	文字を扱う型
4.2.5	数値の型変換
4.2.6	型の役割

### 第5章標準API
5.1	日付時刻
5.1.1	APIとライブラリ
5.1.2	現在日時を取得する
5.1.3	パッケージとimport
5.1.4	日付時刻の操作
5.1.5	指定した日付時刻を扱う
5.1.6	日付時刻の整形
5.1.7	staticメソッドとインスタンスメソッド
5.2	BigDecimal
5.2.1	実数計算の誤差
5.2.2	BigDecimalでの計算
5.2.3	newによるBigDecimalオブジェクトの生成
5.2.4	BigDecimalオブジェクト生成時の注意
5.2.5	オブジェクトの生成の仕方の違い

### 第6章SwingによるGUI
6.1	Swingでのウィンドウ表示
6.1.1	Swing
6.1.2	ウィンドウを表示してみる
6.1.3	入力領域の配置
6.1.4	2つ目の入力領域
6.1.5	ボタンを配置
6.1.6	クラスとオブジェクト、インスタンス
6.1.7	参照を扱う
6.2	画面に絵を描いてみる
6.2.1	ウィンドウの準備
6.2.2	画像の準備
6.2.3	図形の描画
6.3	Javaの基本文法
6.3.1	Javaの文法
6.3.2	入力エラーの対処
6.3.3	IntelliJ IDEAを使わずに実行する

## 第3部Javaの文法
### 第7章条件分岐
7.1	論理型
7.1.1	値の比較
7.1.2	オブジェクトの大小比較
7.1.3	オブジェクトが等しいかどうかの比較
7.1.4	論理演算子
7.1.5	条件演算子
7.2	if文による条件分岐
7.2.1	if文
7.2.2	else句
7.2.3	elseif
7.3	switchによる条件分岐
7.3.1	switch文
7.3.2	default句
7.3.3	switch式
7.3.4	古い形式のswitch

### 第8章データ構造
8.1	Listで値をまとめる
8.1.1	List
8.1.2	変更のできるList
8.1.3	ジェネリクスによる型検査
8.1.4	ジェネリクスの型推論
8.1.5	ラッパークラス
8.2	配列
8.2.1	配列の初期化
8.2.2	要素を設定した配列の初期化
8.2.3	配列の要素の利用
8.2.4	多次元配列
8.3	レコードで違う種類の値を組み合わせる
8.3.1	違う種類の値をListでまとめて扱う
8.3.2	違う種類の値をまとめて扱うレコードを定義する
8.3.3	レコードのオブジェクトを生成する
8.4	Mapで辞書を作る
8.4.1	Map
8.4.2	変更可能なMap
8.4.3	イミュータブル（不変）なオブジェクト

### 第9章繰り返し
9.1	ループ構文
9.1.1	for文の基本
9.1.2	for文の応用
9.1.3	while文
9.1.4	dowhile文
9.1.5	ループのcontinueとbreak
9.2	ループに慣れる
9.2.1	デバッガーでループを覗く
9.2.2	二重ループCOLUMNi、jの次は？
9.2.3	もう少しループの練習
9.2.4	迷路ゲームを作る

### 第10章データ構造の処理
10.1	データ構造を拡張for文で扱う
10.1.1	基本for文でのListの要素の処理
10.1.2	拡張for文によるListの要素の処理
10.1.3	拡張for文による配列の要素の処理
10.1.4	値の集合の処理のパターン
10.2	Stream
10.2.1	IntelliJ IDEAによるStreamへの変換
10.2.2	Streamの構成
10.2.3	ラムダ式
10.2.4	Streamソース
10.2.5	終端処理
10.2.6	中間処理
10.2.7	Optional
10.3	基本型のStream処理
10.3.1	IntStreamで整数の処理
10.3.2	StreamとIntStreamの行き来

### 第11章メソッド
11.1	メソッドの宣言
11.1.1	JShellでのメソッド宣言
11.1.2	staticメソッドの宣言
11.1.3	インスタンスメソッドの宣言
11.1.4	IntelliJ IDEAにメソッドを宣言してもらう
11.2	ラムダ式とメソッド参照
11.2.1	ラムダ式
11.2.2	メソッド参照
11.2.3	IntelliJ IDEAでラムダ式とメソッド参照の変換
11.3	メソッドの使いこなし
11.3.1	メソッドのオーバーロード
11.3.2	メソッド呼び出しの組み合わせ
COLUMN	うまく名前を付けるのも実力のうち
11.3.3	再帰とスタック

## 第4部高度なプログラミング
### 第12章入出力と例外
12.1	ファイルアクセスと例外
12.1.1	ファイル書き込み
12.1.2	ファイル読み込み
12.1.3	例外
12.1.4	throwsで例外を押しつける
12.1.5	try句で例外に対処する
12.1.6	検査例外と非検査例外
12.1.7	例外を投げる
12.2	ネットワークでコンピュータの外の世界と関わる
12.2.1	サーバーとクライアント
12.2.2	ソケット通信とTCP/IP
12.2.3	OutputStreamでのデータ送信
12.2.4	InputStreamでのデータ受信
12.2.5	try-with-resources
12.3	Webの裏側を見てみる
12.3.1	HTTP
12.3.2	HTTPクライアント
12.3.3	HTTPSで安全なWebアクセス
12.3.4	Webクライアントライブラリ
12.3.5	Webサーバーを作る

### 第13章処理の難しさの段階
13.1	ループの難しさの段階
13.1.1	他のデータを参照するループ
13.1.2	隠れた状態を扱うループ
13.2	状態遷移と正規表現
13.2.1	状態遷移の管理とenum
13.2.2	正規表現
13.3	スタックとキュー
13.3.1	スタックとキュー
13.3.2	ツリーの探索
13.3.3	メソッドの再帰呼び出しをスタックを使った処理に置き換える
13.3.4	幅優先探索とキュー
13.3.5	計算の複雑さの階層

### 第14章クラスとインタフェース
14.1	クラス
14.1.1	クラスのメンバー
14.1.2	アクセス制御（可視性）
14.1.3	コンストラクタ
14.1.4	this
14.1.5	フィールド
14.1.6	ネステッドクラスとインナークラス
14.2	インタフェース
14.2.1	インタフェースが欲しい状況
14.2.2	インタフェースを使ってメソッドを統一的に扱う
14.2.3	必要なメソッドを実装していないときのエラー
14.2.4	実装を持ったメソッドをインタフェースに定義する
14.2.5	インタフェースにおけるアクセス制御
14.2.6	公称型と構造的部分型
14.3	ラムダ式と関数型インタフェース
14.3.1	関数型インタフェース
14.3.2	標準APIで用意されている関数型インタフェース
14.4	クラスとファイル
14.4.1	ソースファイル
14.4.2	classファイル
14.4.3	コメント
14.4.4	コマンドラインパラメータ

### 第15章継承
15.1	継承
15.1.1	クラスの継承
15.1.2	継承でのコンストラクタ
15.1.3	Objectクラス
15.1.4	メソッドのオーバーライド
15.1.5	匿名クラス
15.2	継承の活用
15.2.1	差分プログラミング
15.2.2	継承でデータを分類する
15.2.3	継承とオブジェクト指向

## 第5部ツールと開発技法
### 第16章ビルドツールとMaven
16.1	ビルドツールの必要性
16.2	Mavenの基本
COLUMN	Maven以外のJavaビルドツール
16.3	Mavenのモジュールとディレクトリ構成
16.3.1	groupIdとartifactId
16.3.2	Mavenプロジェクトのディレクトリ構成
16.4	ライブラリとMavenRepository
16.4.1	ライブラリへの依存
16.4.2	MavenCentralRepository
16.4.3	Mavenプロジェクトへライブラリを追加する
16.4.4	依存のscope
16.4.5	pom.xmlへの依存の記述
16.4.6	pom.xml記述内容のプロジェクトへの反映
16.4.7	MavenCentralRepositoryのインデックス作成
16.4.8	ライブラリの確認
16.4.9	businessCalendar4Jの動作確認
16.4.10	目的に合ったライブラリを見つける
16.5	MavenのGoal

### 第17章Javadocとドキュメンテーション
17.1	Javadocとは
17.2	ブラウザでJavadocを見る
17.2.1	標準APIのJavadoc
17.2.2	Javadocの読み方
17.2.3	英語版のJavadoc
17.3	IDEからJavadocを見る
17.4	Javadocを書く
17.5	JavadocのHTMLを生成する

### 第18章JUnitとテストの自動化
18.1	テストの自動化とは
18.1.1	JUnitのセットアップと実行
18.1.2	テストケースの実装、実装コードの修正
18.1.3	その他のアサーションメソッド
18.2	テスト自動化のヒント
18.2.1	効果的にテストケースを書く
18.2.2	テスト駆動開発
18.2.3	GUIアプリケーションやWebアプリケーションのテスト
COLUMN	時間がないからテストは書かない？
18.3	オリンピック開催年を判別するコードをテスト

### 第19章IntelliJ IDEAを使いこなす
19.1	補完機能を使いこなす
19.1.1	補完の候補表示と補完確定
19.1.2	import文の補完
19.2	LiveTemplateと後置補完

### 第20章バージョン管理とGit
20.1	アンドゥやファイルコピーによる履歴管理
20.1.1	LocalHistory
20.2	バージョン管理システム
20.2.1	Gitのインストール
20.3	Git連携を有効にする
20.4	コミット
20.4.1	コミット対象ファイルの選択
20.4.2	コミットの実行
20.4.3	ファイル追加時の確認ダイアログ
20.4.4	変更したファイルの差分とコミット
20.4.5	Gitログの確認
20.4.6	.gitignoreファイルの作成
20.5	ブランチ
20.5.1	ブランチの作成と切り換え
20.5.2	ブランチのマージ
20.6	Git誤操作後の復旧方法
20.6.1	Amend
20.6.2	Revert
20.6.3	コミットのReset

## 第6部Webアプリケーション開発
### 第21章SpringBootでWebアプリケーションを作ってみる
21.1	Webアプリケーションとフレームワーク
21.1.1	Webアプリケーションとは
21.1.2	Webアプリケーションの仕組み
21.1.3	アプリケーションフレームワークとは
21.1.4	フレームワークを利用するメリット
21.1.5	Webアプリケーション開発に使える代表的なフレームワーク
21.2	SpringBootでタスク管理アプリケーションを作ってみる
21.2.1	タスク管理アプリケーションの概要
21.2.2	Webアプリケーション用のプロジェクトを作る
21.3	RestControllerでWebアプリケーションの仕組みを学ぶ
21.3.1	@RestControllerアノテーションでコントローラを作成する
21.3.2	クライアントからのリクエストに応えるためのエンドポイントを作る
21.3.3	helloエンドポイントにアクセスしてみる
21.3.4タスク管理アプリケーションをコマンドラインから起動する
21.4	モデルを使ってアプリケーションの内部情報を保持する
21.4.1	タスクの情報を保持するためのモデルの作成
21.4.2	タスクを追加するエンドポイントの作成
21.4.3タスクを一覧表示するエンドポイントの作成
21.5	ユーザーインタフェースの作成にテンプレートエンジンを活用する
21.5.1	@Controllerアノテーションでコントローラを作成する
21.5.2	テンプレートエンジン
21.5.3	Thymeleafが使えるようにpom.xmlを修正する
21.5.4	Thymeleaf用のHTMLテンプレートを作る
21.5.5	HomeControllerのhelloメソッドを修正する
21.5.6	タスクの追加および一覧表示用のテンプレートを用意する
21.5.7	HomeControllerにタスクの一覧表示機能のエンドポイントを実装する
21.5.8	HomeControllerにタスクの追加機能のエンドポイントを実装する
21.5.9	CSSを使ってテンプレートを装飾する

### 第22章Webアプリケーションにデータベースを組み込む
22.1	データベースとは
22.1.1	DBMSの種類
22.1.2	リレーショナルデータベースとは
22.1.3	リレーショナルデータベースにアクセスするための言語「SQL」
22.1.4	Javaによるデータベース接続とJDBC
22.2	SQLでH2データベースを操作する
22.2.1	H2とは
22.2.2	pom.xmlへの依存関係の追加
22.2.3	application.propertiesへの設定の追加
22.2.4	H2コンソールを使ったデータベース接続
22.2.5	テーブルを作成するCREATE文
22.2.6	テーブルにレコードを追加するINSERT文
22.2.7	テーブルに格納されたデータを取得するSELECT文
22.2.8	すでに登録されているレコードを更新するUPDATE文
22.2.9	テーブルに登録されているレコードを削除する
22.2.10	タスク管理アプリケーションで使用するSQL文の例
22.3	SpringBootアプリケーションでSpringJDBCを使用する
22.3.1	SpringJDBCとは
22.3.2	pom.xmlへの依存関係の追加
22.3.3	テーブル初期化用のスクリプトを用意する
22.3.4	データベース操作用のクラスを作成するCOLUMNDI／DIコンテナとは
22.3.5	HomeControllerクラスを修正する
22.3.6	タスク情報の削除機能を追加する
22.3.7	タスク情報の更新機能を追加する
