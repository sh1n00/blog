+++ 
date = 2023-03-18
title = "DMMGUILDインターンに参加してきた！"
description = "インターン"
slug = ""
authors = ["sh1n00"]
tags = ["エンジニア", "学生", "インターン", "DMM"]
categories = ["インターン"]
externalLink = ""
series = []
+++

## 初めに
[@sh1n00](https://twitter.com/Shinori0425)です！
今回は2022年9月にDMM GUILDに参加してきたのでその話をしようと思います。

## DMM GUILDとは
DMM GUILDは [DMM.com](https://ja.wikipedia.org/wiki/DMM.com)が主催しているエンジニア学生向け[インターン](https://dmm-corp.com/recruit/intern/engineer/guild/)です。
2022年は9月5日~9月16日の平日の2週間開催されました。

DMMの各事業部が抱えている課題から好きなものを選択し実装していくインターンです。
課題はフロントエンド・バックエンド・インフラ・CI/CDなど多種多様に渡るため各学生のスキルセットや経験に基づいて課題選択を行えます。
また、各課題にはポイントが振られており課題を解決することでポイントが獲得できます。
インターン最終日に得られたポイントをもとに賞金をゲットできる仕組みになっています！

私はリモートで参加させていただきました。
インターン期間中は実装以外にも社員の方との座談会・人事面談・ワークショップなど多くの楽しいイベントが盛りだくさんでした。

## 応募のきっかけ
逆求人からDMMさんでインターンを知ったことがきっかけでした。
自分と同じ大学の先輩が活躍されていると聞いてすごく興味が湧きそこからインターン選考に進むような形になりました。

書類選考スキップ -> 面談 -> 内定の選考フローでトントン拍子で参加が決まり増田。

## インターンの流れ
初日にPCのセットアップ・会社説明・インターン概要説明などを行い、開発自体は2日目から開始でした。
また同じインターン参加者の学生同士で4人ほどのチームを組みました。
チームごとに毎日朝会と夕会が行われ、その日の目標・その日困ったことや体調などを学生同士で共有しました。

最終日の13時くらいにコードフリーズが行われ、少し休憩したのちに結果発表という流れでした。

## やったこと
インターンではCI/CD・Docker・クラウド・モニタリング周りを中心に行いました。

- CircleCIを用いたテスト実行の並列化
- CircleCI上で動く[SchemaSpy](https://schemaspy.org)の更新
- CircleCIをGithubActionsに移行する
- Dockerのキャッシュ化
- Goアプリケーションに[DataDog](https://www.datadoghq.com/ja/)導入
- GCP -> AWSにデータを移行するためのシェルの実装
- 動画データの計測用シェルの開発
- 動画データをクラウドのあるサービスからあるサービスへ移行する際にかかるコストの概算見積もり

これまでの経験的にこれら分野はガッツリやる機会がなかったのですがこのインターンを通じてとても多く触ることができました。
未知の領域に飛び込むことを目的にしていたので**あえてやったことない課題を選択**してしっかりできるのか不安でしたが各事業部の方のサポートやチームメンバーの支えもありなんとかできました。

DMMさんは様々な事業を持っているため技術スタック多種多様に渡ります。
そのため課題もいろんなものがあり、触れる課題全てが新鮮で楽しかったです。

特に動画データの計測用シェル開発はとても楽しかったです。
実際にDMM.comのサービスで使用されている膨大なデータの容量を見たり、そのデータを移行するためにはどのようなサービスを使用すれば良いのかを考えたり、移行に伴うコストをいかに抑えるかを考えたりするのは動画サービスを古くからやっているDMMさんならではの経験だと思いました。

## 最後に
今回はDMM GUILDのインターンに参加してきました。

本当に楽しいインターンでした。DMMさんの良さを課題や様々なイベントから知ることができて本当に良かったです。

力をつけたい学生エンジニアの方はもちろんのことDMMさんの事業を知りたい・いろんな技術に触れてみたいなど考えている学生の方は是非参加してみてください！