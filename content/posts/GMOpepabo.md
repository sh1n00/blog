+++ 
date = 2023-03-23
title = "GMOペパボ冬インターンに参加してきました！"
description = ""
slug = ""
authors = ["sh1n00"]
tags = ["エンジニア", "学生", "インターン", "GMO"]
categories = ["インターン"]
externalLink = ""
series = []
+++

## 初めに

こんにちはsh1n00です！今回は2023年2月6日～2月17日の期間に行われたGMOペパボのウィンターインターンに参加してきた話をしようと思います．

## 目次
- [初めに](#初めに)
- [応募のきっかけ](#応募のきっかけ)
- [選考フロー](#選考フロー)
- [インターン全体の流れ](#インターン全体の流れ)
- [インターンで開発したもの](#インターンで開発したもの)
   - [echoのミドルウェアとして実装](#echoのミドルウェアとして実装)
   - [redis_rateを用いたレートリミット制御](#redis_rateを用いたレートリミット制御)
   - [goroutineとチャネルを用いた並列化](#goroutineとチャネルを用いた並列化)
- [最後に](#最後に)


## 応募のきっかけ

GMOペパボのサマーインターンをブログからやっていることを知ったのがきっかけでした．
GMOと言えばインフラ領域の技術力が非常に高いイメージがありました．
また，扱っている業界がインターネットやインフラのイメージがあったのでプロダクト開発をしたい自分にとっては程遠いものだと思っていました．

しかしGMOペパボではインフラ領域だけでなくユーザよりのプロダクト開発を行っているのをブログ記事から知り，
今まで触ったことのない**インフラ部分に挑戦したい**＋**ユーザよりの開発を行いたい**と思い応募しました．


## 選考フロー

1. 書類選考
   - 今までの経歴やインターンにおいてやりたいことを簡単に書きました．
   - 分量自体はそこまで多くなかった気がします．

2. 面接
   - 開発経験や大学院の研究・インターンでどのようなことがやりたいかなどを聞かれました．
   - また申し込んだコースが技術基盤コースだったのでk8sやCI/CDなどのインフラ部分のスキルを簡単に聞かれました．

結果は面接した次の日くらいに来ました．
結果が来るまでがすごく早かったので驚いた覚えがあります．

## インターン全体の流れ

インターンは10日間行いました．
インターン生は自分を含めて2人だけの参加でした．
全体のスケジュールは基本的にリモートで開発を行い，最終日だけオフィスに出社して成果発表をするという流れでした．

最終日はメンターの方や人事の方とランチにピザを食べ，夜は全GMOグループが集まる[フクラス](https://blog.kushii.net/archives/2129726.html)(最近ではスティーブ・アオキさんが来たことで有名みたいです)という場所でご飯やお酒を楽しみました．

フクラスでのパーティはすごく楽しかったです．
コロナ前で中々できなかったお酒を飲みながらしゃべることが久々にできてやはり対面は良いなとすごく感じました．

## インターンで開発したもの
インターンでは「**技術基盤の観点から社内の課題を解決するようなものを作る**」というお題で開発を進めました．
開発するにあたっては下記のような流れで開発を行いました．

1. 現場エンジニアから課題ヒアリング
2. デザインドックの作成
3. 技術調査・システム設計
4. APIレートミットをハンドリングするミドルウェアの実装
5. 動作チェック

現場エンジニアからヒアリングの結果，とあるAPIのレートリミットを制御できるようなリバースプロキシの開発を行いました．
実装はGoとフレームワークのechoを用いて行い、echoのミドルウェアとして実装することで簡単にAPIレートリミットを制御できるようにしました.
開発したものはrate-limit-middlewareという名前のOSSとして[リポジトリ](https://github.com/pepabo/rate-limit-middleware)に公開されています．

このrate-limit-middlewareは主に3つの特徴があります．

1. echoのミドルウェアとして実装
2. redis_rateを用いたレートリミット制御
3. goroutineとchannelを用いた複数リクエストに対応

それぞれ簡単に説明しようと思います．

### echoのミドルウェアとして実装
echoのミドルウェアとして実装することで誰でも簡単にレートリミットを制御できるようにしました．
実際に使用感としてはGoのechoで立てたサーバにレートリミットを制御したい場合下記のようなコードを数行書くだけで使用できます．
`rateLimitTime`で1秒間あたり捌けるリクエスト数を指定できます。

```Go
func main() {
    e := echo.New()
    redisClient := redis.NewClient(&redis.Options{
	    // ex) "localhost:8080"
	    Addr: os.Getenv("REDIS_ADDR"),
    })
    rateLimitTime := 1
    e.Use(limit.RateLimitMiddleware(redisClient, rateLimitTime))
    e.Start(":8080")
}
```

### redis_rateを用いたレートリミット制御
レートリミットの制御には[redis_rate](https://github.com/go-redis/redis_rate)を使用しました．
このredis_rateはKVS(Key-Value store)のデータベースであるRedis(ネットワーク接続された永続化可能なインメモリデータベース)へのアクセスを制御することでレートリミットの制御を行えるOSSになっています．
redis_rateを用いることで簡単にレートリミットを行えることに実際にRedisの機能を使用できるところも特徴となっています．（今回は特に使用していないですが。。）

### goroutineとチャネルを用いた並列化
最後にgoroutineを用いて並列化を行うことで複数リクエストを同時に扱えるようにしました．
各リクエストごとにチャネルを生成し、FIFOのデータ構造にためていきます．
redis_rateのレートリミットに従いチャネルリストからチャネルを取り出し値を送信します．
値を送信することで受信側の処理が続行されリクエストの処理が行われるという流れになります．
またこの処理はgoroutineとして書くことで並列処理を可能にしています．

インフラ部分の知識はほぼ皆無でしたがメンターの方の支えもあり，なんとか最後動くものができて非常にうれしかったです．

## 最後に

非常に学びが多かったインターンでした．
特にインフラ部分では様々な人から勉強方法や業務内容を教えてもらうことで少しわかるようになりました．

また，OSSとしてソフトウェアを開発する大切さを知りました．
多くの人に使ってもらうにはどのようなインターフェースにすればよいかを考えるという経験はOSS開発ならではだと感じました．

2週間本当にお世話になりました！