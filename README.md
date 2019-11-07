# alpr_jp

自動車の車両識別標識(ナンバープレート)を検知、認識するための学習モデル作成用の素材を管理するプロジェクトです。

![](https://pbs.twimg.com/media/D-IrWPyUEAUAd4b?format=png&name=small)

## Open ALPR

オープンソースのナンバープレート認識システム Open ALPR を利用します。
Open ALPR では、OpenCV と Tessaract-OCR を使い、以下の解析を行います。

1. ナンバープレートらしき形状の検出。
2. 検出した形状部分を台形補完し、平面展開する。
3. 展開された画像から OCR でナンバー、文字を認識する。

この 1 のフェイズで、「ナンバープレートとは一体どのようなものなのか」を学習させてやる必要があります。
具体的には、次のような画像を大量に覚えさせ、傾向を掴ませます。

![](https://pbs.twimg.com/media/EIu72OeUEAERVyj.jpg)

2019年11月7日時点で、自家用車・事業用車・自家用車(軽)・事業用車(軽)の4種類を合わせて、200枚の画像があります。
本プロジェウトの目標枚数は、1000枚以上です。

## 画像の仕様

* PNG 形式 または JPEG 形式。
* 幅 100 px 〜 400 px 程度。
* できるだけナンバープレートを正面から取らえたもの。台形補正をかけても良いが、極端なパースがついたものは補正後も比率・分解能が変わるため、好ましくない。
* ボケあり、不鮮明なものでも可。見えやすいよう色調補正をかける必要はない。
* アスペクト比は厳密には指定しない。ただし、中判(一般的なサイズ)は 330mm × 165mm (2:1) であることに留意されたい。

(寸法値の参考引用)

![](https://astamuse.com/ja/drawing/JP/970/07/091/A/000010.png)

## ナンバープレートの種類

現行の日本の陸運局が管理するナンバープレートには、いくつか種類があります。

* 自家用
  * 普通車
  * 大型車(大判)
  * 軽自動車
* 事業用
  * 普通車
  * 大型車(大判)
  * 軽自動車
* 地方版図柄入りナンバー
* 五輪記念ナンバー
* ラグビーW杯記念ナンバー
* 小型二輪、軽二輪ナンバー
* etc

このうち、一般的な自家用と事業用のみを募集します。(白地に緑字、黄地に黒字、それらの反転)

## 法的問題

### 個人情報

ナンバープレートの写真からは、2007年の法改正以後、個人が正当な根拠なしにその所有者の個人情報を得るのができなくなりました。また、総務省の資料( http://www.soumu.go.jp/main_content/000028227.pdf )でも

> 自動車のナンバープレートの番号が写り込んでいた場合も、ナンバープレートの番号からその登録名義人を照会することは容易ではないことから11、個人識別性を欠き、「個人情報」には該当しないと考えられる。

との記載があり、個人情報には当たらないという判断が一般的です。
ただし、ナンバープレートの写真に個人識別でいる可能性がある複数の事象が映り込んだり、付随する情報がある場合は、個人情報につながる可能性があります。例えば、

* 風景
* 車体(ナンバープレートの周辺以外の全体)
* 周辺の人物
* 運転者の顔
* 撮影日時、撮影場所

などです。

そこで本プロジェクトは、ナンバープレートの画像の取り扱いについて

* 公開される画像は、ナンバープレート学習に必要な範囲だけトリミングをしたものとする。(その他の要素が映り込まない)
* 撮影日時、撮影場所などの情報をいかなる形でも画像に関連付けしない。
* ナンバープレートの所有者から申し立てがあった場合、リポジトリからの削除等、適切な対応を行う。

とします。

### 著作権

画像の著作権は、画像作成者にありますが、このリポジトリに組み込まれた時より MIT License のもと、配布されます。
