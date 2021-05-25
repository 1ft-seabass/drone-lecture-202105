# 2回目レクチャー

1 回目の状況に応じて。

今日はデモ中心に。

![image](https://i.gyazo.com/fb2869a76956fa7a4359787b2aba0bf9.jpg)

質問フォーム

https://forms.gle/PUEbKt3zqDmn21WB8

↓↓↓　QRコード　↓↓↓

![Image from Gyazo](https://i.gyazo.com/cd06539f7a4d6dad2a62e553e8461060.png)

## 予定している内容

* 2回目　5月25日
  * Node-REDのダッシュボードUIで操作
  * Tello EDU の Node-RED から写真撮影＋デモ
  * こちらの Tello EDU を遠隔操作デモおよび仕組み紹介
  * 質疑応答 30分

## Node-REDのダッシュボードUIで操作

![image](https://i.gyazo.com/af159145ba4c505975ea0175fd084f64.png)

このようなフロー。「ダッシュボードからUIで操作」「ドローン命令の結果受信」というフローが加わっています。

### node-red-dashboard ノードのインストール

![image](https://i.gyazo.com/85d04e2bef80c9cf9321e228f6943dbd.png)

右上のメニューから「パレットの管理」をクリック。

![image](https://i.gyazo.com/7b13264694d458df71dfb09c55667066.png)

ユーザー設定ウィンドウが開いたら「パレット」をクリックし「ノードを追加」タブをクリックします。

![image](https://i.gyazo.com/373caae1cfec4ef31955f9490e6f4521.png)

ノードを検索のところに node-red-dashboard と入力すると、候補が出てきます。出てきたらノードを追加ボタンを押します。

![image](https://i.gyazo.com/42291f006d9517d8bb8d07719676f4eb.png)

通知が出るので追加をクリック。

![image](https://i.gyazo.com/1c89611eecf5bb13bd3723eab3fec472.png)

追加しました となればインストール成功です。

![image](https://i.gyazo.com/dd43dc47696d4a493e2de4b4b0af8c62.png)

右側のパレットに dashboard が登場します。

![image](https://i.gyazo.com/f69fd3e54cd9662f4ec1e93f1c57e38c.png)

こんな感じ。

### フローを読み込みます

![image](https://i.gyazo.com/996d09ec0eaa719ac91e96b24a9c510a.png)

右上のメニューを表示します。

![image](https://i.gyazo.com/f0422d24736f2355c8cd16e19e29acd9.png)

こちらに「読み込み」という機能をクリックします。

![image](https://i.gyazo.com/d0724448942eadce5960d0b43f1b3c12.png)

クリップボードをクリックします。


```
[{"id":"645ad3ef.c49a3c","type":"tab","label":"Tello First UI","disabled":false,"info":""},{"id":"daf1acc8.e3a83","type":"udp out","z":"645ad3ef.c49a3c","name":"","addr":"192.168.10.1","iface":"","port":"8889","ipv":"udp4","outport":"45678","base64":false,"multicast":"false","x":590,"y":120,"wires":[]},{"id":"ccdac9db.62a198","type":"inject","z":"645ad3ef.c49a3c","name":"","repeat":"","crontab":"","once":false,"onceDelay":"","topic":"","payload":"takeoff","payloadType":"str","x":250,"y":400,"wires":[["daf1acc8.e3a83"]]},{"id":"5280888a.054ce8","type":"inject","z":"645ad3ef.c49a3c","name":"","repeat":"","crontab":"","once":false,"onceDelay":"","topic":"","payload":"land","payloadType":"str","x":250,"y":440,"wires":[["daf1acc8.e3a83"]]},{"id":"1dc8dd08.07ddf3","type":"inject","z":"645ad3ef.c49a3c","name":"","repeat":"","crontab":"","once":false,"onceDelay":"","topic":"","payload":"command","payloadType":"str","x":240,"y":80,"wires":[["daf1acc8.e3a83"]]},{"id":"c6d11713.6bf958","type":"comment","z":"645ad3ef.c49a3c","name":"離着陸操作","info":"","x":240,"y":360,"wires":[]},{"id":"79f59946.5e8838","type":"udp in","z":"645ad3ef.c49a3c","name":"","iface":"","port":"45678","ipv":"udp4","multicast":"false","group":"","datatype":"utf8","x":540,"y":240,"wires":[["70b0cf9f.b78bb","41512754.56d1e8"]]},{"id":"70b0cf9f.b78bb","type":"debug","z":"645ad3ef.c49a3c","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"payload","x":690,"y":240,"wires":[]},{"id":"189ab224.a725ce","type":"comment","z":"645ad3ef.c49a3c","name":"ドローン命令の結果受信","info":"","x":590,"y":200,"wires":[]},{"id":"6e654a0d.2fa1f4","type":"inject","z":"645ad3ef.c49a3c","name":"","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":"","topic":"","payload":"battery?","payloadType":"str","x":240,"y":160,"wires":[["daf1acc8.e3a83"]]},{"id":"eadc1b38.5cd4c8","type":"comment","z":"645ad3ef.c49a3c","name":"コマンド開始","info":"","x":230,"y":40,"wires":[]},{"id":"2aa75f5d.11f0b","type":"comment","z":"645ad3ef.c49a3c","name":"バッテリー残量問い合わせ","info":"","x":190,"y":120,"wires":[]},{"id":"4ae0cf15.ecf5b","type":"comment","z":"645ad3ef.c49a3c","name":"ドローンへ命令送信","info":"","x":570,"y":80,"wires":[]},{"id":"51b00cb.b4265f4","type":"comment","z":"645ad3ef.c49a3c","name":"飛行時間（秒）問い合わせ","info":"","x":190,"y":200,"wires":[]},{"id":"cf100b02.08b638","type":"inject","z":"645ad3ef.c49a3c","name":"","repeat":"","crontab":"","once":false,"onceDelay":"","topic":"","payload":"time?","payloadType":"str","x":250,"y":240,"wires":[["daf1acc8.e3a83"]]},{"id":"6f3f534a.f93c0c","type":"inject","z":"645ad3ef.c49a3c","name":"","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":"","topic":"","payload":"height?","payloadType":"str","x":250,"y":320,"wires":[["daf1acc8.e3a83"]]},{"id":"335ed47.329412c","type":"comment","z":"645ad3ef.c49a3c","name":"飛行高度（cm）問い合わせ","info":"","x":180,"y":280,"wires":[]},{"id":"dd406f62.b88e6","type":"ui_button","z":"645ad3ef.c49a3c","name":"","group":"451274e2.41bb6c","order":1,"width":0,"height":0,"passthru":false,"label":"command","tooltip":"","color":"","bgcolor":"","icon":"","payload":"command","payloadType":"str","topic":"","x":120,"y":520,"wires":[["a7b9a78d.51b568"]]},{"id":"a94ee8ee.ccbc98","type":"ui_button","z":"645ad3ef.c49a3c","name":"","group":"451274e2.41bb6c","order":2,"width":0,"height":0,"passthru":false,"label":"takeoff","tooltip":"","color":"","bgcolor":"","icon":"","payload":"takeoff","payloadType":"str","topic":"","x":110,"y":600,"wires":[["a7b9a78d.51b568"]]},{"id":"41d3aa6c.785be4","type":"ui_button","z":"645ad3ef.c49a3c","name":"","group":"451274e2.41bb6c","order":4,"width":0,"height":0,"passthru":false,"label":"land","tooltip":"","color":"","bgcolor":"","icon":"","payload":"land","payloadType":"str","topic":"","x":110,"y":640,"wires":[["a7b9a78d.51b568"]]},{"id":"41512754.56d1e8","type":"ui_text","z":"645ad3ef.c49a3c","group":"451274e2.41bb6c","order":8,"width":0,"height":0,"name":"","label":"Tello response","format":"{{msg.payload}}","layout":"col-center","x":720,"y":340,"wires":[]},{"id":"c64af58d.caa6c8","type":"comment","z":"645ad3ef.c49a3c","name":"ダッシュボードからUIで指示","info":"","x":180,"y":480,"wires":[]},{"id":"92bdfe2b.ba209","type":"comment","z":"645ad3ef.c49a3c","name":"ダッシュボードで応答表示","info":"","x":750,"y":300,"wires":[]},{"id":"25423c23.2c54a4","type":"ui_button","z":"645ad3ef.c49a3c","name":"","group":"451274e2.41bb6c","order":5,"width":0,"height":0,"passthru":false,"label":"battery?","tooltip":"","color":"","bgcolor":"","icon":"","payload":"battery?","payloadType":"str","topic":"","topicType":"str","x":120,"y":680,"wires":[["a7b9a78d.51b568"]]},{"id":"3e8b70b8.c2784","type":"ui_button","z":"645ad3ef.c49a3c","name":"","group":"451274e2.41bb6c","order":6,"width":0,"height":0,"passthru":false,"label":"height?","tooltip":"","color":"","bgcolor":"","icon":"","payload":"height?","payloadType":"str","topic":"","topicType":"str","x":120,"y":720,"wires":[["a7b9a78d.51b568"]]},{"id":"a7b9a78d.51b568","type":"function","z":"645ad3ef.c49a3c","name":"<HUB>","func":"\nreturn msg;","outputs":1,"noerr":0,"initialize":"","finalize":"","libs":[],"x":340,"y":580,"wires":[["daf1acc8.e3a83","3903b7ea.d1a9d8"]]},{"id":"3a10d992.bd1ed6","type":"ui_button","z":"645ad3ef.c49a3c","name":"","group":"451274e2.41bb6c","order":3,"width":0,"height":0,"passthru":false,"label":"cw 90","tooltip":"","color":"","bgcolor":"","icon":"","payload":"cw 90","payloadType":"str","topic":"","topicType":"str","x":110,"y":560,"wires":[["a7b9a78d.51b568"]]},{"id":"3903b7ea.d1a9d8","type":"ui_text","z":"645ad3ef.c49a3c","group":"451274e2.41bb6c","order":7,"width":0,"height":0,"name":"","label":"Tello current command","format":"{{msg.payload}}","layout":"col-center","x":560,"y":580,"wires":[]},{"id":"451274e2.41bb6c","type":"ui_group","name":"デフォルト","tab":"fbbccbb5.ed3b48","order":1,"disp":false,"width":"6","collapse":false},{"id":"fbbccbb5.ed3b48","type":"ui_tab","name":"ホーム","icon":"dashboard","disabled":false,"hidden":false}]
```

こちらをまずコピーして先ほどの画面に戻ります。

![image](https://i.gyazo.com/112ec952e4b46c3eedf3f1eafd0fdac6.png)

テキストエリアにペーストして、読み込みボタンが押せるようになるのでクリックして読み込みます！

![image](https://i.gyazo.com/10850014dbd6872a7a00160a625d6b88.png)

「Tello First UI」というタブが読み込まれるのでクリックして確認します。

![image](https://i.gyazo.com/af159145ba4c505975ea0175fd084f64.png)

このようなフローが確認できました。

### Tello EDU を AP モードで起動

では Tello EDU につないでみましょう。

AP モードは、Tello EDU 自身に Wi-Fi アクセスポイントがあり、PC 側から Wi-Fi につないで Tello EDU の IP `192.168.10.1` に指示を出すほうです。

### Tello EDU のアクセスポイントにつなげる

Wi-Fi を探して接続します。

![image](https://i.gyazo.com/ebc36e3c4f5bb9bbe285030c28056c78.png)

### Dashboard を表示する

![image](https://i.gyazo.com/0ee45f79e508891c76b01c23a3157743.png)

右上のメニュー > 表示 > Dashboard をクリック。

![image](https://i.gyazo.com/2591c7f1216713013f77b2e906edd50a.png)

サイドメニューを見てみるとダッシュボードの情報が表示されています。

![image](https://i.gyazo.com/b124c03268e9ddf78fd400a028768d2c.png)

このようになっています。

![image](https://i.gyazo.com/c9068f1bcd1736953524a5b0b22fee4d.png)

このアイコンをクリックするとダッシュボードが表示されます。

![image](https://i.gyazo.com/d9af030f2c90aeb9d4780f187d550cd3.png)

表示されました。

### デモ：操作してみる

![image](https://i.gyazo.com/f74090abe747b565fa17734d0a47dd92.jpg)

* command を押して操作可能にする
* takeoff で離陸
* cw 90 で時計回り90度に回転
* land で着陸
* height? で高度情報が Tello response に返答されることを確認
* battery? でバッテリー情報が Tello response に返答されることを確認

を行います。まず、動画で様子を見せつつ。デモします。

## Tello EDU の Node-RED から写真撮影＋デモ

よりディープな Tello の Node-RED フローはこちら。

[johnwalicki/Node\-RED\-Tello\-Control: Node\-RED flows to control the Ryze Tello Drone](https://github.com/johnwalicki/Node-RED-Tello-Control)

![image](https://i.gyazo.com/2a1665010fb52604484dffbd70669cc4.png)

ここを紐解けば Tello のほとんどの動作が体験できます。

![image](https://i.gyazo.com/829af48374d759c110efd73042588e26.png)

チュートリアルも分かりやすいです。

### 今日は写真撮影部分を抽出

[PART7 Take pictures](https://github.com/johnwalicki/Node-RED-Tello-Control/blob/main/docs/PART7.md) のフロー( [part7_solution.json](https://github.com/johnwalicki/Node-RED-Tello-Control/blob/main/flows/solutions/part7_solution.json) )をベースに写真撮影部分だけ抽出してます。

### node-red-node-base64 ノードのインストール

解析した画像のバッファを base64 にしてダッシュボートに表示するためにnode-red-node-base64 ノードのインストールします。

![image](https://i.gyazo.com/aadd962018a0b34e3109798a69dec49d.png)

### node-red-contrib-image-output ノードをインストール

バッファをワークスペース上で画像表示するためにnode-red-contrib-image-output ノードもインストールします。もし宿題をしてインストール済みの人もいればそのままでOK。

![image](https://i.gyazo.com/fb02568bbd1e757da835b91938c3d861.png)

### フローを読み込みます

以下のフローを読み込みます。

```
[{"id":"865602f6.dc2338","type":"tab","label":"Tello Picture Dash Kaishi","disabled":false,"info":""},{"id":"5b0a7d4e.258d2c","type":"udp out","z":"865602f6.dc2338","name":"","addr":"192.168.10.1","iface":"","port":"8889","ipv":"udp4","outport":"52955","base64":false,"multicast":"false","x":1010,"y":200,"wires":[]},{"id":"d8f0f1c9.9d5b6","type":"function","z":"865602f6.dc2338","name":"Tello Send Cmd","func":"var TBL_CRC16 = [\n\t\t\t0x0000, 0x1189, 0x2312, 0x329b, 0x4624, 0x57ad, 0x6536, 0x74bf, 0x8c48, 0x9dc1, 0xaf5a, 0xbed3, 0xca6c, 0xdbe5, 0xe97e, 0xf8f7,\n\t\t\t0x1081, 0x0108, 0x3393, 0x221a, 0x56a5, 0x472c, 0x75b7, 0x643e, 0x9cc9, 0x8d40, 0xbfdb, 0xae52, 0xdaed, 0xcb64, 0xf9ff, 0xe876,\n\t\t\t0x2102, 0x308b, 0x0210, 0x1399, 0x6726, 0x76af, 0x4434, 0x55bd, 0xad4a, 0xbcc3, 0x8e58, 0x9fd1, 0xeb6e, 0xfae7, 0xc87c, 0xd9f5,\n\t\t\t0x3183, 0x200a, 0x1291, 0x0318, 0x77a7, 0x662e, 0x54b5, 0x453c, 0xbdcb, 0xac42, 0x9ed9, 0x8f50, 0xfbef, 0xea66, 0xd8fd, 0xc974,\n\t\t\t0x4204, 0x538d, 0x6116, 0x709f, 0x0420, 0x15a9, 0x2732, 0x36bb, 0xce4c, 0xdfc5, 0xed5e, 0xfcd7, 0x8868, 0x99e1, 0xab7a, 0xbaf3,\n\t\t\t0x5285, 0x430c, 0x7197, 0x601e, 0x14a1, 0x0528, 0x37b3, 0x263a, 0xdecd, 0xcf44, 0xfddf, 0xec56, 0x98e9, 0x8960, 0xbbfb, 0xaa72,\n\t\t\t0x6306, 0x728f, 0x4014, 0x519d, 0x2522, 0x34ab, 0x0630, 0x17b9, 0xef4e, 0xfec7, 0xcc5c, 0xddd5, 0xa96a, 0xb8e3, 0x8a78, 0x9bf1,\n\t\t\t0x7387, 0x620e, 0x5095, 0x411c, 0x35a3, 0x242a, 0x16b1, 0x0738, 0xffcf, 0xee46, 0xdcdd, 0xcd54, 0xb9eb, 0xa862, 0x9af9, 0x8b70,\n\t\t\t0x8408, 0x9581, 0xa71a, 0xb693, 0xc22c, 0xd3a5, 0xe13e, 0xf0b7, 0x0840, 0x19c9, 0x2b52, 0x3adb, 0x4e64, 0x5fed, 0x6d76, 0x7cff,\n\t\t\t0x9489, 0x8500, 0xb79b, 0xa612, 0xd2ad, 0xc324, 0xf1bf, 0xe036, 0x18c1, 0x0948, 0x3bd3, 0x2a5a, 0x5ee5, 0x4f6c, 0x7df7, 0x6c7e,\n\t\t\t0xa50a, 0xb483, 0x8618, 0x9791, 0xe32e, 0xf2a7, 0xc03c, 0xd1b5, 0x2942, 0x38cb, 0x0a50, 0x1bd9, 0x6f66, 0x7eef, 0x4c74, 0x5dfd,\n\t\t\t0xb58b, 0xa402, 0x9699, 0x8710, 0xf3af, 0xe226, 0xd0bd, 0xc134, 0x39c3, 0x284a, 0x1ad1, 0x0b58, 0x7fe7, 0x6e6e, 0x5cf5, 0x4d7c,\n\t\t\t0xc60c, 0xd785, 0xe51e, 0xf497, 0x8028, 0x91a1, 0xa33a, 0xb2b3, 0x4a44, 0x5bcd, 0x6956, 0x78df, 0x0c60, 0x1de9, 0x2f72, 0x3efb,\n\t\t\t0xd68d, 0xc704, 0xf59f, 0xe416, 0x90a9, 0x8120, 0xb3bb, 0xa232, 0x5ac5, 0x4b4c, 0x79d7, 0x685e, 0x1ce1, 0x0d68, 0x3ff3, 0x2e7a,\n\t\t\t0xe70e, 0xf687, 0xc41c, 0xd595, 0xa12a, 0xb0a3, 0x8238, 0x93b1, 0x6b46, 0x7acf, 0x4854, 0x59dd, 0x2d62, 0x3ceb, 0x0e70, 0x1ff9,\n\t\t\t0xf78f, 0xe606, 0xd49d, 0xc514, 0xb1ab, 0xa022, 0x92b9, 0x8330, 0x7bc7, 0x6a4e, 0x58d5, 0x495c, 0x3de3, 0x2c6a, 0x1ef1, 0x0f78\n\t\t];\n\t\t\nvar TBL_CRC8 = [\n\t\t\t0x00, 0x5e, 0xbc, 0xe2, 0x61, 0x3f, 0xdd, 0x83, 0xc2, 0x9c, 0x7e, 0x20, 0xa3, 0xfd, 0x1f, 0x41,\n\t\t\t0x9d, 0xc3, 0x21, 0x7f, 0xfc, 0xa2, 0x40, 0x1e, 0x5f, 0x01, 0xe3, 0xbd, 0x3e, 0x60, 0x82, 0xdc,\n\t\t\t0x23, 0x7d, 0x9f, 0xc1, 0x42, 0x1c, 0xfe, 0xa0, 0xe1, 0xbf, 0x5d, 0x03, 0x80, 0xde, 0x3c, 0x62,\n\t\t\t0xbe, 0xe0, 0x02, 0x5c, 0xdf, 0x81, 0x63, 0x3d, 0x7c, 0x22, 0xc0, 0x9e, 0x1d, 0x43, 0xa1, 0xff,\n\t\t\t0x46, 0x18, 0xfa, 0xa4, 0x27, 0x79, 0x9b, 0xc5, 0x84, 0xda, 0x38, 0x66, 0xe5, 0xbb, 0x59, 0x07,\n\t\t\t0xdb, 0x85, 0x67, 0x39, 0xba, 0xe4, 0x06, 0x58, 0x19, 0x47, 0xa5, 0xfb, 0x78, 0x26, 0xc4, 0x9a,\n\t\t\t0x65, 0x3b, 0xd9, 0x87, 0x04, 0x5a, 0xb8, 0xe6, 0xa7, 0xf9, 0x1b, 0x45, 0xc6, 0x98, 0x7a, 0x24,\n\t\t\t0xf8, 0xa6, 0x44, 0x1a, 0x99, 0xc7, 0x25, 0x7b, 0x3a, 0x64, 0x86, 0xd8, 0x5b, 0x05, 0xe7, 0xb9,\n\t\t\t0x8c, 0xd2, 0x30, 0x6e, 0xed, 0xb3, 0x51, 0x0f, 0x4e, 0x10, 0xf2, 0xac, 0x2f, 0x71, 0x93, 0xcd,\n\t\t\t0x11, 0x4f, 0xad, 0xf3, 0x70, 0x2e, 0xcc, 0x92, 0xd3, 0x8d, 0x6f, 0x31, 0xb2, 0xec, 0x0e, 0x50,\n\t\t\t0xaf, 0xf1, 0x13, 0x4d, 0xce, 0x90, 0x72, 0x2c, 0x6d, 0x33, 0xd1, 0x8f, 0x0c, 0x52, 0xb0, 0xee,\n\t\t\t0x32, 0x6c, 0x8e, 0xd0, 0x53, 0x0d, 0xef, 0xb1, 0xf0, 0xae, 0x4c, 0x12, 0x91, 0xcf, 0x2d, 0x73,\n\t\t\t0xca, 0x94, 0x76, 0x28, 0xab, 0xf5, 0x17, 0x49, 0x08, 0x56, 0xb4, 0xea, 0x69, 0x37, 0xd5, 0x8b,\n\t\t\t0x57, 0x09, 0xeb, 0xb5, 0x36, 0x68, 0x8a, 0xd4, 0x95, 0xcb, 0x29, 0x77, 0xf4, 0xaa, 0x48, 0x16,\n\t\t\t0xe9, 0xb7, 0x55, 0x0b, 0x88, 0xd6, 0x34, 0x6a, 0x2b, 0x75, 0x97, 0xc9, 0x4a, 0x14, 0xf6, 0xa8,\n\t\t\t0x74, 0x2a, 0xc8, 0x96, 0x15, 0x4b, 0xa9, 0xf7, 0xb6, 0xe8, 0x0a, 0x54, 0xd7, 0x89, 0x6b, 0x35,\n\t\t]\n\n\t\t\nfunction _calcCRC16 (buf, size) {\n\t\tvar i = 0 ;\n\t\tvar seed = 0x3692 ;\n\t\twhile (size > 0) {\n\t\t\tseed = TBL_CRC16[(seed ^ buf[i]) & 0xff] ^ (seed >> 8)\n\t\t\ti++ ;\n\t\t\tsize-- ;\n\t\t} \n\t\treturn seed ;\n\t}\n\nfunction _calcCRC8 (buf, size) {\n\t\tvar i = 0 ;\n\t\tvar seed = 0x77 ;\n\t\twhile (size > 0) {\n\t\t\tseed =  TBL_CRC8[(seed ^ buf[i]) & 0xff]\n\t\t\ti++ ;\n\t\t\tsize-- ;\n\t\t}\n\t\treturn seed ;\n\t}\n\n\t\nfunction buildPacket(pacType, cmdID, seq, data) {\n\t\tvar size = 11 + (data?data.length:0);\n\t\tvar bb = Buffer.alloc(size)\n\t\tvar packetTypeInfo = 0x40 | ((pacType & 0x07) <<3);\n\t\tbb.writeUInt8(0xCC,0)\n\t\tbb.writeUInt8((size << 3) & 0xFF ,1)\n\t\tbb.writeUInt8((size >> 5) & 0xFF ,2)\n\t\n    \tvar crc8 = _calcCRC8([...bb], 3)\n\t\tbb.writeUInt8(crc8,3);\n\t\tbb.writeUInt8(packetTypeInfo,4);\n\t\tbb.writeUInt16LE(cmdID,5);\n\t\tbb.writeUInt16LE(seq,7);\n\t\t//console.log(\"DBG\", data, len);\n\t\tif (data) {\n\t\t\tfor (var i=0; i<data.length; i++) {\n\t\t\t\tbb.writeUInt8(data[i], 9+i);\n\t\t\t}\n\t\t}\n\t\tvar crc16 = _calcCRC16([...bb], size - 2);\n\t\tbb.writeUInt16LE(crc16, size-2) ;\n\t\treturn bb ;\n\t}\n\t\nvar seqID = global.get(\"seqID\");\nif (\"undefined\" === typeof seqID) {\n    seqID = -1 ;\n}\nseqID++ ;\nglobal.set(\"seqID\", seqID);\n\n\nvar out = buildPacket(msg.payload.packType, msg.payload.TelloCmdId, seqID, msg.payload.data);\nmsg.payload = out;\nmsg.hex = out.toString('hex');\n\nreturn msg;","outputs":1,"noerr":0,"x":780,"y":200,"wires":[["5b0a7d4e.258d2c"]]},{"id":"cb99267f.854da8","type":"change","z":"865602f6.dc2338","name":"TELLO_CMD_TAKEPIC - 48","rules":[{"t":"set","p":"payload","pt":"msg","to":"{\"TelloCmdId\":48,\"packType\":5}","tot":"json"}],"action":"","property":"","from":"","to":"","reg":false,"x":540,"y":200,"wires":[["d8f0f1c9.9d5b6"]]},{"id":"d61e7a62.713d18","type":"inject","z":"865602f6.dc2338","name":"TELLO_CMD_TAKEPIC","repeat":"","crontab":"","once":false,"onceDelay":"","topic":"","payload":"TELLO_CMD_TAKEPIC","payloadType":"str","x":230,"y":200,"wires":[["cb99267f.854da8"]]},{"id":"4918976f.81511","type":"udp in","z":"865602f6.dc2338","name":"","iface":"","port":"52955","ipv":"udp4","multicast":"false","group":"","datatype":"buffer","x":200,"y":380,"wires":[["a3804454.755fb8"]]},{"id":"a3804454.755fb8","type":"function","z":"865602f6.dc2338","name":"parse incoming messages","func":"//var TELLO_CMD_ALT_LIMIT = 4182;\n//var TELLO_CMD_LIGHT_STRENGTH = 53;\n//var TELLO_CMD_LOW_BATT_THRESHOLD = 4183;\n//var TELLO_CMD_STATUS = 86;\n//var TELLO_CMD_LOG_HEADER_WRITE = 4176;\n//var TELLO_CMD_LOG_DATA_WRITE = 4177;\n\nvar TELLO_msgDoConnect           = 0x0001 // 1\nvar TELLO_msgConnected           = 0x0002 // 2\nvar TELLO_msgQuerySSID           = 0x0011 // 17\nvar TELLO_msgSetSSID             = 0x0012 // 18\nvar TELLO_msgQuerySSIDPass       = 0x0013 // 19\nvar TELLO_msgSetSSIDPass         = 0x0014 // 20\nvar TELLO_msgQueryWifiRegion     = 0x0015 // 21\nvar TELLO_msgSetWifiRegion       = 0x0016 // 22\nvar TELLO_msgWifiStrength        = 0x001a // 26\nvar TELLO_msgSetVideoBitrate     = 0x0020 // 32\nvar TELLO_msgSetDynAdjRate       = 0x0021 // 33\nvar TELLO_msgEisSetting          = 0x0024 // 36\nvar TELLO_msgQueryVideoSPSPPS    = 0x0025 // 37\nvar TELLO_msgQueryVideoBitrate   = 0x0028 // 40\nvar TELLO_msgDoTakePic           = 0x0030 // 48\nvar TELLO_msgSwitchPicVideo      = 0x0031 // 49\nvar TELLO_msgDoStartRec          = 0x0032 // 50\nvar TELLO_msgExposureVals        = 0x0034 // 52 (Get or set?)\nvar TELLO_msgLightStrength       = 0x0035 // 53\nvar TELLO_msgQueryJPEGQuality    = 0x0037 // 55\nvar TELLO_msgError1              = 0x0043 // 67\nvar TELLO_msgError2              = 0x0044 // 68\nvar TELLO_msgQueryVersion        = 0x0045 // 69\nvar TELLO_msgSetDateTime         = 0x0046 // 70\nvar TELLO_msgQueryActivationTime = 0x0047 // 71\nvar TELLO_msgQueryLoaderVersion  = 0x0049 // 73\nvar TELLO_msgSetStick            = 0x0050 // 80\nvar TELLO_msgDoTakeoff           = 0x0054 // 84\nvar TELLO_msgDoLand              = 0x0055 // 85\nvar TELLO_msgFlightStatus        = 0x0056 // 86\nvar TELLO_msgSetHeightLimit      = 0x0058 // 88\nvar TELLO_msgDoFlip              = 0x005c // 92\nvar TELLO_msgDoThrowTakeoff      = 0x005d // 93\nvar TELLO_msgDoPalmLand          = 0x005e // 94\nvar TELLO_msgFileSize            = 0x0062 // 98\nvar TELLO_msgFileData            = 0x0063 // 99\nvar TELLO_msgFileDone            = 0x0064 // 100\nvar TELLO_msgDoSmartVideo        = 0x0080 // 128\nvar TELLO_msgSmartVideoStatus    = 0x0081 // 129\nvar TELLO_msgLogHeader           = 0x1050 // 4176\nvar TELLO_msgLogData             = 0x1051 // 4177\nvar TELLO_msgLogConfig           = 0x1052 // 4178\nvar TELLO_msgDoBounce            = 0x1053 // 4179\nvar TELLO_msgDoCalibration       = 0x1054 // 4180\nvar TELLO_msgSetLowBattThresh    = 0x1055 // 4181\nvar TELLO_msgQueryHeightLimit    = 0x1056 // 4182\nvar TELLO_msgQueryLowBattThresh  = 0x1057 // 4183\nvar TELLO_msgSetAttitude         = 0x1058 // 4184\nvar TELLO_msgQueryAttitude       = 0x1059 // 4185\n\nvar seqID ;\nvar pacType;\n\nfunction parsePacket (bb) {\n    var ret = {};\n\tvar size = bb.length;\n\tvar payload = bb.slice(9,size);\n\tvar dataSize = 0;\n\tvar cmdID    = 0;\n\n\tif (bb.length >= 11) {\n\t\tvar mark = bb.readUInt8(0);\n\t\tif (mark == 0xCC) {\t// start of packet\n\t\t    size      = bb.readUInt16LE(1) >> 3;\n\t\t    var crc8  = bb.readUInt8(3);\n\t\t    pacType   = bb.readUInt8(4);\n\t\t    cmdID     = bb.readUInt16LE(5);\n\t\t    seqID     = bb.readUInt16LE(7);\n\t        dataSize  = size - 11;\n\t        var data  = false;\n\t        if (dataSize > 0) {\n\t            data = bb.slice(9, size-2);\n\t        }\n\t        var crc16 = bb.readUInt16LE(size - 2);\n\t        \n\t        ret.cmd = cmdID;\n\t        ret.seq = seqID;\n\t        ret.pacType= pacType;\n\t        ret.dataSize = dataSize;\n\t        ret.data = data;\n\t\t} else {\n\t\t    ret = bb.toString();\n\t\t}\n\t} else {\n\t    ret = bb.toString();\n\t}\n\treturn ret;\n}\n\t\nmsg.payload = parsePacket(msg.payload);\nif (msg.payload.cmd) {\n    var tstatus = global.get(\"tellomsg\") | {};\n    tstatus.cmdID  = msg.payload.cmd;\n    tstatus.seqID  = msg.payload.seq;\n    tstatus.pacType= msg.payload.pacType;\n    global.set(\"tellomsg\",tstatus);\n}\nreturn msg;","outputs":1,"noerr":0,"x":400,"y":380,"wires":[["8df549.78793ab8"]]},{"id":"9203aa1b.6b2c6","type":"debug","z":"865602f6.dc2338","name":"Otherwise","active":false,"tosidebar":true,"console":false,"tostatus":false,"complete":"true","x":780,"y":480,"wires":[]},{"id":"a1f903c9.9ca2d","type":"comment","z":"865602f6.dc2338","name":"Receive Return Strings","info":"","x":240,"y":340,"wires":[]},{"id":"43ff55ff.8f10e4","type":"function","z":"865602f6.dc2338","name":"Send Con_Req","func":"videoPort = 6038;\nmsg = {};\nmsg.payload = new Buffer(\"conn_req:lh\");\nmsg.payload[9] = videoPort & 0xFF;\nmsg.payload[10] = (videoPort >> 8) & 0xFF;\nglobal.set(\"seqID\", -1);\nreturn msg;","outputs":1,"noerr":0,"x":780,"y":160,"wires":[["5b0a7d4e.258d2c"]]},{"id":"4603c589.6ed634","type":"inject","z":"865602f6.dc2338","name":"TELLO_LOW_LEVEL_CONNECT","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":"","topic":"","payload":"true","payloadType":"bool","x":260,"y":120,"wires":[["43ff55ff.8f10e4"]]},{"id":"8df549.78793ab8","type":"switch","z":"865602f6.dc2338","name":"","property":"payload.cmd","propertyType":"msg","rules":[{"t":"eq","v":"86","vt":"num"},{"t":"eq","v":"26","vt":"num"},{"t":"eq","v":"53","vt":"num"},{"t":"eq","v":"4176","vt":"num"},{"t":"eq","v":"98","vt":"num"},{"t":"eq","v":"99","vt":"num"},{"t":"eq","v":"48","vt":"num"},{"t":"else"}],"checkall":"true","repair":false,"outputs":8,"x":590,"y":380,"wires":[[],[],[],[],["3f41ea5b.baa436"],["2b644e1c.14938a"],["ef29b4f9.1ae9"],["9203aa1b.6b2c6"]],"outputLabels":["FlightStatus","WifiStrength","LightStrength","LogHeader","FileSize","FileData","DoTakePic","otherwise"]},{"id":"ef29b4f9.1ae9","type":"debug","z":"865602f6.dc2338","name":"DoTakePic","active":false,"tosidebar":true,"console":false,"tostatus":false,"complete":"true","x":790,"y":440,"wires":[]},{"id":"aa8ecfdc.aa0128","type":"link in","z":"865602f6.dc2338","name":"TELLO-SND_LOW_LEVEL_CMD","links":["d9406e9d.313378"],"x":635,"y":240,"wires":[["d8f0f1c9.9d5b6"]]},{"id":"3f41ea5b.baa436","type":"function","z":"865602f6.dc2338","name":"unpack FileSize message","func":"// Ignore if not from drone\nif (0x80 & msg.payload.pacType) {\n    msg.payload.fileType = msg.payload.data.readInt8(0);\n    msg.payload.fileSize = msg.payload.data.readInt32LE(1);\n    msg.payload.fileID = msg.payload.data.readInt16LE(5);\n    flow.set(\"file\" +  msg.payload.fileID, {\"size\" : msg.payload.fileSize, \n                                \"receivedBytes\" : 0,\n                                \"imageBytes\" : Buffer.alloc(msg.payload.fileSize),\n                                \"pieces\" : {}\n                            });\n    return msg;\n}","outputs":1,"noerr":0,"x":830,"y":360,"wires":[["c6da806c.43e838"]]},{"id":"c6da806c.43e838","type":"change","z":"865602f6.dc2338","name":"Ack FileSizeMsg","rules":[{"t":"set","p":"payload","pt":"msg","to":"{\"TelloCmdId\":98,\"data\":[0],\"packType\":2}","tot":"json"}],"action":"","property":"","from":"","to":"","reg":false,"x":1060,"y":360,"wires":[["d9406e9d.313378"]]},{"id":"d9406e9d.313378","type":"link out","z":"865602f6.dc2338","name":"","links":["aa8ecfdc.aa0128"],"x":1215,"y":380,"wires":[]},{"id":"2b644e1c.14938a","type":"function","z":"865602f6.dc2338","name":"Unpack FileData message","func":"var fileID = msg.payload.data.readInt16LE(0);\nvar filePiece = msg.payload.data.readInt32LE(2);\nvar fileChunk = msg.payload.data.readInt32LE(6);\nvar chunkLen = msg.payload.data.readInt16LE(10);\nvar file = flow.get(\"file\" + fileID);\nif ((!file) || (\"undefined\" === typeof file.receivedBytes)) {\n    msg.payload = {};\n} else {\n    msg.payload.data.copy(file.imageBytes, 1024*fileChunk, 12);\n    msg.payload = {};\n    msg.payload.unpackedHeader = {\"ID\" : fileID, \n                \"piece\" : filePiece,\n                \"chunk\" : fileChunk,\n                \"len\" : chunkLen\n    };\n    if (file.pieces[filePiece]) {\n        if (!file.pieces[filePiece].includes(fileChunk)) {\n            file.pieces[filePiece].push(fileChunk);\n            file.receivedBytes += chunkLen;\n            if (8 == file.pieces[filePiece].length) {\n                msg.payload.TelloCmdId = 99;\n                msg.payload.packType = 2;\n                msg.payload.data = Buffer.alloc(7);\n                msg.payload.data.writeInt8(0, 0);\n                msg.payload.data.writeInt16LE(fileID, 1);\n                msg.payload.data.writeInt32LE(filePiece, 3);\n            }\n        }\n    } else {\n        msg.payload = {};\n        msg.payload.unpackedHeader = {\"ID\" : fileID, \n                \"piece\" : filePiece,\n                \"chunk\" : fileChunk,\n                \"len\" : chunkLen\n        };\n        file.pieces[filePiece] = [fileChunk];\n        file.receivedBytes += chunkLen;\n    }\n    msg.payload.unpackedHeader.receivedBytes = file.receivedBytes;\n    \n    if (file.receivedBytes == file.size) {\n        flow.set ([\"file\" + fileID], null);\n        msg.payload.TelloCmdId = 99;\n        msg.payload.packType = 2;\n        msg.payload.data = Buffer.alloc(7);\n        msg.payload.data.writeInt8(1, 0);\n        msg.payload.data.writeInt16LE(fileID, 1);\n        msg.payload.data.writeInt32LE(filePiece, 3);\n        \n        msg1 = {\"payload\" : {}};\n        msg1.payload.TelloCmdId = 100;\n        msg1.payload.packType = 1;\n        return [[msg, msg1], {\"payload\":file.imageBytes}];\n    } else if (msg.payload.TelloCmdId) {\n        flow.set(\"file\" + fileID, file);\n        return [msg, null];\n    } else {\n        flow.set(\"file\" + fileID, file);\n        return [null, null];\n    }\n}","outputs":2,"noerr":0,"x":840,"y":400,"wires":[["d9406e9d.313378"],["7deed9e0.4b1ec"]],"outputLabels":["completedPieceAck","Received image"]},{"id":"a40bb8cc.dae26","type":"ui_template","z":"865602f6.dc2338","group":"230dc716.b089d","name":"Photo","order":2,"width":"12","height":"9","format":"<div ng-bind-html></div>\n<img width=\"300\" height=\"300\" alt=\"Watson Image\" src=\"data:image/jpg;base64,{{msg.payload}}\"/>","storeOutMessages":false,"fwdInMessages":false,"templateScope":"local","x":790,"y":600,"wires":[[]]},{"id":"6376d619.fd6d28","type":"change","z":"865602f6.dc2338","name":"","rules":[{"t":"set","p":"template","pt":"msg","to":"<div ng-bind-html></div> <img width=\"300\" height=\"300\" alt=\"Watson Image\" src=\"data:image/jpg;base64,{{msg.payload}}\"/>","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":590,"y":600,"wires":[["a40bb8cc.dae26"]]},{"id":"eda2f263.8283c8","type":"ui_button","z":"865602f6.dc2338","name":"","group":"230dc716.b089d","order":1,"width":0,"height":0,"passthru":false,"label":"Take Picture","color":"","bgcolor":"","icon":"","payload":"","payloadType":"str","topic":"","x":290,"y":240,"wires":[["cb99267f.854da8"]]},{"id":"7deed9e0.4b1ec","type":"link out","z":"865602f6.dc2338","name":"Picture Arrived","links":["d64a7534.24e1e"],"x":1215,"y":420,"wires":[]},{"id":"d64a7534.24e1e","type":"link in","z":"865602f6.dc2338","name":"Picture Processing","links":["7deed9e0.4b1ec"],"x":155,"y":620,"wires":[["22e77fcb.046f6","7570cb2b.c4b584"]]},{"id":"22e77fcb.046f6","type":"base64","z":"865602f6.dc2338","name":"Encode","x":340,"y":600,"wires":[["6376d619.fd6d28"]]},{"id":"83aee586.ee0908","type":"comment","z":"865602f6.dc2338","name":"1. まず LOW_LEVEL でつなぐ","info":"","x":220,"y":80,"wires":[]},{"id":"5242f593.db917c","type":"comment","z":"865602f6.dc2338","name":"2. 撮影コマンド","info":"","x":180,"y":160,"wires":[]},{"id":"7570cb2b.c4b584","type":"image","z":"865602f6.dc2338","name":"","width":160,"data":"payload","dataType":"msg","thumbnail":false,"active":true,"pass":false,"outputs":0,"x":360,"y":680,"wires":[]},{"id":"e9578e68.1e116","type":"comment","z":"865602f6.dc2338","name":"3-1. 撮影バッファを base64 に変換してダッシュボードに表示","info":"","x":500,"y":560,"wires":[]},{"id":"ebd5a8dd.eab858","type":"comment","z":"865602f6.dc2338","name":"3-2. 撮影バッファを image-output ノードでこのワークスペース上に表示","info":"","x":540,"y":640,"wires":[]},{"id":"230dc716.b089d","type":"ui_group","name":"Drone Image","tab":"192b6a33.f665ce","order":1,"disp":true,"width":"12","collapse":false},{"id":"192b6a33.f665ce","type":"ui_tab","name":"Tello Camera","icon":"fa-tachometer","order":5}]
```

こちらを読み込みます。

![image](https://i.gyazo.com/7319fd0e453f72a6e50774850d4ed78b.png)

「Tello Picture Dash Kaishi」というタブが読み込まれるのでクリックして確認します。

![image](https://i.gyazo.com/38fc05034161b8433cff93698bb510c2.png)

このようなフローを確認できます。

### デモ：操作してみる

![image](https://i.gyazo.com/d54eed803bf2f2c58696f4f5d4829b05.png)

![image](https://i.gyazo.com/5a3347522b3657760b72fb6c3e8d2d91.png)

* まず LOW_LEVEL でつなぐ
  * 一度このコマンドでつながないと撮影できないので注意
* 撮影コマンドをクリック
* 撮影バッファを base64 に変換してダッシュボードに表示
* 撮影バッファを image-output ノードでこのワークスペース上に表示

をデモします。

## こちらの Tello EDU を遠隔操作デモおよび仕組み紹介

### こんな仕組み

今日の授業のためだけに建てた [CloudMQTT](https://www.cloudmqtt.com/) の MQTT ブローカーを経由して、みなさんの設定した宿題フローから操作ができます。

![image](https://i.gyazo.com/d38dbfc7d0118d836c5809fcf5dfd451.png)

MQTT ブローカーを経由して時計回りの回転を送ったり。

![image](https://i.gyazo.com/09380cf974eaaa94e5f12b54ba45767e.png)

キャプチャの指示をして写真撮影を行って

![image](https://i.gyazo.com/bd56dc7a250522816e5bbf4466f8bd60.png)

折り返しで画像データを送ることで遠隔写真撮影ができたり。

### ※状況に応じて、宿題フローを行わなくてもいじれる別のアプローチをするかもしれません。

![image](https://i.gyazo.com/669ae4754c77ec2bd194802061b1b042.png)

[IBM Cloud で Node\-RED セットアップ \(2021年4月\) \- Qiita](https://qiita.com/Kakimoty_Field/items/ed30531445cafcb30a63) を参考に作った Node-RED を使える環境で作られたダッシュボードをみんなで操作してみる。

![image](https://i.gyazo.com/3182dbfcd80bd156baecdebdef031d67.png)

動作イメージ。

### station モード にする

「家の中のドローンを動かしつつ」「外部ネットワーク経由でMQTTにデータを送る」という内外のネットワークに対してアクションを行うので、いよいよ。

![image](https://i.gyazo.com/2c713ec5d86ce6ba419eb4706d815ff3.png)

* AP モードの状態で一度 Tello EDU に station mode 化の指示を Wi-Fi SSID / パスワードを知らせる形で発動します。
* 以後は起動するたびに設定した Wi-Fi を探します。
* station mode にしてから、自分自身がアクセスポイントになる状況にリセットする場合は、電源を長押しする
* つないだ Wi-Fi ネットワークがインターネットに向けてもつながっていれば、さまざまなデータ連携ができる

STATION モードのくわしい設定のやりかたが、私のブログにあります。

* [Tello EDUをNode\-REDから station mode にして操作するメモ – 1ft\-seabass\.jp\.MEMO](https://www.1ft-seabass.jp/memo/2019/05/01/tello-edu-meets-nodered-setting-station-mode/)
  * station mode 化を参考にしましょう。
  * Node-REDで動かすナレッジもあるが、ここは今日教える一歩手前の UDPノードで自前でつなげる」ナレッジなので参考程度に。

### デモ：通常操作の API で cw （時計回り回転）の遠隔操作のデモ

宿題のみなさんのフローから送ってみる or 以下のダッシュボードUIで操作

https://node-red-ibm-champ-event-tseigo-2021.mybluemix.net/ui/#!/0

![image](https://i.gyazo.com/34fad98c059b45f88d4bf19054cd001c.png)

### デモ：遠隔の写真撮影

* 低レベル API の写真撮影 → できたら
  * [Low\-Level Protocol](https://tellopilots.com/wiki/protocol/) をベースにしているので、通常の UDP で文字列を送る操作と共存できない
  * 低レベル API での操作を併用すれば色々操作できる
    * 今日はやらない
* この場合はビデオストリーム＋通常操作の API で切り取ったほうがいいかもしれないですね

https://node-red-ibm-champ-event-tseigo-2021.mybluemix.net/ui/#!/1

![image](https://i.gyazo.com/f8ffbf1d5b2fd8966600f79f9fb2f6f7.png)

## TIPS

### いろいろなアプローチで組めるとベター

個人的には、Node-RED を触れて便利さも体験しつつも、Node.js や Python のように素のプログラムを書いて、色々な大変さ（UIを作る・非同期処理・UDPプロトコルなど）も知っていると、細かく拡張するときに自由度が高まります。

例としては、Python でも指示が出せると Python は機械学習と親和性が高いので、一部任せられたり。UDPの基礎の仕組みが分かっていれば 3D に強い Unity で使う言語である C# でも実装できたりします。

例 : [HoloLens1 UWPでTello EDUとUDP連携をして操作するメモ – 1ft\-seabass\.jp\.MEMO](https://www.1ft-seabass.jp/memo/2019/05/04/hololens1-meets-tello-edu/)

### 参考文献

私の記事で「トイドローン Tello をビジュアルプログラミングツール Node-REDで制御してみよう」という連載があります。参考にしてみてください。

※本特別授業は、以下を元に Node-RED 1.3 に合わせて再構成したものです。

* 第1回 準備編
  * https://flxy.jp/article/2756
* 第2回 離着陸編
  * https://flxy.jp/article/2903
* 第3回 ドローン状態確認編
  * https://flxy.jp/article/2963
* 最終回 操縦編
  * https://flxy.jp/article/3103

## 質疑応答

なんでも、どうぞ！

![image](https://i.gyazo.com/ac1fa5944bb2f544f6ce895ac365439f.png)

質問フォーム

https://forms.gle/PUEbKt3zqDmn21WB8

↓↓↓　QRコード　↓↓↓

![Image from Gyazo](https://i.gyazo.com/cd06539f7a4d6dad2a62e553e8461060.png)

## おわりに

→ [READMEに戻る](./README.md)