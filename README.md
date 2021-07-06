# 職務経歴書

## 個人データ

* 遠山 篤史(とおやま あつし)
* [GitHub](https://github.com/Toasa)
* [Twitter](https://twitter.com/toasa_3)
* [Blog](https://toasa3.hatenablog.com/)

## 職務概要

新卒で株式会社EWMファクトリーに入社後、CMSや自社製のPHPフレームワークを使用しWebサイトの改修・保守業務を担当しました。
二社目はコネクトフリー株式会社で、Zen言語を使用したぜい弱性解析ツール、ライブラリの開発を行いました。
三社目は株式会社イーゲルで、ネットワークのシミュレータを開発しています。

## 職務経歴

### 株式会社イーゲル (2020年12月 ~ 現在)

### 試験的ネットワークプロトコルのアプリケーション開発 (2021年4月 ~ 現在)

  - 開発環境
    - C, Ubuntu 20.04
  - ポイント
    - [DPDK](https://www.dpdk.org/) 使った試験的ネットワークプロトコルの実装
    - ビルドツールに Meson/ninja を使用
        - ユニットテストも Meson を使用
  - 2名/メンバー

### 試験的ネットワークプロトコルのシミュレータ開発 (2020年12月 ~ 2021年4月)

  - 開発環境
    - C++, Ubuntu 20.04
  - ポイント
    - [ns-3](https://www.nsnam.org/) のネットワークプロトコルのモデル実装
        - アプリケーション層 (NVMe-oF) とトランスポート層 (RDMA, UDP) の分離を意識した開発
        - Roce 層の再送処理
    - Wireshark での pcap 解析
    - NVMe, NVMe-oF の習熟
    - RDMA の習熟
  - 2名/メンバー

### コネクトフリー株式会社 (2019年11月 ~ 2020年11月)

#### LLVM-IRを解析するぜい弱性検出ツールの開発 (2019年11月 ~ 2020年11月)

  - 開発環境
    - Zen
  - ポイント
    - C言語のぜい弱性に関する知識
    - LLVM-IR の習熟
    - C-FFI の作成
    - アジャイル開発の経験
    - テスト駆動開発
  - 4名/メンバー

#### カレンダー、time 標準ライブラリの作成 (2020年8月)

  - 開発環境
    - Zen
  - ポイント
    - Unix時間、うるう年、うるう秒の仕様把握
    - 範囲外時刻のエラー処理
    - テスト駆動開発
  - 2名/メンバー

### 株式会社EWMファクトリー (2018年4月 ~ 2019年9月)

#### 複数Webサイトの保守業務 (2019年4月 ~ 2019年9月)

  - 開発環境
    - macOS, CMS(Movable Type 6,7)
  - ポイント
    - CMSのバージョンアップ
    - テストの作成
  - 2名/メンバー

#### ニュース系Webサイトの改修業務 (2019年1月 ~ 2019年4月)

  - 開発環境
    - macOS, CMS(Movable Type6)
  - ポイント
    - 動的な記事生成の処理時間を短縮
      - 全記事のループをハッシュ化し計算量を`O(n)`から`O(1)`に短縮
      - 記事更新時に生成不要な広告をcronを用いて別途定期的に再生成する。（アクセスの少ない深夜に行う）
  - 3名/メンバー

#### 官庁系Webサイトの保守業務 (2018年6月 ~ 2018年12月)

  - 開発環境
    - macOS, 自社製のPHPフレームワーク
  - ポイント
    - MVCモデルの習熟

## 言語経験

|言語|業務|業務外|
|---|---|---|
|PHP|半年|-|
|Zen|1年|-|
|C|-|3年|
|Go|-|1年|
|Python3|-|半年|

## 自己PR

### 技能

言語処理系は業務外において自作し、基本的な理論から実装まで幅広い知識を持っています。

### 資格

- TOEIC 850 点 (受験日: 2021年6月20日午後)

### 性格

転職先は Web系、言語処理系、ネットワーク系とコンピュータ・サイエンスの分野が変化しています。
未経験の分野であっても好奇心を持って勉強し、挑戦することができます。

気になったことを根気強く調べ、時間をかけて理解を進めることが好きです。
例えばOSのinitプロセスの始まりに興味をもち、xv6というOSのinitプロセスについてカーネル/VM探検隊@関西 10回目（[スライド](https://speakerdeck.com/toasa/xv6-initpurosesu-kotohazime), [ビデオ](https://youtu.be/J-pF4fg3r04?t=1750)）で発表しました。

予定を立てコツコツとタスクをこなすことが得意です。他者の気持ちを汲み、チームの一員としてプロジェクトを進めることができます。

## 業務外/個人活動

低レイヤ技術（コンパイラ、OS）、計算理論（オートマトン、計算可能性、計算複雑性）に興味があり勉強を進めています。
コンパイラ、インタプリタなどの言語処理系は主にCコンパイラ、Lispインタプリタなどを実装し学習しています。
計算理論は "Introduction to the theory of computation" から学び、実装として正規表現エンジンを作成しました。

### 言語処理系

|レポジトリ名|言語|説明|
|---|---|---|
|[2020cc](https://github.com/Toasa/2020cc)|C|Cコンパイラ|
|[tisp](https://github.com/Toasa/tisp)|C|Lispインタプリタ|
|[regexp](https://github.com/Toasa/regexp)|Go|正規表現エンジン。構文木の出力、状態遷移図の出力、正規表現の受理判定を実装。|
|[tgoc](https://github.com/Toasa/tgoc)|Go|Goコンパイラ|
|[g9cc](https://github.com/Toasa/g9cc)|Go|Cコンパイラ|
|[monkey by rust](https://github.com/Toasa/monkey_by_rust)|Rust|Go で書かれた[Monkey](https://monkeylang.org/) インタプリタを Rust で書き直した|
|[tbf](https://github.com/Toasa/bf_interpreter)|C|Brainf*ckインタプリタ|

### ゲーム

|レポジトリ名|言語|説明|
|---|---|---|
|[getris](https://github.com/Toasa/getris)|Go|テトリス|
|[game of life](https://github.com/Toasa/game_of_life)|Go|ライフゲーム|

### 深層学習

|レポジトリ名|言語|説明|
|---|---|---|
|[zelkova](https://github.com/Toasa/zelkova)|Python3|欅坂46のブログを機械学習を用いて自動生成した。web上にある欅坂のブログをスクレイピングし、文章をmecabを用いて形態素に分解し、単語ベクトルを生成し、LSTM（RNNの一種）で文章を自動生成した。|

### Webアプリ

|レポジトリ名|言語|説明|
|---|---|---|
|[homepage](https://github.com/Toasa/homepage)|PHP|自作ホームページ。Laravel + MySQLでのHP＆ブログホスティングサービス(2020年9月現在クローズ)|
|[bbs](https://github.com/Toasa/bbs)|PHP|自作掲示板。Ajax通信を利用した掲示板。JSフレームワークとしてVue.jsを使用。|
