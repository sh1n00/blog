+++ 
draft = false
date = 2023-04-20T01:23:43+09:00
title = "PIXIV SPRING BOOT CAMP202"
description = "インターン"
slug = ""
authors = ["sh1n00"]
tags = ["エンジニア", "学生", "インターン", "pixiv"]
categories = ["インターン"]
externalLink = ""
series = []
+++

## 初めに
[@sh1n00](https://twitter.com/Shinori0425)です！
今回は2023年3月にPIXIV SPRING BOOT CAMP2023に参加してきたのでその話をしようと思います。

## PIXIV SPRING BOOT CAMP2023とは
[PIXIV SPRING BOOT CAMP2023](https://internship.pixiv.co.jp/)は [ピクシブ](https://www.pixiv.net/)が毎年春に開催しているエンジニア学生向けインターンです。
全部で15コース程度しかない非常に選考倍率の高いインターンで毎年技術力の高いエンジニア学生が申し込んでいるイメージがあります。
2023年3月6日~3月15日の期間で10日間参加してきました。

## 応募のきっかけ
ピクシブというと百科事典やFANBOXなどエンタメ事業を中心に事業を展開しているイメージがあります。
また、エンジニアの技術力が非常に高く、毎年多くのレベルの高い学生がこのインターンに参加しているイメージがありました。

エンタメ領域に非常に興味がありゲームも好きという安直な動機からダメもとでデータ分析コースに申し込みました。

書類選考->コーディング&技術面接という流れで選考が進み、面接の2日後に結果が来ました。

説明しながらのコーディング面接は初めて少し不安もありましたが、得意なPythonということもありすらすら解けました。
面接を担当していたメンターのmytkさんに褒められてうれしくなった覚えがあります。

技術面接でも過去のコンペに出場した話を楽しく話すことができ全体的にすごく楽しかった面接でした。

結果が来てからはとても興味があったのですぐにインターン参加を決めました。

## インターン概要
データ分析コースではpixivで実際に運用されている広告における施策の提案を行いました。

## やったこと
やったことは運用型広告におけるクリエイティブ最適化です。

ピクシブではpixivで配信する広告をクライアントから金額を積み立ててもらうことで配信しています。
クライアントは広告の配信を積み立てた金額の分だけをpixivに要求することができます。
その結果pixivでクライアントの広告を表示できるという仕組みになっています。
実際にはクライアントは複数いるのでオークションと呼ばれる広告枠の競争が行われ、買った場合のみ課金されるという仕組みになっています。
クライアントがあらかじめ設定したクリエイティブ[^1]を競争で勝ち取った広告枠に対して表示されることで普段私たちが見る広告配信の仕組みが出来上がっています。

インターンではこのクリエイティブ選択の最適化の改善に取り組みました。
簡単に説明すると従来のpixivのクリエイティブ選択ではimpression数[^2]とclick数[^3]のみでクリエイティブ選択が行われていました。
このような広告におけるクリエイティブ選択では多腕バンディットアルゴリズムが用いられます。
多腕バンディットは強化学習の一種であり、複数の選択肢の中からよりよい選択を選ぶという問題を解くフレームワークです。
詳しくは<cite>[多腕バンディット問題に触れてみる](https://blog.brainpad.co.jp/entry/2021/12/07/110446)</cite>を参照してください。

このクリエイティブ選択ではユーザ情報を考慮していないためユーザ一人一人に最適なクリエイティブを選択できていないという問題点がありました。
そこで私はユーザ情報を考慮したクリエイティブ選択を行えるように文脈付きバンディットアルゴリズムの実装及び評価を行いました。
文脈付きバンディットアルゴリズムは<cite>[A Contextual-Bandit Approach to Personalized News Article Recommendation](https://arxiv.org/abs/1003.0146)</cite>の論文で紹介されている手法で年齢・性別・国籍などのユーザ情報の特徴量に最適になるようにパラメータの更新を行っていくアルゴリズムになります。

いくつかアルゴリズムがある中で私はLinUCBとLinThompsonSamplingの手法の実装を行いました。
LinUCBではαの値で探索と活用と呼ばれる行動を制御できる点、LinTSでは事前分布から事後分布をガウス分布的に導くことができる点が挙げられます。下記にそれぞれのアルゴリズムの疑似コードを載せます。

LinUCB
![linucb](/images/pixiv/linucb.png)

LinThompsonSampling
![lints](/images/pixiv/lints.png)

評価に関してはpixivの過去のログデータを用いて各クリエイティブごとのCTR[^4]値を算出し、各アルゴリズムごとのCTRの平均値を使用しました。

結果としてはCTRが従来の結果と比較すると数パーセント向上していることがわかりました。

## 印象に残ったこと
色々面白い企画や福利厚生があったのですがその中でも特に面白いなと思ったことを2つ挙げます。

一つ目はドリンクが飲み放題の福利厚生です。
会社に設置してある自販機に置いてある全てのドリンクが飲み放題です。
ドリンクにはお茶・野菜ジュース・リンゴジュース・コーヒーなど幅広いドリンクが置いてあります。
自分が行ったときにはエナジードリンクも置いてあって非常にわくわくしました。

二つ目はゲーム部があるところです。
意外とゲーム会社系の会社でもゲーム部があるところが少なく、非常に驚きました。
mytkさんにvalorant[^5]を誘われて参加したのですが他の様々な事業部の人たちも参加していてとても楽しかったです。

## 最後に
今回はPIXIV SPRING BOOT CAMP2023に参加してきました。

本当に楽しいインターンでした。
遊んでいるかのように仕事をできる環境で本当に働きやすかったです。

エンタメが好きな学生やこのインターンで圧倒的に技術力的に成長したい学生は是非参加してみてください！

[^1]: 漫画やサービスなどの画像です。
[^2]: 表示された広告数
[^3]: 表示された広告のクリック数
[^4]: Click Through Rate 表示された広告のうちどの程度クリックされたかの割合
[^5]: FPSゲーム