# 1回目レクチャー

## 予定している内容

* 1回目　5月18日
  * Tello EDU の基本操作＋α（カメラ撮影とかもできるよ）
  * Tello EDU の UDP プロトコルによる制御
  * Tello EDU の Node-RED から操作できる＋デモ（単純操作）
  * 質疑応答 30分

## Tello EDU の基本操作＋α（カメラ撮影とかもできるよ）

### できること

[Tello公式ウェブサイト \- Shenzhen Ryze Technology Co\.,Ltd\.](https://www.ryzerobotics.com/jp/tello-edu)

![image](https://i.gyazo.com/41b50edd017c5131feda598a203951db.png)

> たくさんの驚きがつまったTello EDUは、プログラミングも学べるので、教育にもぴったりなドローンです。Scratch／Python／Swiftといったプログラミング言語を簡単に学べます。アップグレードされたSDK 2.0を搭載するTello EDUは、さらに高度なコマンドと充実したデータインターフェースを備えています。Tello EDUは、DJIのフライトコントロール技術を採用し、EIS（電子式映像ブレ補正）にも対応。編隊飛行させるコマンドのコードを書いて、わくわくするAI機能を開発してみよう。Tello EDUで、プログラミングがもっと楽しく学べます！

## 単体で動かすならアプリもよい

![image](https://i.gyazo.com/242382ab4aa5108cbc6b25fb535659a7.png)

Tello のスマホアプリはあるので、これでどんな風に動かせるかを確認すると良いです。

![image](https://i.gyazo.com/e3143d5691b3afa4ee513c06e3ed7e73.png)

こんな UI でつなぐことができる。この場合、Tello EDU 本体がアクセスポイントになる AP モードが想定されています。

![image](https://i.gyazo.com/d0ee312935fb85c4b5bb0ff9fc12b241.png)

こんなかんじ。

### Wi-Fi のモード

Tello EDU は、2つの Wi-Fi モードがあります。

![image](https://i.gyazo.com/904e35920b2c7fc85892ce6d3c26aecc.png)

* AP モード
  * Tello EDU 自身に Wi-Fi アクセスポイントがあり、PC 側から Wi-Fi につないで Tello EDU の IP `192.168.10.1` に指示を出すタイプ
  * 指示の出し方は後述します
  * 1 x 1 の接続でネットワークが閉じてしまうので外部のデータの連携ができない

![image](https://i.gyazo.com/2c713ec5d86ce6ba419eb4706d815ff3.png)

* STATION モード
  * AP モードの状態で一度 Tello EDU に station mode 化の指示を Wi-Fi SSID / パスワードを知らせる形で発動します。
  * 以後は起動するたびに設定した Wi-Fi を探します。
  * station mode にしてから、自分自身がアクセスポイントになる状況にリセットする場合は、電源を長押しする
  * つないだ Wi-Fi ネットワークがインターネットに向けてもつながっていれば、さまざまなデータ連携ができる
  * 同じ Wi-Fi ネットワークに Tello EDU が複数台あっても IP アドレスさえわかれば複数同時制御も夢ではない（めっちゃがんばる）

STATION モードのくわしい設定のやりかたが、私のブログにあります。

* [Tello EDUをNode\-REDから station mode にして操作するメモ – 1ft\-seabass\.jp\.MEMO](https://www.1ft-seabass.jp/memo/2019/05/01/tello-edu-meets-nodered-setting-station-mode/)
  * station mode 化を参考にｓましょう。
  * Node-REDで動かすナレッジもあるが、ここは今日教える一歩手前の UDPノードで自前でつなげる」ナレッジなので参考程度に。

### Wi-Fi 接続はハマるときはハマるので注意

[Tello公式ウェブサイト \- Shenzhen Ryze Technology Co\.,Ltd\.](https://www.ryzerobotics.com/jp/tello-edu/specs) にもあるとりで、

![image](https://i.gyazo.com/be7bd417ed5d6b4dfcd0aa5704301205.png)

Wi-Fi は 2.4 GHz帯をつかっている。

経験上、以下を注意するといい。

* 対象の Wi-Fi ルーターが性能以上に機器がつながってないか
  * Tello EDU が後から入ると弾かれてしまう
  * 入ろうとしては入れないことを繰り返してゴリゴリ電池がなくなってしまう
* 対象の Wi-Fi ルーターが 5 GHz 優先にしていると 2.4 GHz帯につながらないケースがある
  * 2.4 GHz帯の機器は 2.4 GHz帯 を選ぶようにするなど設定を整える
* 2.4 GHz帯が苦手なことをしない
  * 電子レンジを動かして電波干渉・金属が多い場所で電波が乱れてしまうなど
* 動かしたい場所に、たくさんの Wi-Fi アクセスポイントがある
  * 複数人で、それぞれの手持ちの Tello EDU を自分のテザリングでつなぐと結構つながりにくくなるケースがある（あるあるネタ）

上記を踏まえて、自分の部屋でシンプルに試すなど、確実に動かす確証を持ってから色々と試しましょう。一気にやろうとするとハマります（自戒）。

ディスプレイがない機器で LED だけで「機器がうまく動いたかを確認する」のは苦労します。適宜、「このネットワークにちゃんとつながったかどうか」を確認するために Wi-Fi チェックツールを使いましょう。

* Android アプで私が使っているのは [Fing \(フィング\) \- ネットワークツール \- Google Play のアプリ](https://play.google.com/store/apps/details?id=com.overlook.android.fing&hl=ja&gl=US)
* iOS アプリでもありそう。
* ルーターの管理画面で接続チェックも有効。

以後、チェックしやすくするために、 MAC アドレスも覚えておきましょう。

### Tello EDU の UDP プロトコルによる制御

さて、実際の制御の話。

![image](https://i.gyazo.com/86f32d2d49201e08ae19f4bf2b6576cc.png)

[Tello公式ウェブサイト \- Shenzhen Ryze Technology Co\.,Ltd\.](https://www.ryzerobotics.com/jp/tello-edu/downloads)

こちらで SDK を確認しましょう。

![image](https://i.gyazo.com/65d83baef5c57fdca6f79b147068af28.png)

2021/5 時点でバージョンは 2.0 。

![image](https://i.gyazo.com/3616bcd03cc11469fbfde01fa62ce839.png)

PDF データです。

→ [PDF:SDK 2.0 User Guide](https://dl-cdn.ryzerobotics.com/downloads/Tello/Tello%20SDK%202.0%20User%20Guide.pdf)

![image](https://i.gyazo.com/97fbd355dbb8be994c5cfcf7918afa15.png)

* コマンドを送受信する
  * UDP receive & send
* Tello EDU の機器の状態を取得する
  * UDP receive
* ビデオストリームを取得する

![image](https://i.gyazo.com/02e208c832dd7d5028ed85eb50b2d245.png)

![image](https://i.gyazo.com/e289ebccd382ac1b9064d789b780193d.png)

いろいろなコマンド操作ができます。 station mode もある。PDFの中身も見てみましょう。

![image](https://i.gyazo.com/75abd79d50b04e10c59d3a6f9aa7338e.png)

こういう情報が受信できます。

![image](https://i.gyazo.com/9786e4cbff74feb709398dd4c4c645f4.png)

つまり、 UDP で指示が出せればどの言語でも操れます。

![image](https://i.gyazo.com/856fa76227ccf54afc514f49326f29a1.png)

操作するだけなら何でもよいが、操作するUIや状態をモニタリングするとなると、それなりに作るパワーが必要になる。

そういうとき、UIもサッと作れて、人と共有しても仕組みが分かりやすい Node-RED はおすすめ。

## Tello EDU の Node-RED から操作できる＋デモ（単純操作）

[node\-red\-contrib\-tello \(node\) \- Node\-RED](https://flows.nodered.org/node/node-red-contrib-tello)

最近は Node-RED で Tello を動かすノードが出てきています。三浦さんという IBM Champion が作ったノードです。

三浦さんの記事 → [Node\-REDでTelloを動かすためのノードを作って公開してみた \- KMiura's diary](https://supernove.hatenadiary.jp/entry/2020/12/16/004621)

私の UDP ノードでがんばるところが、良い感じにやってくれるノードです。

### Tello を AP モードで起動

AP モードは、Tello EDU 自身に Wi-Fi アクセスポイントがあり、PC 側から Wi-Fi につないで Tello EDU の IP `192.168.10.1` に指示を出すほうです。

2021/5 現在は、AP モード想定で node-red-contrib-tello ノードは動きます。

![image](https://i.gyazo.com/ebc36e3c4f5bb9bbe285030c28056c78.png)

### Node-RED を起動

Node-RED は手元のPCにインストールされている前提で進めます。

ターミナルで `node-red` と打って起動します。

![image](https://i.gyazo.com/103bacfba66675af01ea8c703200bb3a.png)

起動したら `http://localhost:1880/` と Chrome ブラウザにアドレス打ち込んで表示します。

### node-red-contrib-tello インストール

![image](https://i.gyazo.com/7b13264694d458df71dfb09c55667066.png)

右上のメニューから「パレットの管理」をクリック。

![image](https://i.gyazo.com/85d04e2bef80c9cf9321e228f6943dbd.png)

ユーザー設定ウィンドウが開いたら「パレット」をクリックし「ノードを追加」タブをクリックします。

![image](https://i.gyazo.com/42d939128dc556e2823ef429d5107450.png)

ノードを検索のところに node-red-contrib-tello と入力すると、候補が出てきます。出てきたらノードを追加ボタンを押します。

![image](https://i.gyazo.com/8b2ce97f5e9cfc185ad1e56abb786233.png)

通知が出るので追加をクリック。

![image](https://i.gyazo.com/3075720302a3c5401c03aeda73b0cf1f.png)

追加しました となればインストール成功です。

### 右のパレットに追加されます

![image](https://i.gyazo.com/a9708d247747e731f0e7b541d4deca7b.png)

## TIPS

### 電池すぐなくなるよ問題

![image](https://i.gyazo.com/508b762ce68f87299fb9b9b70167a533.png)

動かさなくても 15 分で電池なくなっちゃう感じ。

電池 50 % 以下は Wi-Fi 不安定になって制御不能になったりして遠隔制御バッドケースの体験にはうってつけだけど、こわすぎますね。

飛行させるともっと減りが早い。フレッシュに動いて正確に検証できるのは満充電の使用開始で5分程度と見ておくと良いです。（このあたりもうちょっと精密に検証するとイイかも）

![image](https://i.gyazo.com/91af99b52157f31192a50db101dc29cf.jpg)

この写真のように、ときどきバッテリーが膨らんで使えなくなるのも要注意。この場合、満充電のランプがついても、すぐ充電が再開してしまうループに入って、放置すると発火しそうな熱が出ます。

* 最近買ったけど便利
  * [Amazon \| 3\.8V 1100mah 1Sリチウム電池＋充電ケーブル TELLOに適応 四軸航空機スペアパーツ リモコンドローン \| Makerfire \| ドローン・マルチコプター用バッテリーパック](https://www.amazon.co.jp/gp/product/B08Z7Q9KPX/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)
  * はやく検証したいのに、充電のために本体に挿さないといけなくて占有するのがネックなので、こういう外部充電はありがたい
* ちなみに、しっかり複数充電するならこちららしい（未購入）
  * [Amazon\.co\.jp： Anbee Ryze Tello ドローン 用バッテリー充電ハブ 充電器: ホビー](https://www.amazon.co.jp/dp/B07GZDGHZ3/ref=sspa_dk_detail_8?psc=1&pd_rd_i=B07GZDGHZ3&pd_rd_w=EAtUS&pf_rd_p=37aaae60-66a0-4093-9681-4dcd496d4545&pd_rd_wg=fsm84&pf_rd_r=2HMXF74ZA6MQPDYZ8NR1&pd_rd_r=568a496c-ddb3-4ae4-b694-e764036e8bfc&spLa=ZW5jcnlwdGVkUXVhbGlmaWVyPUExUDJRT1I2OExZVFdVJmVuY3J5cHRlZElkPUEwNjMwNjU3M0NWNkcyU0g5UVBMMCZlbmNyeXB0ZWRBZElkPUEzTEtTTjRNU1FYQTNDJndpZGdldE5hbWU9c3BfZGV0YWlsJmFjdGlvbj1jbGlja1JlZGlyZWN0JmRvTm90TG9nQ2xpY2s9dHJ1ZQ==)

### カバーは大事

![image](https://i.gyazo.com/159b9ba157224ca03f4e29abba8d40a1.png)

上記の通り、制御不能はカジュアルにおきます。ケガの元なので。カバーは必須です。

ちなみに、制御不能になると、空中でどうにかしてつかまえて電源スイッチを押してOFFにするか電池切れまで待つという対応になります。

* [Amazon\.co\.jp： PGYTECH TELLO用 保護ケージ: カメラ](https://www.amazon.co.jp/Hensych-%E3%83%97%E3%83%AD%E3%83%86%E3%82%AF%E3%82%BF%E3%83%BC-%E3%82%AC%E3%83%BC%E3%83%89for-Tello-%E3%82%A2%E3%82%AF%E3%82%BB%E3%82%B5%E3%83%AA%E3%83%BC%E3%80%81%E3%83%96%E3%83%A9%E3%83%83%E3%82%AF/dp/B07F3WXPKF/ref=bmx_25?pd_rd_w=WqGrf&pf_rd_p=15227690-d528-45ba-946b-0553700173e0&pf_rd_r=ZZVRWZWG12FJXDZWM22K&pd_rd_r=41cebe08-0a06-461b-a402-df723f215939&pd_rd_wg=RPJVZ&pd_rd_i=B07F3WXPKF&psc=1)
  * スタンダードなカバー。私も持ってます。ただちょっとかさばるのと、歪むのがネック。
* [Amazon\.co\.jp： Cynova プロペラガード\(Tello 用\) \(グレー\): おもちゃ](https://www.amazon.co.jp/dp/B07NQ137BG/ref=sspa_dk_detail_6?psc=1&pd_rd_i=B07NQ137BG&pd_rd_w=EAtUS&pf_rd_p=37aaae60-66a0-4093-9681-4dcd496d4545&pd_rd_wg=fsm84&pf_rd_r=2HMXF74ZA6MQPDYZ8NR1&pd_rd_r=568a496c-ddb3-4ae4-b694-e764036e8bfc&smid=A1BA781B3TJGWB&spLa=ZW5jcnlwdGVkUXVhbGlmaWVyPUExUDJRT1I2OExZVFdVJmVuY3J5cHRlZElkPUEwNjMwNjU3M0NWNkcyU0g5UVBMMCZlbmNyeXB0ZWRBZElkPUFTQVo4UDhHUlNKTEgmd2lkZ2V0TmFtZT1zcF9kZXRhaWwmYWN0aW9uPWNsaWNrUmVkaXJlY3QmZG9Ob3RMb2dDbGljaz10cnVl)
  * かさばらないのが Good。つまり歪みにくい。

制御不能でなくても、私が経験した範囲だと、こういう危ないケースがあります。

* 外で風が吹いて自分に向かってきた
  * そよ風程度は耐えれるけど、それ以上は厳しい印象。制止しようと頑張るけど。
  * 基本、風の吹いてない室内で楽しむとイイと思います。
* 夏場にエアコンの下で離陸したらエアコンの風に流されて壁に激突してプロペラが折れる
  * 購入時に替えのプロペラはついているので事なきを得たが、そもそも減らしなくなかった！
  * 自分に飛んできたらと考えたら結構怖いと思い直した

## 質疑応答

## おわりに

→ [READMEに戻る](./README.md)