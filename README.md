# 書籍『プロになるJava』を読んでこのように理解しました
## 第1部 Javaを始める準備
### 第1章 Javaってなんだろう
##### Javaのプログラミング言語としての特徴<br>
Javaはオブジェクト指向言語だが、近年は関数型プログラミング手法を取り入れている。<br>
- オブジェクト指向言語とは、クラスという単位でプログラムをまとめて全体を構築する手法のこと。<br>
- 関数型プログラミングとは、関数を単位にプログラムをまとめる手法のこと。<br>

### 第2章 開発環境の準備と最初の一歩
第2章も引き続き環境設定に関する説明が多いのでメモを省略するが、注意点が1つ。<br>
JDKのインストールはインストーラーから行うこと。IntelliJ IDEA内でJDKを直接ダウンロードすると、OSの「パス」が設定されないため、あとで利用するjavacやjshellなどのコマンドが使えなくなる。<br>

##### プロジェクトの作成
- IntelliJ IDEAではプログラムをプロジェクトとして管理する。<br>
- JavaでデファクトスタンダードとなっているプロジェクトはMaven形式。<br>
- Maven形式プロジェクトではソースコードをクラスとしてプロジェクトディレクトリ内のsrc/main/java以下に置く。<br>

##### クラスの作成
- Javaではソースコードを記述したファイルをクラスと呼ぶ。<br>

## 第2部Javaの基本
### 第3章 値と計算
#### プログラムがうまく動かない3段階
「構文エラー」、「例外」、「期待したのと違う結果」の3段階がある。<br>
下記、構文エラーと例外の違い。<br>

##### 構文エラー
- プログラムとして解釈できず実行できなかったことを示す。<br>
- 独立したプログラムを作るときには、「プログラムを作れなかった」ことを示す。<br>

##### 例外
- プログラムを動かしてみたら正しく動作できなかったことを示す。<br>
- 独立したプログラムを作るときには、「プログラムは作れたが、正しく動作できなかった」ことを示す。<br>

#### メソッド
- メソッドとは、処理をまとめて名前を付けたもの。<br>
下記のように書く。ここで「値」とは、テキスト内では処理を行いたい文字列を置いている。メソッドにも種類があり、一部のメソッドでは「値」のことを正式には戻り値型と呼ぶらしい。詳しくはテキストの後の方で学ぶのだと思う。<br>
```
値.メソッド名()
```

##### 引数
- 引数とは、メソッドに渡すパラメータ。
テキスト内では、「値」（処理を行いたい文字列）の一部や処理を行う回数などを引数にしている。<br>
```
値.メソッド名(引数)
```

##### メソッドのシグネチャ
-	オーバーロード：名前が同じで引数が違うメソッドを用意すること。<br>
-	シグネチャ：	メソッドの名前と受け取る引数、戻り値の種類をあわせたもの<br>

#### 値と演算
##### 整数、実数の演算<br>
注意点は下記の3つ。
- Javaでは小数点のない数値は整数とみなされる。<br>
- 小数点以下までを気にする値を実数とよぶ。<br>
- 演算のどれかが実数であれば結果も実数になる。<br>
練習問題<br>
```
jshell> 7+2
$2 ==> 9

jshell> 7-2
$3 ==> 5

jshell> 7*2
$4 ==> 14

jshell> 7/2
$5 ==> 3

jshell> 7%2
$6 ==> 1

jshell> 7.0/2
$7 ==> 3.5
```

##### 文字列の連結にも+演算子を使う。<br>
注意点は下記の3つ。
- 文字列リテラルと数値リテラルを連結することもできる。<br>
- +演算子の左右のどちらかが文字列の場合は文字列の連結が行われる。<br>
- 足し算は左から行われる。<br>
	文字列が一番左に書いてある場合は、下記コードでは12と3が文字列として扱われて「test123」となる。<br>
```
jshell> "test"+12+3
$1 ==> "test123"
```

	文字列よりも左側にある数字は整数または実数として扱われて演算される。下記コードでは12と3は整数として扱われて演算されるので「15test」となる。<br>
```
jshell> 12+3+"test"
$2 ==> "15test"`
```

##### 文字列の掛け算(繰り返し)や引き算
###### repeatメソッド
- 文字列を繰り返すためのメソッド。<br>
```
"文字列".repeat(n)
```
練習問題<br>
```
jshell> "test".repeat(4)
$11 ==> "testtesttesttest"
```

###### replaceメソッド
- 文字列の一部を削除または置換するためのメソッド。<br>
```
"文字列".replace("置換する文字列の一部",  "置換された文字列の一部")
```

###### formattedメソッド
- 文字列の連結が複雑なときに使うと分かりやすくなるメソッド。<br>
```
String String.formatted(Object...)
```

- 書式指定子：書式指定子の部分が、formattedメソッドに渡した引数の値で置き換えられる。<br>
	文字列に置き換えたい場所には書式指定子「%s」を使う。 <br>
	値に置き換えたい場所には書式指定子「%d」を使う。 <br>
- 書式指定子に対して引数が足りないとき：例外 MissingFormatArgumentExceptionが発生する。<br>
- 書式指定子に対して引数が多いとき：あふれた引数は無視され、エラーも例外も示されない。<br>
例<br>
```
jshell> "test%s".formatted(12+3)
$3 ==> "test15"

jshell> "%sと%s".formatted("test","sample")
$4 ==> "testとsample"

jshell> "%d+%d=%d".formatted(2,3,2+3)
$5 ==> "2+3=5"

jshell> "%s、%sおよび%s".formatted("test","sample")
|  例外java.util.MissingFormatArgumentException: Format specifier '%s'
|        at Formatter.format (Formatter.java:2768)
|        at Formatter.format (Formatter.java:2705)
|        at String.formatted (String.java:4200)
|        at (#6:1)

jshell> "%sならびに%s".formatted("test","sample","trial")
$7 ==> "testならびにsample"
```

###### その他の文字列に関するメソッド
練習問題から<br>
文字列の長さを返すメソッド<br>
```
jshell> "test".length()
$9 ==> 4
```

文字列の一部を返すメソッド<br>
substringメソッドの引数は`削除する文字の数`であることに注意。<br>
```
jshell> "test".substring(1)
$15 ==> "est"
```

### 第4章 変数と型
#### 変数
- 変数の宣言：変数を用意すること。
- 変数に値を割り当てるには「=」（代入演算子）を使う。値を割り当てなおすこともできる。
```
var 変数名 = 値
```

練習
```
jshell> var s = "site"
s ==> "site"
```
#### 複合代入演算子
- 変数を使って計算しても、変数の保持する値は変わらない。<br>
```
jshell> var n = 5
n ==> 5

jshell> n * 3
$9 ==> 15

jshell> n
n ==> 5
```

- 変数の値を変えるには、「=」を使った割り当てが必要。<br>
```
jshell> n = n*5
n ==> 25

jshell> n
n ==> 25
```

- 上記と同じことを複合代入演算子を使って、下記のように書くことができる。<br>
- 複合代入演算子とは、演算と変数への割り当てを複合した演算子。<br>
```
jshell> n*=5
$16 ==> 25

jshell> n
n ==> 25
```

なお、複合代入演算子は<br>
- 文字列にも使うことができる。<br>
- 変数の前に付けることも後ろに付けることもできる。<br>

#### 型
型とは、値の種類のこと。<br>
##### 型の種類
以下の5種類がある。<br>
- 整数　int<br>
- 実数　double<br>
- 論理値　boolean<br>
- 文字　char<br>
- 文字列　String<br>

##### 型の確認
/v コマンドで変数の方を確認することができる。<br>
ただし、これはJShellのコマンドであって、Javaの言語ではないので注意。<br>
```
jshell> var t = "test"
t ==> "test"

jshell> /v t
|    String t = "test"
```

##### 型の指定
varが導入される前は、変数の宣言のときに型を指定する必要があった。<br>
なお、このとき右側の値（←初期値としての扱い）は必ずしも必要ない。初期値がなくても型が推論できるから。（下記に詳説）<br>
```
型 変数名 = 値
```

型の代わりにvarを使うときは右側の値から推論して変数の型が決められる（型推論という）。<br>
練習
```
jshell> int c
c ==> 0

jshell> c = 5
c ==> 5

jshell> String u
u ==> null

jshell> u = "UFO"
u ==> "UFO"

jshell> int w
w ==> 0

jshell> w = "watch"
|  エラー:
|  不適合な型: java.lang.Stringをintに変換できません:
|  w = "watch"
|      ^-----^

jshell> String w
w ==> null

jshell> w = "watch"
w ==> "watch"

jshell>  int d
d ==> 0

jshell> d = 12
d ==> 12

jshell> String d
d ==> null

jshell> d = 12
|  エラー:
|  不適合な型: intをjava.lang.Stringに変換できません:
```

##### 文字を扱う型char
charは文字列の中の文字を扱う型。<br>
char型は0から65535までの整数を扱う型。それぞれの数値に文字が割り当てられている。<br>

##### 数値の型変換
###### 整数←→実数
整数（int）と実数（doubule）を下記のように変換することができる。<br>
ただし、実数から整数に変換されるときは小数点以下を切り捨てることになる。このとき失われた値は、整数から実数に戻しても回復されない。<br>
```
jshell> int i = 234
i ==> 234

jshell> double d = i
d ==> 234.0

jshell> double d = 3.14
d ==> 3.14

jshell> int i = (int)d
i ==> 3

jshell> double e = i
e ==> 3.0
```

###### 文字列←→数値
- 文字列を整数に変換するとき、Integer.parseIntメソッドを使う。ただし、数値とみなせる文字列しか変換できない。<br>
- 文字列を実数に変換するとき、Double.parseDoubleメソッドを使う。<br>
- 数値から文字列に変換するとき、複数の方法がある。まずは空文字""と連結すればよい。カンマ区切りの文字列にする場合や実行速度が気になるときは下記参照。<br>
	- +演算子を用いて、空文字と連結する。（Java9以降ではこれで実用上問題ない）<br>
	```
	jshell> String s = 123 + ""
	s ==> "123"
	```

	- String.valueOfメソッドを使う。（Java8以前、または実行速度に厳しい場合）<br>
	```
	jshell> s = String.valueOf(123)
	s ==> "123"
	```

	- formattedメソッドを使う。（カンマ区切りの文字列にしたいとき）<br>
	```
	jshell> s = "%,d".formatted(12345)
	s ==> "12,345"
	```

	- NumberFormatクラスを使う。（変換する量が多く実行速度が気になるとき）<br>
	```
	jshell> java.text.NumberFormat.getInstance().format(12345)
	$38 ==> "12,345"
	```

##### 型の役割
複数人でプログラムを構築・運用・改良していくときに、型を明示しておくと便利。<br>
また、型を明示しておくことによって、IntelliJ IDEAの補完機能を利用して効率的にソースコードを書いていくこともできるようになる。<br>

### 第5章 標準API
- ライブラリとは、APIをまとめたもの。<br>
- APIとは、他から呼び出せるようにしたプログラム。<br>
- APIは「パッケージ」「クラス」「メソッド」の順に書く<br>
```
java.time.LocalDateTime.now()
java.time　←パッケージ
LocalDateTime　←クラス
now()　←メソッド
```

- APIを他から呼び出すときは、`import`とパッケージ名を書く。→呼び出した後は、パッケージ名を省略して記述することができる。<br>
```
jshell> import java. time.*
```

練習<br>
```
jshell> import java.time.*

jshell> LocalDate.now()
$43 ==> 2022-04-29

jshell> LocalTime.now()
$44 ==> 08:45:09.852732300
```

#### 日付時刻
- 現在日時を取得する<br>
※秒の後ろの9桁の数字はナノ秒<br>
```
jshell> java.time.LocalDate.now()
$41 ==> 2022-04-29

jshell> java.time.LocalTime.now()
$40 ==> 08:20:54.124346200

jshell>	java.time.LocalDateTime.now()
$39 ==>	2022-04-29T08:19:23.517245500
```

##### 日付時刻の操作<br>
- 日時の計算　.now()メソッドの後ろにメソッドを追記して計算させる。<br>
(例)3日後の日付はこう書く。<br>
```
jshell> LocalDateTime.now()
$45 ==> 2022-04-29T08:50:24.203177

jshell> LocalDateTime.now().plusDays(3)
$46 ==> 2022-05-02T08:50:50.355908800
```

- 変数に日付を代入する　特定の日時を使いまわすことができるようになる。<br>
```
jshell> var today = LocalDateTime.now()
today ==> 2022-04-29T08:58:49.992420800

jshell> today.plusWeeks(2)
$48 ==> 2022-05-13T08:58:49.992420800
```

- 指定した日時時刻を扱う　`LocalDate.of()`、`LocalTime.of()`、`LocalDateTime.of()`メソッドを使う。<br>

- 日付時刻の整形　`formatted`メソッドを使う。<br>

練習<br>
```
jshell> "%tY年%<tm月%<td日".formatted(java17date)
$52 ==> "2021年09月14日"

jshell> "%tY年%<tm月%<td日%tH時%<tM分".formatted(java17date,java17time)
$58 ==> "2021年09月14日14時30分"
```

月日や時分秒の値が一桁のとき、`DateTimeFormatter`クラスを使うことによって、例えば「09月」を「9月」と表示することができる。<br>
なお、「月」の"M"は大文字、「分」の"m"は小文字と決まっている。<br>
```
jshell> var formatter = java.time.format.DateTimeFormatter.ofPattern("y年M月d日")
formatter ==> Value(YearOfEra)'年'Value(MonthOfYear)'月'Value(DayOfMonth)'日'

jshell> formatter.format(java17date)
$69 ==> "2021年9月14日"

jshell> var formatter = java.time.format.DateTimeFormatter.ofPattern("y年M月d日H時m分")
formatter ==> Value(YearOfEra)'年'Value(MonthOfYear)'月'Value(Day ... )'時'Value(MinuteOfHour)' 分'

jshell> var java17datetime = LocalDateTime.of(2021,9,14,14,30)
java17datetime ==> 2021-09-14T14:30

jshell> formatter.format(java17datetime)
$72 ==> "2021年9月14日14時30分"
```

##### staticメソッドとインスタンスメソッド
- staticメソッド：クラス名を指定して呼び出すメソッド　`クラス名.メソッド名(引数)`<br>
- インスタンスメソッド：値に対して呼び出すメソッド　`値.メソッド名(引数)`<br>
- 動作が全く同じで両方のメソッドで書ける場合がある。何をしたいかが分かる書き方を選ぶのがコツ。<br>
	例：formatメソッド（staticメソッド）とformattedメソッド（インスタンスメソッド）。<br>
	- staticメソッドは「値.メソッド」の形で呼び出すこともできるが、できるだけ避ける。このときの値は無視されて、想定外の結果になることがあるため。<br>

練習<br>
```
jshell> LocalDate.of(2020,2,28).plusDays(1)
$74 ==> 2020-02-29

jshell> LocalDate.of(2020,2,28).plusWeeks(2)
$75 ==> 2020-03-13
```
```
jshell> String.format("%tm月",today)
$78 ==> "04月"

jshell> String.format("%sは%d","two",2)
$79 ==> "twoは2"

jshell> "%tY年".formatted(today)
$80 ==> "2022年"
```

#### BigDecimal
- 実数(double)の演算は2進数で行われるため、桁数が多いと10進数での計算と誤差が生じる場合がある。<br>
- 10進数で計算させるときに使えるのがBigDecimalクラス。<br>
- BigDecimalクラスからvalueOfメソッドを使って10進数のオブジェクトを生成し、計算に用いる。 `BigDecimal.valueOf(値)`<br>
- BigDecimalでは演算子を使えないので、演算子に対応したメソッドを使う。<br>
- BigDecimalでの計算は記述が長くなるので、変数に代入するのが実用的。<br>
- `BigDecimal.valueOf(値)`オブジェクトでは桁数が15桁以上の実数を受け取ることができない。→ new演算子を用いて`new BigDecimal(値)`と書いて受け取る。<br>
- newを使ってクラスからオブジェクトを作成するコード：`new クラス名(引数)`
練習<br>
```
jshell> 119999 * 0.1
$86 ==> 11999.900000000001

jshell> BigDecimal.valueOf(119999).multiply(BigDecimal.valueOf(0.1))
$87 ==> 11999.9

jshell> var b119999 = BigDecimal.valueOf(119999)
b119999 ==> 119999

jshell> var b01 = BigDecimal.valueOf(0.1)
b01 ==> 0.1

jshell> b119999.multiply(b01)
$90 ==> 11999.9

jshell> var r2 = new BigDecimal("1.4142135623730950488")
r2 ==> 1.4142135623730950488

jshell> r2.multiply(r2)
$96 ==> 1.99999999999999999999522356663907438144
```
> 「new クラス名(引数)」によりBigDecimalクラスから作成したオブジェクトを変数r2に代入している。<br>
> multiplyはメソッド<br>

### 第6章 SwingによるGUI
- Swingとは、ウィンドウを出すためのライブラリ。<br>
	> ライブラリとは、APIをまとめたもの。APIとは、他から呼び出せるようにしたプログラム。<br>
	> APIは「パッケージ」「クラス」「メソッド」の順に書く。<br>
	> APIを他から呼び出すときは、`import`とパッケージ名を書く。importしたら「パッケージ」の記述を省略できる。<br>
#### ウィンドウを表示する。　`JFrame`クラス
```
jshell> import javax.swing.*

jshell> var f = new JFrame("test")
f ==> javax.swing.JFrame[frame0,0,0,0x0,invalid,hidden, ... tPaneCheckingEnabled=true]

jshell> f.setVisible(true)

jshell> f.setSize(600,400)

jshell> f.setLocation(200,200)

jshell> f.getLocation()
$6 ==> java.awt.Point[x=200,y=200]
```
> - `javax.swing`パッケージをimportした。このパッケージのクラスのひとつである`JFrame`クラスとそのメソッドを使ってウィンドウを表示する。<br>
> - `JFrame`クラスからnewを用いてオブジェクトを作成する。引数（ウィンドウのタイトルになる）を文字列"test"とし、変数fに割り当てた。<br>
> - この変数fに`値.メソッド(引数)`（インスタンスメソッド）の形でウィンドウの表示／非表示を設定するメソッド`setVisible`、ウィンドウのサイズを設定するメソッド`setSize`、ウィンドウの大きさを設定するメソッド`setSize`、ウィンドウの表示位置を設定するメソッド`setLocation`、ウィンドウの表示位置を取得するメソッド`getLocation`を用いた。<br>

#### 入力領域を配置する。　`JText.Field`クラス
```
jshell> var t = new JTextField()
t ==> javax.swing.JTextField[,0,0,0x0,invalid,layout=ja ... rizontalAlignment=LEADING]

jshell> f.add("North",t)
$6 ==> javax.swing.JTextField[,0,0,0x0,invalid,layout=javax.swing.plaf.basic.BasicTextUI$UpdateHandler,alignmentX=0.0,alignmentY=0.0,border=javax.swing.plaf.BorderUIResource$CompoundBorderUIResource@3d921e20,flags=296,maximumSize=,minimumSize=,preferredSize=,caretColor=sun.swing.PrintColorUIResource[r=51,g=51,b=51],disabledTextColor=javax.swing.plaf.ColorUIResource[r=184,g=207,b=229],editable=true,margin=javax.swing.plaf.InsetsUIResource[top=0,left=0,bottom=0,right=0],selectedTextColor=sun.swing.PrintColorUIResource[r=51,g=51,b=51],selectionColor=javax.swing.plaf.ColorUIResource[r=184,g=207,b=229],columns=0,columnWidth=0,command=,horizontalAlignment=LEADING]

jshell> t.setText("Hello")

jshell> t.getText()
$8 ==> "Hello"

jshell> var t2 = new JTextField("second")
t2 ==> javax.swing.JTextField[,0,0,0x0,invalid,layout=ja ... rizontalAlignment=LEADING]

jshell> f.add("South",t2)
$10 ==> javax.swing.JTextField[,0,0,0x0,invalid,layout=javax.swing.plaf.basic.BasicTextUI$UpdateHandler,alignmentX=0.0,alignmentY=0.0,border=javax.swing.plaf.BorderUIResource$CompoundBorderUIResource@3d921e20,flags=296,maximumSize=,minimumSize=,preferredSize=,caretColor=sun.swing.PrintColorUIResource[r=51,g=51,b=51],disabledTextColor=javax.swing.plaf.ColorUIResource[r=184,g=207,b=229],editable=true,margin=javax.swing.plaf.InsetsUIResource[top=0,left=0,bottom=0,right=0],selectedTextColor=sun.swing.PrintColorUIResource[r=51,g=51,b=51],selectionColor=javax.swing.plaf.ColorUIResource[r=184,g=207,b=229],columns=0,columnWidth=0,command=,horizontalAlignment=LEADING]

jshell> f.validate()


jshell> t.setText(t2.getText())

jshell> t.setText(t2.getText().toUpperCase())

// 練習
jshell> t2.setText(t.getText())

jshell> t2.setText(t.getText().toLowerCase())
```
> - 前節から`javax.swing`パッケージや変数fを引き継いでいる。<br>
> - `javax.swing`パッケージのクラスのひとつである`JTextField`クラスとそのメソッドを使ってウィンドウに入力領域を配置する。<br>
> - `JTextField`クラスからnewを用いてオブジェクトを作成し、変数tに割り当てた。<br>
> - この変数tに`値.メソッド(引数)`（インスタンスメソッド）の形で入力領域を追加するメソッド`add`、文字列を入力するメソッド`setText`、入力欄の文字列を取得するメソッド`getText`を用いた。<br>
> - `値.メソッド(引数)`の引数に`値.メソッド(引数)`を記述したり、`値.メソッド(引数)`の後ろにメソッドを追加したりすることもできる。→`値.メソッド(値.メソッド().メソッド())`<br>

#### ボタンを配置する。　`JButton`クラス
- ラムダ式：「必要なときにこの処理を呼び出してください」という式。→詳細は第10章。
```
変数名 -> 処理
```
```
jshell> var b = new JButton("Upper")
b ==> javax.swing.JButton[,0,0,0x0,invalid,alignmentX=0 ... Upper,defaultCapable=true]

jshell> f.add("Center",b)
$17 ==> javax.swing.JButton[,0,0,0x0,invalid,alignmentX=0.0,alignmentY=0.5,border=javax.swing.plaf.BorderUIResource$CompoundBorderUIResource@8e24743,flags=296,maximumSize=,minimumSize=,preferredSize=,defaultIcon=,disabledIcon=,disabledSelectedIcon=,margin=javax.swing.plaf.InsetsUIResource[top=2,left=14,bottom=2,right=14],paintBorder=true,paintFocus=true,pressedIcon=,rolloverEnabled=true,rolloverIcon=,rolloverSelectedIcon=,selectedIcon=,text=Upper,defaultCapable=true]

jshell> f.validate()

jshell> b.addActionListner(ae -> t.setText(t2.getText().toUpperCase()))
```
> - 前節までから`javax.swing`パッケージや変数f、変数tを引き継いでいる。<br>
> - `javax.swing`パッケージのクラスのひとつである`JButton`クラスとそのメソッドを使ってウィンドウに入力領域を配置する。<br>
> - `JButton`クラスからnewを用いてオブジェクトを作成し、変数bに割り当てた。<br>
> - この変数tに`値.メソッド(引数)`（インスタンスメソッド）の形で入力領域を追加するメソッド`add`、文字列を入力するメソッド`setText`、入力欄の文字列を取得するメソッド`getText`を用いた。<br>
> - ラムダ式を用いてボタンの動作を登録した。<br>

#### 参照型
- 参照型とは、オブジェクトなどを置いた場所を示す値を保持する変数。<br>

#### 画面に絵を描いてみる。　
```
jshell> import javax.swing.*

jshell> var f = new JFrame("drawing")
f ==> javax.swing.JFrame[frame0,0,0,0x0,invalid,hidden, ... tPaneCheckingEnabled=true]

jshell> f.setVisible(true)

jshell> var label = new JLabel("test")
label ==> javax.swing.JLabel[,0,0,0x0,invalid,alignmentX=0. ... rticalTextPosition=CENTER]

jshell> f.add(label)
$5 ==> javax.swing.JLabel[,0,0,0x0,invalid,alignmentX=0.0,alignmentY=0.0,border=,flags=8388608,maximumSize=,minimumSize=,preferredSize=,defaultIcon=,disabledIcon=,horizontalAlignment=LEADING,horizontalTextPosition=TRAILING,iconTextGap=4,labelFor=,text=test,verticalAlignment=CENTER,verticalTextPosition=CENTER]

jshell> f.pack()

jshell> import java.awt.image.BufferedImage

jshell> var image = new BufferedImage(600,400,BufferedImage.TYPE_INT_RGB)
image ==> BufferedImage@1dfe2924: type = 1 DirectColorModel ... 0 yOff = 0 dataOffset[0] 0

jshell> label.setIcon(new ImageIcon(image))

jshell> f.pack()
```
- 前節までと同じく、`javax.swing`パッケージの`JFrame`クラスを`new`して変数fに代入し、`setVisible`メソッドの引数に`true`を渡してウィンドウを表示させた。<br>
- 文字列や画像を表示する`JLabel`クラスから作成して変数labelに代入したオブジェクトを引数にして、上記変数fに対して`add`メソッドを呼び出した。→JLabelオブジェクトをウィンドウに配置した。中略。<br>
- 描画処理のための`java.awt.image`パッケージの`BufferedImage`クラスからコンストラクタに画像の幅、高さ、種類（色の扱い）を指定して作成したオブジェクトを変数imageに代入した。<br>
- 画像をアイコンとして扱うための`ImageIcon`クラスから変数imageを引数にして作成したオブジェクトを、さらに引数にして、画像を設定するための`setIcon`メソッドを変数labelに対して呼び出した。すると、ラベル部分が黒くなった。<br>
- 変数fに対して`pack`メソッドを呼び出すと、ウィンドウが画像のサイズに合わせて大きくなった。<br>

6.3	Javaの基本文法
6.3.1	Javaの文法
6.3.2	入力エラーの対処
6.3.3	IntelliJ IDEAを使わずに実行する

## 第3部 Javaの文法
### 第7章 条件分岐
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

### 第8章 データ構造
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

### 第9章 繰り返し
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

### 第10章 データ構造の処理
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

### 第11章 メソッド
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

### 第13章 処理の難しさの段階
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

### 第14章 クラスとインタフェース
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

### 第15章 継承
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

## 第5部 ツールと開発技法
### 第16章 ビルドツールとMaven
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

### 第17章 Javadocとドキュメンテーション
17.1	Javadocとは
17.2	ブラウザでJavadocを見る
17.2.1	標準APIのJavadoc
17.2.2	Javadocの読み方
17.2.3	英語版のJavadoc
17.3	IDEからJavadocを見る
17.4	Javadocを書く
17.5	JavadocのHTMLを生成する

### 第18章 JUnitとテストの自動化
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

### 第19章 IntelliJ IDEAを使いこなす
19.1	補完機能を使いこなす
19.1.1	補完の候補表示と補完確定
19.1.2	import文の補完
19.2	LiveTemplateと後置補完

### 第20章 バージョン管理とGit
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

## 第6部 Webアプリケーション開発
### 第21章 SpringBootでWebアプリケーションを作ってみる
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

### 第22章 Webアプリケーションにデータベースを組み込む
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
