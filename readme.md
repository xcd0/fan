# fan74

fan90のPCB、アクリルケースの発注が終わった。暇。この間に次のキーボードを作る。  
とりあえず名前はそのまま引き継ぐ。古いものは別ブランチに残す。別リポジトリにするかも...

## コンセプト

両手用左右分離型キーボード。fan90を小さくした。 片手に37キーの予定。  
ただしキーマトリクスが余る分を小さなリセットスイッチなどで設け、  
あまり使用頻度が高くない機能を割り当てる(マイコンの設定など)。  

* 指に合わせていい感じにキーが配置されてる両手で使えるキーボード欲しい。fan90二つはちょっと...
* fan90は流行に逆らったマキシマムな設計だったので、次は長いものに巻かれる小さ目な設計にする。
* 基盤はfan90と同じように両面対応する。
* fan90では筋力的にできなかった左右分割のキーボードにする。（左右間で通信する）
* ケースはできれば3Dプリンターを使ってみる。

## 設計

## 以下古いバージョン

<details>
<summary>v1 fan90 片手用フルキーボード</summary>

## one hand keyboard fan90

片手用キーボードです。G13のような用途を想定しています。  
左手で使うことを想定していますが、右手でも使えるようにPCBは作っています。  
流行りのミニマムなキーボードとは反対方向のマキシマムな方向のキーボードです。  
両手で使うことを想定していませんが、両面対応しているので2つ用意すれば可能です。  

初めての自作キーボードなので楽しみなのと不安なのが混在しています\_(:3 」∠ )\_
あくまで初めてつくる自作キーボードであるため、当然ながら動かない可能性が高いです。

![](./img/fan.png)

<details>
<summary>開発経緯</summary>

### キーボード割ろうとしたら曲がった
* ありものは素晴らしい、でも自分で作ってみたい。よし、初めてのキーボード自作だ！PCBから作るぞ\\('ω')/
* 今使ってるhelixよい。でもErgodox的な縦のずれがあるキーボードもよさそう。そういうの作ろう...
* 左右分割型のキーボード良い。割りたい！でも左右の通信とかどうやってるんだろう...ちゃんと作れるかな...
* とりあえずキーを並べてみる。小指とか根元に近く配置しよう...
* 見た目汚いな...とりあえずきれいに並べてみるか...あれ、なんか曲がってきた...
* あれこれ片手でフルキーボードいけるんじゃ...

という感じでした\_(:3 」∠ )\_  
つまりキーボードを割ろうとしたが、  
筋力が足りなかったため（左右に分割したときの左右間の通信を電源(VCC,GND)と信号線の3本でどうやって通信してるのかわからなかったので）、  
割れずに曲がってしまった。  
次作るときは割りたい。  
名前は見た目がうちわのようになったため。  もちろん余った基板は重めの団扇として使うことができる。
鍋敷きにしてもよい。
</details>

<details>
<summary>構想</summary>

#### コンセプト
以下で東西南北を言うときは、左手で中指の方向を北とした場合の手のひらからの方向を指します。

* 片手でたくさんのキーを使える。
	* フルキーボード相当のキーを使えるものとする。
		* 現状6x15のマトリクスで87キーを配置。
		* 残り３キーはあまり使わない用途向けにリセットスイッチ部品で配置。

* 片手で使いやすい。
	* 指毎の特徴に合わせて配置する。  
		例えば
		* 親指はゲームのコントローラーで多用されるように本来非常に性能が良い。  
		しかしキーボードを使う上で親指を生かすのは難しい。  
		Twitterの投票によると親指に複数のキーを割り当てているときに使っているキーの数はせいぜい4キーらしい。  
		このキーボードでは多めに5キーを割り当てる。
		* 人差し指は性能が良くQWERTYでもほかの指より多いキーを担当する。  
		このキーボードでも人差し指の担当は多くする。
		* 中指は人差し指と同じくらいのせいのがある。中指にも多めのキーを割り当てる。
		* 薬指は中指と一緒に動かないと性能が良くないので、キーボードではあまり性能を発揮できない。
		ただし、北西方向は強く、北西方向に関しては小指より適している。。
		* 小指は短いので、北西方向の移動は難しい。  
		しかし西方向、南西方向はそこそこ性能が良い。
	* 指に合わせてキーを配置する。
		* 変則的な配置なので指１本に対して割り当てられたキーの数は様々。
			* 現状小指20、薬指15、中指12、人差し指31、親指5キー。人差し指と小指は無駄キーを含む。足しても90にはならない。
		* 将来的にはキーを立体的に配置するのもよいが、現状は平面に配置。
	* 指は伸ばした状態のほうが押しやすく、キーを押し分けやすい。
		* 指の根本に近いキーよりも指を伸ばしたときに押すキーのほうが押しやすい。
		* 指の根元に近いキーを減らし、指を伸ばしたときに押すキーを増やす。
	* レイヤーは極力つかわない。
		* シフトキーのように押しながら操作することは片手だと難しい。

* すべてのキーを常に使うキーにはせず、使う用途に合わせてカスタマイズできるよう、無駄にキーを配置する。

#### 実現方法

* 以下の2点からキーを扇状に配置する。
	* 小指の性能を発揮できるように小指のキーは手首側に寄せる。
	* 伸ばした状態で使える人差し指、中指のキーを増やす。
* 列方向には揃えず、行方向にはそろえる。
* 無駄にキーを小指の西側、人差し指の東側、すべての指の北側に配置する。つまり一回り大きくする。

#### 将来的にやりたいこと

* QMKを使わずに作る。(現状使う)
* C以外の言語で作る。(現状C言語)
* マイコンを複数種類使えるようにする。(現状むずかしい)
* raspberry pi zeroと画面を搭載して、それ単体でPCとして動作させ多機能にする。(現状ソケットのみ用意)
* ケースを3Dプリンターなどでつくる。
* キーを立体的に配置する。

</details>

### PCB設計

kicadを使って設計した。

回路は6x15のマトリクス。column方向からスキャンし、rowを検出する。  
column方向のスキャンは床に転がっていたSN74HC595を使う。  
シフトレジスタを使えば簡単にスキャンできそう。  
これで信号線数を15-5で10本減らせることになる。  
pro microはデジタルIOピンが14本、デジタルとしても使えるアナログIOピンが4本なので、
最大18本をデジタルIOとして使うことができる。
6本をrowのデジタル入力に、5本をシフトレジスタへのデジタル出力に、
2本をリセットスイッチに使用することにした。
配置は特にこだわりなく並べた。このせいで後々苦労するかもしれないがまあ初めてなので良しとする。

![](./img/promicropin.png)

### アクリルケース設計

* ケースもとりあえずアクリルで作ることにした。
* ケースもDXFで入稿できるみたいなのでkicadでそのまま作った。
	* SVGでもよさそうだがそもそもSVGで線幅を狭くするとinkscapeやchromeで表示したとき線が描画されない問題があった。
* アクリルは[工房Emerge+](https://www.emergeplus.jp/laser-cutting-service/)を使ってみることにした。
	* elecrowはウェブサイトの調子が良くないのか、そもそもサービス中止中なのか、  
	https://twitter.com/xcd0/status/1233658167684296704  
	のようにfalseとなっていた。
	* 遊舎工房は、キーボードのサイズが大きいので元のアクリル板が最低でもA3より大きな必要があり、  
	A5,A4,450 X 300と、450x300以外の選択肢がなく、このサイズでも2枚発注する必要がある。  
	そして150x300程度の余白ができてしまう。
	* Emarge+は600x300に対応しており、これだと１枚に収まる。なのでここにしてみた。
	* 遊舎工房とEmerge+はillustratorありきの体制で、すごくストレスフルであった。
	* inkscapeは線幅の問題で使えず、外形と内形を色を変えるとかレイヤーを変えるとか言った操作はillustratorがないと難しいというか不可能な作業であった。
	* 今回５個ほどソフトを試したが、どれも満たせずあきらめてillustratorの7日間仕様版を使った。
	* 次回はaiやsvgではなくDXFで入稿したい。
	* elecrow復活してほしい...
* データ蹴られるかと思ったがとりあえず通った。
* DXFもレイヤー分けていればよいらしい。

### プログラム作成

qmkでもよいがとりあえず動作確認にarduinoを使う。
以下を参考にarduino studioで書き込めるか調べる。
https://learn.sparkfun.com/tutorials/pro-micro--fio-v3-hookup-guide#installing-windows
https://learn.sparkfun.com/tutorials/pro-micro--fio-v3-hookup-guide/hardware-overview-pro-micro

![](https://make.kosakalab.com/.blog/wp-content/uploads/2016/07/Pro_Micro.png)

</details>

