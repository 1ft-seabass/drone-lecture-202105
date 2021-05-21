# 1回目と2回目の間の宿題

![image](https://i.gyazo.com/8c395ddad36d9064e670af17868640a5.png)

より理解を深めるための宿題です。2回目がより楽しめます。

もし対応しなかったとしても2回目は問題なく受講できますが、ぜひチャレンジよろしくおねがいします！

## 1. AP モードでの接続を試してみましょう

![image](https://i.gyazo.com/36b6425469e2ef18be5f42f39807e573.png)

[第1回目の資料](chapter-01-01.md) の「Tello EDU の Node-RED から操作＆情報取得＋デモ（単純操作）」の「フローを動かしてみる」まで、試してみましょう。

## 2. 自分のPCの Node-RED にフローを読み込んで設定をしてみましょう

自分の PC の Node-RED に「遠隔で田中の家の Tello を動かすフロー」を読み込んでおきます。

### 画像を表示するノード node-red-contrib-image-output ノードを追加

画像を表示するノード node-red-contrib-image-output ノードを追加してみましょう。

![image](https://i.gyazo.com/2271eff3f05b9ba38e50d6e820dd27df.png)

右上のメニューを開きます。

![image](https://i.gyazo.com/b8db5a749429272b6235a0ecffdc11d6.png)

メニューから「パレットの管理」をクリック。

![image](https://i.gyazo.com/e2925fe3a3d0d91f090781899084dd36.png)

現在のノードが表示されるので、

![image](https://i.gyazo.com/fb7c3f5177824037c5a14905f6d0bb94.png)

ノードを追加のタブをクリックします。

![image](https://i.gyazo.com/417aebe2e3b97171e91678537f8b6246.png)

ノードを追加機能が表示されます。

![image](https://i.gyazo.com/fe0db25502255250ea5923575af72034.png)

ノードを検索書かれているエリアで検索できるので、

![image](https://i.gyazo.com/fb02568bbd1e757da835b91938c3d861.png)

node-red-contrib-image-output と入力して検索して、 node-red-contrib-image-output が出てきます。

![image](https://i.gyazo.com/e0828f744d38cc58f8daf935f7871e96.png)

ノード追加をクリックします。

![image](https://i.gyazo.com/090675c4500e96afbbe138ab41077311.png)

ダイアログが下りてくるので追加ボタンをクリックします。

![image](https://i.gyazo.com/45e03adcb75df2e225b22d8fa821624f.png)

しばらく待っているとインストールが完了します。

![image](https://i.gyazo.com/c6f1867b4aecd7cc5a022034409bebf8.png)

右側のエリアの中で image というノードが登場していたら成功です。

![image](https://i.gyazo.com/e887b76943d9deacc130400a9172c5c9.png)

### フローを読み込みます

1回目の授業の「Tello EDU の Node-RED から操作＆情報取得＋デモ（単純操作）」で行ったフローの読み込みと同じように、今回の「遠隔で田中の家の Tello を動かすフロー」を読み込みます。

```
[{"id":"91c655ef.4d0f38","type":"tab","label":"Remote Control Try","disabled":false,"info":""},{"id":"ad1b4e80.071c9","type":"mqtt in","z":"91c655ef.4d0f38","name":"","topic":"/get/image","qos":"2","datatype":"auto","broker":"77d1dda.a028924","nl":false,"rap":true,"rh":0,"x":620,"y":160,"wires":[["2d2fffd0.3c833","6fd80acf.53d404"]]},{"id":"64b587bc.970c08","type":"mqtt out","z":"91c655ef.4d0f38","name":"","topic":"/drone/control","qos":"","retain":"","respTopic":"","contentType":"","userProps":"","correl":"","expiry":"","broker":"77d1dda.a028924","x":440,"y":280,"wires":[]},{"id":"ef0d644d.588518","type":"inject","z":"91c655ef.4d0f38","name":"","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"capture","payloadType":"str","x":130,"y":160,"wires":[["64b587bc.970c08"]]},{"id":"2596275d.376c68","type":"inject","z":"91c655ef.4d0f38","name":"","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"cw 90","payloadType":"str","x":130,"y":220,"wires":[["64b587bc.970c08"]]},{"id":"2d2fffd0.3c833","type":"debug","z":"91c655ef.4d0f38","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":930,"y":160,"wires":[]},{"id":"6fd80acf.53d404","type":"image","z":"91c655ef.4d0f38","name":"","width":"320","data":"payload","dataType":"msg","thumbnail":false,"active":true,"pass":false,"outputs":0,"x":940,"y":220,"wires":[]},{"id":"206ec2c6.11be7e","type":"inject","z":"91c655ef.4d0f38","name":"","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"cw 180","payloadType":"str","x":130,"y":280,"wires":[["64b587bc.970c08"]]},{"id":"cb7bc109.cee1e","type":"inject","z":"91c655ef.4d0f38","name":"","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"cw 270","payloadType":"str","x":130,"y":340,"wires":[["64b587bc.970c08"]]},{"id":"629cab13.b11e14","type":"inject","z":"91c655ef.4d0f38","name":"","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"cw 360","payloadType":"str","x":130,"y":400,"wires":[["64b587bc.970c08"]]},{"id":"8d54a449.d9e0c8","type":"comment","z":"91c655ef.4d0f38","name":"ドローンから画像表示","info":"","x":660,"y":100,"wires":[]},{"id":"a9e98c8c.99fe9","type":"comment","z":"91c655ef.4d0f38","name":"ドローンへ命令","info":"","x":140,"y":100,"wires":[]},{"id":"77d1dda.a028924","type":"mqtt-broker","name":"driver.cloudmqtt.com","broker":"driver.cloudmqtt.com","port":"18715","clientid":"","usetls":false,"protocolVersion":"4","keepalive":"60","cleansession":true,"birthTopic":"","birthQos":"0","birthPayload":"","birthMsg":{},"closeTopic":"","closeQos":"0","closePayload":"","closeMsg":{},"willTopic":"","willQos":"0","willPayload":"","willMsg":{},"sessionExpiry":""}]
```

こちらを読み込むと「Remote Control Try」というタブが表示されます。

![image](https://i.gyazo.com/93deeb9c3a91787a677512e6be029e4f.png)

### MQTT のパスワードを設定

![image](https://i.gyazo.com/0725f7ac25da17df04a76af9a03a1213.png)

`/drone/control` MQTT ノードをダブルクリックして設定を開きます。

![image](https://i.gyazo.com/8e5cf1a28ac568a328864d914e9dfeee.png)

ノード設定の MQTT サーバー設定 `driver.cloudmqtt.com` の横にある編集ボタン（鉛筆ボタン）をクリックしてサーバー設定の詳細に行きます。

![image](https://i.gyazo.com/5e987cbc6530d4802ed66298344ada53.png)

接続設定は、すでにできています。セキュリティタブをクリックしてMQTT のパスワードを設定します。

![image](https://i.gyazo.com/ec75ea10272206180a8cf3587bb0fe34.png)

ユーザー名とパスワードの欄に以下を設定します。

* ユーザー名
  * kaishi-user
* パスワード
  * 0xkS9rRLq21R

![image](https://i.gyazo.com/f829c34cdca7adc4742264aa77110402.png)

設定できたら更新ボタンをクリックします。

![image](https://i.gyazo.com/60f937aef42ea1b0468a53ba6ca8b4e3.png)

サーバー設定から mqtt out ノード編集の画面まで戻るので完了をクリックします。

![image](https://i.gyazo.com/b0a3c835751a08c13a96f9b1a804c839.png)

右上のデプロイボタンをクリックして処理を確定します。

![image](https://i.gyazo.com/b1aa332b07a060aa22e972896f3a2fbf.png)

デプロイボタンが灰色になれば完了です。

### 動作チェック

![image](https://i.gyazo.com/7d5057eb4c2ec2adde9e591ebd1c5105.png)

設定がうまくできれば、こちらの2つの MQTT ノードが接続済みになります。

![image](https://i.gyazo.com/e8e384be7880d313799ef4bc02539edf.png)

こちらの capture という inject ノードをクリックします。

![image](https://i.gyazo.com/0d378842d30aadecde2b9197d3da6ca5.png)

`/get/image` の MQTT ノードが、こちらの仕組みからデータを受信して、このような画像が表示されたら設定がうまくできています。

![gif](https://i.gyazo.com/b544b0d7c731aafad3175cdd09a881ff.gif)

### 当日は

うまくいけば、ここに私（田中）の部屋のドローンが撮影して取得した画像が返ってきます。

## 3. 聞きたいことがあれば、質問よろしくです（あればでOK。質問必須ではないです。）

1回目の授業が終わった上で、もし質問したいことがあれば、以下のフォームからお気軽にご質問ください！

https://forms.gle/PUEbKt3zqDmn21WB8

↓↓↓　QRコード　↓↓↓

![Image from Gyazo](https://i.gyazo.com/cd06539f7a4d6dad2a62e553e8461060.png)