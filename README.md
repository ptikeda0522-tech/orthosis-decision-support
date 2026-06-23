# 下肢装具選定支援Webアプリ v0.3 pilot

脳血管障害患者の下肢装具選定における臨床推論を整理するための、PT/OT向け試作Webアプリです。

v0.3では、提供画像の「脳卒中下肢装具アルゴリズム」を参考に、BRSを起点としてKAFOコース/AFOコースへ分岐するロジックへ再実装しました。

## 重要な注意

- 本アプリは診断、処方、最終判断を代替するものではありません。
- 提供画像の施設内アルゴリズムをそのまま複製するものではなく、臨床推論の流れを参考に一般化した試作版です。
- 実証実験では、患者氏名、患者ID、生年月日、病棟、入院日、詳細経過など、個人を特定できる情報を入力しないでください。
- 最終判断は医師、義肢装具士、リハビリ職の評価、歩行観察、皮膚状態、生活環境を踏まえて行ってください。

## v0.3の主な判定軸

- BRS下肢
- 高次脳機能障害、Pusher、USN
- 非麻痺側上肢支持での静止立位
- ROM制限、強固な拘縮、変形
- 指示理解、ロック管理
- 年齢、活動性
- 非麻痺側下肢伸展位保持
- 麻痺側下肢伸展位保持
- 麻痺コントロール、下垂足

## v0.3の主な出力候補

- 特殊支持を含むKAFO / 訓練用KAFO
- SPEX膝継手付KAFO
- ダイヤルロック膝継手付KAFO
- リングロック膝継手付KAFO
- 金属支柱付きAFO / Shoe horn AFO
- APS-AFO / Gait Solution
- 湯之児式AFO / UDFlex long
- Gait Solution / GS-Design / 硬性AFO
- UDFlex long / 大河原式 / Dream Brace
- 靴型装具 / インソール / 簡易AFO
- UDFlex short / KU half / ORTOP / インソール

## ファイル構成

- `index.html`: アプリ本体。HTML/CSS/JavaScript一体型です。
- `README.md`: この説明書です。

## ローカルで確認する方法

このフォルダで以下を実行します。

```bash
python3 -m http.server 8080
```

ブラウザで開きます。

```text
http://127.0.0.1:8080/
```

8080番が使用中の場合は、8081番など別のポートで起動します。

```bash
python3 -m http.server 8081
```

```text
http://127.0.0.1:8081/
```

## GitHubで公開する方法

### 1. GitHubにログイン

1. <https://github.com/> を開きます。
2. 右上の `Sign in` からログインします。
3. アカウントがない場合は `Sign up` で作成します。

### 2. 新しいリポジトリを作る

1. ログイン後、右上の `+` を押します。
2. `New repository` を選びます。
3. `Repository name` に名前を入れます。
   - 例: `orthosis-decision-support`
4. 公開実験でURL共有したい場合は `Public` を選びます。
5. `Add a README file` はオンでもオフでも構いません。
6. `Create repository` を押します。

### 3. ファイルをアップロード

1. 作成したリポジトリ画面で `Add file` を押します。
2. `Upload files` を選びます。
3. このフォルダ内の `index.html` と `README.md` をドラッグ&ドロップします。
4. 下部の `Commit changes` を押します。

### 4. GitHub Pagesを有効化

1. リポジトリ画面上部の `Settings` を開きます。
2. 左側メニューの `Pages` を開きます。
3. `Build and deployment` の `Source` で `Deploy from a branch` を選びます。
4. `Branch` で `main` と `/ (root)` を選び、`Save` を押します。
5. 数分待つと公開URLが表示されます。
   - 例: `https://ユーザー名.github.io/orthosis-decision-support/`

GitHub Pagesの反映には数分かかることがあります。

## Googleフォームを使った実証実験のすすめ

最初の実証実験では、アプリ側にデータ保存機能を持たせず、Googleフォームでフィードバックを集める方法が安全で簡単です。

### 推奨質問

1. 職種
   - PT
   - OT
   - 医師
   - 義肢装具士
   - その他
2. 臨床経験年数
   - 1年未満
   - 1〜3年
   - 4〜7年
   - 8年以上
3. 推奨結果は臨床感覚と合っていましたか
   - 1: 合わない
   - 2
   - 3
   - 4
   - 5: とても合う
4. 操作はわかりやすかったですか
   - 1: わかりにくい
   - 2
   - 3
   - 4
   - 5: とてもわかりやすい
5. 装具選定の思考整理に役立ちそうですか
   - 1: 役立たない
   - 2
   - 3
   - 4
   - 5: とても役立つ
6. 判定結果のコピー内容
   - 長文回答
7. 不足している評価項目
   - 長文回答
8. 判定ロジックへの違和感
   - 長文回答
9. 教育・新人指導に使えそうですか
   - はい
   - いいえ
   - どちらともいえない
10. その他コメント
   - 長文回答

### フォームURLをアプリに設定する方法

Googleフォームを作成したら、共有URLをコピーします。

`index.html` の下記部分を探します。

```js
const FEEDBACK_FORM_URL = "https://docs.google.com/forms/d/e/1FAIpQLScin42L7aQNAwfy_49bJjxTXf4iHvB1DH0oOfFRb_92nHtbqg/viewform";
```

次のようにURLを貼り付けます。

```js
const FEEDBACK_FORM_URL = "https://docs.google.com/forms/d/e/1FAIpQLScin42L7aQNAwfy_49bJjxTXf4iHvB1DH0oOfFRb_92nHtbqg/viewform";
```

これでアプリ内の「フォームを開く」ボタンからフォームへ移動できます。

## 実証実験の進め方

おすすめは2週間の小規模パイロットです。

1. 対象者: PT/OT 10〜30名
2. 方法: 仮想症例、または個人情報を除いた症例傾向で使用
3. 収集: Googleフォームで主観評価と自由記載を回収
4. 評価: 操作性、臨床適合度、教育利用可能性、不足項目を確認
5. 改善: 判定ロジックと入力項目をv0.3へ更新

## 共有時の文面例

以下をメールや院内チャットで共有できます。

```text
脳卒中患者さんの下肢装具選定を支援する試作Webアプリを作成しました。
臨床推論の整理や新人教育に使えるかを検証したく、数分で触ってフィードバックをいただけると助かります。

注意:
本ツールは診断・処方・最終判断を代替するものではありません。
患者氏名、ID、生年月日など、個人を特定できる情報は入力しないでください。

アプリURL:
ここにGitHub PagesのURLを貼る

フィードバックフォーム:
https://docs.google.com/forms/d/e/1FAIpQLScin42L7aQNAwfy_49bJjxTXf4iHvB1DH0oOfFRb_92nHtbqg/viewform
```
