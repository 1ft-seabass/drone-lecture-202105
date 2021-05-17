# 2回目レクチャー

1 回目の状況に応じて。

## 予定している内容

* 2回目　5月25日
  * Tello EDU の Node-RED から写真撮影＋デモ
  * こちらの Tello EDU を遠隔操作デモおよび仕組み紹介
  * 質疑応答 30分

## Tello EDU の Node-RED から写真撮影＋デモ

![image](https://i.gyazo.com/d31d35ec10e55979564d7575363c5a7c.png)

## こちらの Tello EDU を遠隔操作デモおよび仕組み紹介

![image](https://i.gyazo.com/d31d35ec10e55979564d7575363c5a7c.png)

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

## おわりに

→ [READMEに戻る](./README.md)