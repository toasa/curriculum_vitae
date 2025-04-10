# 職務経歴書

## 個人情報

* 名前：遠山 篤史(とおやま あつし)
* GitHub：https://github.com/Toasa
* 学歴
  * 名古屋大学 大学院 多元数理科学研究科 (2016年-2018年)
  * 佐賀大学 理工学部 数理科学科 (2012年-2016年)

## 職務概要

|期間|会社|職種|概要|主な技術スタック|
|---|---|---|---|---|
|2020年12月 - 現在|[株式会社イーゲル](https://www.igel.co.jp/)| ソフトウェアエンジニア、研究調査|RDMA シミュレータ・アクセラレータの開発 / Android のグラフィクスに関する調査|RDMA, [DPDK](https://www.dpdk.org/), Android, C, C++|
|2019年11月 - 2020年11月| [コネクトフリー株式会社](https://ewm.co.jp/)| 言語処理系エンジニア | Zen 言語を使用した脆弱性検出ツールの開発、標準ライブラリの開発 | Zen言語, C++, LLVM IR |
|2018年4月 - 2019年9月| [株式会社EWMファクトリー](https://ewm.co.jp/)| ウェブエンジニア | CMSや自社製のPHPフレームワークを使用したWebサイトの改修・保守業務|PHP, CMS(Movable Type)|

## 職務経歴

### [株式会社イーゲル](https://www.igel.co.jp/) (2020年12月 - 現在)

#### RDMA アクセラレータの開発 (2025年04月 - 現在)


#### Android のグラフィクスに関する調査 (2024年10月 - 2025年3月)

- 開発環境
  - C++, Java, Android 14, 15
- ポイント
  - Android グラフィクスの理解
    - Android のディスプレイパイプライン（アプリによる描画処理、SurfaceFlingerによる合成処理、HWC による画面表示）
    - VSYNC、ジャンクフレーム
  - Android 15 に登場したディスプレイミラーリング機能の調査
    - MirroredSurfaceView というミラーリング機能の調査。公式ドキュメントによる説明がなかったため、ソースコードから使用方法や性能を把握
    - テストプログラムの作成
    - エミュレータ上での動作確認
  - 動画 (フルHD@60fps) 再生時の性能評価
    - [Perfetto](https://perfetto.dev/) という Android のトレースツールを用いた性能評価。CPU, GPU 使用率、SurfaceFlinger の合成時間などクエリする SQL の作成。
    - [FrameTimeline を用いたジャンク検出機能](https://perfetto.dev/docs/data-sources/frametimeline)の調査。60fps の動画生成で合成時間が 16.6 msを越えるにも関わらずジャンクと判定されないフレームが存在したため、ソースコードから原因を特定。スケジューラが想定したフレーム終了時刻と実際の表示時刻の差が一定時間以内であればジャンクと判定されないことがわかった。
- 2名/メンバー

#### RDMA アクセラレータの開発 (2021年4月 - 2024年10月)

- 開発環境
  - C, DPDK, Ubuntu 20.04
- ポイント
  - RDMA 通信を高速化するアプリケーションの開発
    - RDMA のアクセラレータとして振る舞うアプリの開発。RDMAの通信ホストはアプリの存在を認知せず、通信を高速化する。
    - パケット処理に [DPDK](https://www.dpdk.org/) を使用。アプリケーションが NIC を管理することにより、パケットの送受信をカーネルを介さず、高速に処理することができる。
  - アクセラレータ開発では、パケット処理以外のサブ機能を担当
    - 設定ファイルの読み込み機能
      - 静的に渡したい値（内部バッファのサイズ、アクセラレータ機能の無効化、）を TOML ファイルから設定し、その設定を読み込めるようにした。
    - アプリケーションの高速化のための環境設定
      - 開発環境では CPU、NIC、メモリのペアが複数個存在する環境（NUMA 環境）だったため、NIC が載った NUMA ノードでアプリが動くように動かすよう、numactl、isolcpus で設定 
    - DPDK が提供する shaper 機能の調査、実装
      - パケットの流量制限と平滑化を行いたい動機から、DPDK の shaper 機能を調査し、テストプログラムを作成。実機の RDMA NIC では対応していなかったため、softnic を用いた実装
    - DPDK が提供するメトリクス機能の調査
      - 入出力のビットレートなどの stats 機能の実装
    - アクセラレータ機能の On/Off を動的に切り替え
      - 内部バッファの使用率に応じて、アクセラレータ機能を停止、再会する機能を実装
    - RDMA NIC 実機上でのテスト
      - アクセラレータ機能の On/Off、RDMA オペレーション (RDMA WRITE, RDMA READ, SEND)、パケットサイズなどを変えテスト
      - E810 / ConnectX-5,6 などの RDMA NIC でテスト
    - DPDK バージョンアップ対応
      - Deprecated になった API の置き換え
    - 通信の完了時間の計測
      - ホスト間での正確な時刻同期のため、PTP Timestamping を使用
  - アクセラレータの性能を検証するための、テストプログラムの開発
    - Periodic に RDMA パケットを送信するアプリの開発
      - アクセラレータが存在することにより、Jiiter の低減、パケロス時の早期回復を証明
- 2名/メンバー

#### RDMA アクセラレータの開発に向けた PoC 用シミュレータ開発 (2020年12月 - 2021年4月)

- 開発環境
  - C++, Ubuntu 20.04
- ポイント
  - [ns-3](https://www.nsnam.org/) を用いたシミュレータ開発
    - 大容量・低遅延を目指したネットワークの実現に向け、試験的に策定したネットワークプロトコルについて、PoC としてのシミュレータを ns-3 を用いて作成した。
  - アプリケーション層 (NVMe-oF) とトランスポート層 (RDMA) の分離を意識した開発
    - NVMe-oF の仕様把握。NVMe という SSD 向けの高速通信規格を、ネットワークに接続されたホスト間での通信に拡張したもの。
    - RDMA の仕様把握。ネットワークを介して、リモートホストのメモリに直接アクセスする機能。
  - [Wireshark](https://www.wireshark.org/) を使用したパケットの解析、検証
    - 打ち出すパケットの中身を解析し、期待するペイロードか確認。また、自作したパケットの正当性を Wireshark の Dissector により確認。
- 2名/メンバー

### コネクトフリー株式会社 (2019年11月 - 2020年11月)

#### LLVM-IRを解析する脆弱性検出ツールの開発 (2019年11月 - 2020年11月)

- 開発環境
  - Zen
- ポイント
  - 開発動機
    - Zen 言語をアピールするための PoC 用アプリの開発。Zen 言語のコンパイラがバックエンドに LLVM を用いることから、LLVM IR (LLVM の中間表現) を解析して脆弱性を検出できると、元のZen 言語ソースコードのチェッカ機能としても活用できそう。また、LLVM IR という中間表現のチェッカのため、Zen 言語だけでなく、C/C++/Rust など LLVM IR をターゲットにする言語の脆弱性も発見でき嬉しいという動機。
  - 必要な知識の習熟
    - C言語のぜい弱性に関する知識
    - LLVM-IR の習熟
  - 実装
    - バッファオーバーフローの検出機能の実装。配列のサイズとインデックスの値からオーバーフローを検出した。
    - 未使用関数の検出機能の実装。関数のコールグラフを作成し、ルートから辿れるものは使用済みとしてマークした。
    - C-FFI の作成
  - その他
    - コロナウイルスの発生に伴い、開発途中からリモートワークに移行。またそのタイミングでプロジェクトリーダーを務める。
    - アジャイル開発の経験
- 4名/メンバ（プロジェクトの途中からリーダー）

#### 時間、時刻を扱う標準ライブラリの作成 (2020年8月)

- 開発環境
  - Zen
- ポイント
  - API 仕様決め
    - ライブラリ作成の動機は主に２つ。１. 組み込み向けのアプリ開発時に時間の計算機能が必要となる場面が増えたため。2. Zen のフォーク元の [Zig 言語](https://ziglang.org/)には、開発当時、時間に関する標準ライブラリが存在しなかったため。
    - 仕様決め。Go, Rust, C++ など既存言語の標準ライブラリを参照し、かつ必要最小限の機能（時間に時刻を加減算する機能、２つの時間を比較する機能）のみ盛り込む。
    - 日時を内部データで管理するため、Unix時間、うるう年、うるう秒の仕様を把握した。
  - エラー処理
    - 範囲外の時間、不正な演算結果などのエラー処理
  - テスト駆動開発
- 2名/メンバー

### 株式会社EWMファクトリー (2018年4月 - 2019年9月)

#### ニュース系Webサイトの改修業務 (2019年1月 - 2019年9月)

- 開発環境
  - macOS, CMS(Movable Type6)
- ポイント
  - 記事の表示時間を短縮
    - 表示処理時に全記事のループをやめ、あらかじめ記事をハッシュ化した上で、必要な記事のみを選択するようにした。計算量を`O(n)`から`O(1)`に短縮した。
    - 記事の更新タイミングと、記事に付随する広告の生成タイミングを分離。広告の生成は、アクセスの少ない深夜に、cronを用いて行った。
  - CMS バージョンアップに伴うテストの実施
    - 必要なテストの洗い出し。テストを記事の表示テスト、投稿機能のテストに大別。表示テストでは、記事内容、リンクの正しさ、複数ブラウザによる検証などを実施。投稿機能のテストでは、新規投稿、既存記事の編集、記事の削除機能などを検証した。
- 3名/メンバー

#### 官庁系Webサイトの保守業務 (2018年6月 - 2018年12月)

- 開発環境
  - macOS, 自社製のPHPフレームワーク
- ポイント
  - MVCモデルの習熟

## 言語経験

|言語|業務|業務外|
|---|---|---|
|C|4年|3年|
|C++|1年|-|
|Go|-|1年|
|Python3|-|3年|
|SQL|半年|-|
|PHP|半年|-|

## 自己PR

### 性格

これまで経験した職種は Web系、言語処理系、ネットワーク系と変化していますが、
未経験の分野であっても好奇心を持って勉強し、挑戦することができます。

気になったことを根気強く調べ、時間をかけて理解を進めることが好きです。
例えば、オペレーティングシステムの教科書で init プロセスという最初に起動するプロセスについて知り、
そのプロセスがどのように生成され、実行されるか興味があったため、
[xv6](https://github.com/mit-pdos/xv6-riscv)という教育用 OS のソースコードを読み、
[カーネル/VM探検隊](https://connpass.com/event/161201/)という低レイヤ技術好きの勉強会で発表しました（[スライド](https://speakerdeck.com/toasa/xv6-initpurosesu-kotohazime), [ビデオ](https://youtu.be/J-pF4fg3r04?t=1750)）。

予定を立てコツコツとタスクをこなすことが得意です。他者の気持ちを汲み、チームの一員として協力してプロジェクトを進めることができます。

### 技能

言語処理系は業務外において自作し、基本的な理論から実装まで幅広い知識を持っています。

### 資格

- TOEIC 850 点 (受験日: 2021年6月20日午後)

## 業務外/個人活動

低レイヤ技術（コンパイラ、OS）、計算理論（オートマトン、計算可能性、計算複雑性）に興味があります。
言語処理系では主にCコンパイラ、Lispインタプリタなどを実装しました。
計算理論は "Introduction to the theory of computation" から学び、実装として正規表現エンジンを作成しました。

### 言語処理系

|レポジトリ名|言語|説明|
|---|---|---|
|[2020cc](https://github.com/Toasa/2020cc)|C|C言語のコンパイラを自作した。C言語のソースコードをトークナイズし、トークン列をパースして抽象構文木を生成。生成した構文木からアセンブリを出力する。一連のプロセスをテストするユニットテストを作成。|
|[tisp](https://github.com/Toasa/tisp)|C|Lispインタプリタを自作|
|[regexp](https://github.com/Toasa/regexp)|Go|正規表現エンジンを自作。構文木の出力、状態遷移図の出力、正規表現の受理判定を実装。|
|[tgoc](https://github.com/Toasa/tgoc)|Go|Go言語のコンパイラを自作|
|[g9cc](https://github.com/Toasa/g9cc)|Go|C言語のコンパイラを自作|
|[monkey by rust](https://github.com/Toasa/monkey_by_rust)|Rust|書籍化された [Monkeyインタプリタ](https://monkeylang.org/)について、Go言語で書かれた実装を Rust で書き直した。|
|[tbf](https://github.com/Toasa/bf_interpreter)|C|Brainf*ckインタプリタ|

### ゲーム

|レポジトリ名|言語|説明|
|---|---|---|
|[getris](https://github.com/Toasa/getris)|Go|Go言語でテトリスのような落ちものゲームを作成した。|
|[game of life](https://github.com/Toasa/game_of_life)|Go|Go言語でライフゲームを作成した。|

### 機械学習

|レポジトリ名|言語|説明|
|---|---|---|
|[zelkova](https://github.com/Toasa/zelkova)|Python3|ネット上にあるブログを学習し、機械学習によってブログを自動生成するアプリ。ブログをスクレイピングし、文章を mecab を用いて形態素に分解し、単語ベクトルを生成し、LSTM（RNNの一種）で文章を自動生成した。|

### Webアプリ

|レポジトリ名|言語|説明|
|---|---|---|
|[homepage](https://github.com/Toasa/homepage)|PHP|自作ホームページ。Laravel + MySQLでのHP＆ブログホスティングサービス(2020年9月現在クローズ)|
|[bbs](https://github.com/Toasa/bbs)|PHP|自作掲示板。Ajax通信を利用した掲示板。JSフレームワークとしてVue.jsを使用。|
