---
layout: post
title: "Nuita通信 9月号"
subtitle: "今回の話は少し技術オタク向けになっているようです……"
date: 2020-09-27 18:00 +0900
background: '/img/posts/september.png'
---
いつも[Nuita](https://nuita.net) をご利用いただきありがとうございます。  
今月も1ヶ月に1度のお楽しみ、Nuita通信の時間がやってまいりました！一緒に今月のNuitaを振り返っていきましょう。  
とはいえ、今回の内容は少しばかり技術オタク向けのようですが……

#### imageproxyを導入しました
![投稿のイメージ画像]({{site.baseurl}}img/content/tags_on_nweet.png)

NuitaではユーザーのヌイートにURLが含まれていた場合、自動でリンク先のページを解析して情報を取得し、タイムラインにコンテンツの内容を表示しています(その処理は[panchira](https://github.com/nuita/panchira)として公開・開発されています)。

コンテンツのサムネイルを表示するためには、元ページの画像を取得・共有する必要があります。そこで直接元リンクの画像を埋め込んでしまうと、セキュリティ上の問題が発生するだけでなく、Nuitaへのアクセスがあるたびに元サイトの画像へのリクエストを送ることになり、元サイトのサーバーへの負担をかけてしまうことになります。

そこで、元サイトへの直接的なアクセスを防ぐために、これまで一時的にプロキシサーバーとして[camo](https://github.com/atmos/camo)を利用していました。これはいわば踏み台としての働きをなし、画像への直接的なリンクを避ける効果があり、[Togetter](https://qiita.com/MintoAoyama/items/6cd71b84e6225f86f819)などの様々なWebサービスで実際に用いられている（た?）ようです。  
一方で、キャッシュサーバーとしての機能は別途用意する必要がある上に、3年ほど前から更新が止まっているためか（最後の更新は2017年のようです）、時々うまく行かなくなることがあり、結果としてやむを得ず運用を最小限に留めなければいけないことがありました。

そこで、今月からの新しい試みとして、Nuitaでは[imageproxy](https://github.com/willnorris/imageproxy)を導入しました！  
これも先程のcamo同様プロキシサーバーとしての機能がありますが、同時にキャッシュサーバーとしての機能も兼ね備えていて、投稿された画像をメモリやストレージ上に一時保存することで元サイトへのアクセスを最小限に留めることができます。  
ユーザーがURLを投稿すると、Nuitaのサーバーのメモリ上にその画像がキャッシュされ、元サイトに一切アクセスすることなくURLのサムネイルが表示されます。また、キャッシュの領域としてはメモリ以外にAWS上のストレージが利用されることもありますが、その画像は直接閲覧できない形で保存されており、一定の期日が来ると自動的に削除されるようになっています。

![図]({{site.baseurl}}img/content/zu.png)
<center><small>図(お分かりいただけただろうか?)</small></center>

Nuitaでは、コンテンツのプラットフォームやクリエイターにとっての利益となるサービスを目指して今後も開発を進めて参ります。そのポリシーの詳細については、[こちらの記事](https://blog.nuita.net/2020/06/29/for-creators.html)をご確認いただければ幸いです。

#### Docker, Github Actionsを導入しました
Nuitaの開発はGithub上で進められており、[レポジトリ](https://github.com/nuita/nuita)上では有志の技術者たちがより良い射精報告のために日夜を問わず開発を進めています。  

しかし、ソフトウェア開発は見た目も地味な上に何の喜びも得られないことも多く、直接的な快感を得るためにNuitaより自分自身の身体を開発しがちになっていました。

そのため、Nuitaに充てられた数少ない限られた時間で最大の効果を得られるよう、Nuitaでは新しく**Docker**, そして**Github Actions**を導入しました！

**Docker**はコンテナ（詳しい人に怒られることを承知の上で書くと、一種の仮想マシンのようなものです）を簡単に立ち上げられるソフトウェアで、その設定ファイルを共有することで複数の開発者の間でも簡単に開発環境を共有できるようになります。

また、**Github Actions**はGithub上のコードに対して自動的に仮想環境で一連の命令を実行できる便利な機能で、これさえあれば人間が射精している間も機械にテスト・デプロイ等を行わせることができます。将来的にはデプロイの自動化も目標に入っていますが、現段階では出されたプルリクエストやマージされたコードに対する自動テストに用いられています。

![Github Actions]({{site.baseurl}}img/content/github_actions.png)

これらの新しい技術の導入により、Nuitaの開発はますます便利になったと確信しております！これを読んでくださっている方で、もし少しでもWebエンジニアリングの技術を少しでもお持ちでしたら、ぜひ一緒に楽しいNuitaの開発を進めていきませんか？


今回の新機能を使った感想など、もし何かございましたらお気軽に[twitter](https://twitter.com/nuita_net)や[GitHub](https://github.com/nuita/nuita)までお寄せください。
それでは、新しいタイムラインが加わってより便利になったNuitaで射精をお楽しみください！
