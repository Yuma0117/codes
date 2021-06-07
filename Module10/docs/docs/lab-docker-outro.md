# Docker Lab： おわりに

## ここまででできたこと

コンテナの概念に慣れるべく、Docker の基本的な取り扱いをざっくり総ざらいしました。

単一のコンテナを動かせるだけでなく、複数のコンテナを協調させられ、データの永続化もできるようになりました。さらに、既成のコンテナイメージが存在していなくても、自分のアプリケーションを自分だけのコンテナイメージにビルドして利用する方法を学習しました。

ここまでくれば、実際のところ、相当にいろいろなことがコンテナで実現できます。

今回は何らかのアプリケーションを動かすことを目的にしていましたが、例えば、**CentOS や Ubuntu のコンテナイメージ** も存在しており、うまく使えば開発作業やちょっとした動作確認でも柔軟に活用できます。

今日、コンテナを **なんとなくでもいいからとりあえず使えること** は、これからの時代、必ず武器にできるものです。すでにみなさんは、インタネットでおもしろそうなツールを見つけたときに、

- OS を汚しそうだからやめておこう
- コンテナで動かすっぽいけどよくわからないからやめておこう

……な理由であきらめる必要はなくなっています。GCP でインスタンスを作って、とにかく `docker run` してしまうところから、コンテナライフを始めていきましょう。

## 仮想マシンとコンテナ

コンテナは仮想マシンとよく比較されます。論理的に別の空間を作り出してその中で別のものを動かす、という概念レベルでは近しいものではありますが、実際の使い勝手や性能は大きく異なります。

仮想マシンでは、ハイパバイザが仮想ハードウェアを提供し、そこでゲスト OS を動かして、さらにその中でアプリケーションが動きます。最終的に動かしたいアプリケーションがどれだけ軽量なものであっても、そもそも OS を動かすためのリソースは必ず用意することになり、無駄が非常に多いことになります。

また、いわゆるマイクロサービスの概念を仮想マシンレベルで行おうとすると、そうした無駄が蓄積するばかりでなく、ネットワークの構成やストレージの構成も複雑化してしまうなど、根本的にデプロイが非常に大変です。例えばそのアプリケーション専用の OVF ファイルを作成するとしても、自動デプロイ向けの設計を作りこんだり、ゲスト OS レイヤのメンテナンスを考慮したり、大容量の OVF ファイルを大量に配信するインフラを整えたり、いくつものハードルがあります。

他方、コンテナは、理論上、オーバヘッドはほとんどありません。Linux のカーネルがもともと持っている論理的なリソース分割の仕組みをうまくまとめ上げ、あるプロセス専用の空間をコンテナホスト上に論理的に作り出してくれます。ゲスト OS レイヤが存在しないため非常に軽量で、圧倒的な速度で気軽に作ったり消したり作り直したりできます。

なにより、コンテナを取り巻くエコシステムの習熟が驚異的です。Docker Hub をはじめとするレジストリには膨大なコンテナイメージが集まっていますし、コンテナの利用を前提にしたアプリケーションの配布も一般化してきました。

開発環境もコンテナをうまく使うようになってきて、たとえ Windows 端末上であっても Docker を使って CentOS や Ubuntu 上での動作を確認できます。コンテナホストを汚すことなく疑似的に別の OS と同等の空間を作れるので、依存するパッケージがツール間で競合していたとしても、それぞれ用のコンテナを作ってあげれば、気にする必要もありません。Python でバージョンやモジュールを切り替えるために `pyenv` や `venv` でがんばらなくてもよくなってきています。