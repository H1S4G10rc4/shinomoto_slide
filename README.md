# 科学プレゼンの構成と図解

研究紹介や学会発表を章立てし、引用図・概念図・フローチャートを中心に説明するCodex向けスキルです。スライドの制作では全ページにスピーカーノートを付けます。Google Slidesへの実装手順も含みます。

バージョン：1.5.0

配布元：[H1S4G10rc4/shinomoto_slide](https://github.com/H1S4G10rc4/shinomoto_slide)

篠本滋氏の講義から抽出した構成と推敲の技法に、依頼者の指定した章立て、参考PDFのレイアウト、`scientific-figure-design` の作図方針を組み合わせています。

## 作成するスライド

- BackgroundとIntroductionで前提と問いを分け Contentsは必要な場合に加える
- Methodsは処理図や概念図 Resultsは引用図やデータに基づくグラフを中心にする
- BackgroundとIntroductionを整えてから 本文のFigと各パネルを原著の順に本編で説明する
- Summaryは必ず文章の箇条書きにし 限界や解釈も必要に応じて文章で説明する
- 本編に収まらない補助情報はSummaryの後のAppendixに載せ 本編から案内する
- 左上には通常はセクション名を置き 論文図のページではFig.1-aなどの図識別子に置き換える
- 見出しは中央に揃え 重複する凡例説明を削り 必要な補助注記は図の近くへ小さく置く
- 白背景に黒い文字を置き 強調には赤を使う
- 見出しには原則として句読点を一切使わない
- 全スライドに各パネルの条件 軸 観察 解釈 留保を省略しない発表原稿を付ける
- 結果の直前に必要な手法と数理を説明し 代表的方法との違いを推定対象と仮定から示す
- 数式はTeXで組版し 原式 記号 画像の可読性を確認する
- ノートは発表全体の問いと結果をつなぐ話し言葉だけにし 英語発表では英語原稿の後に対応する日本語原稿を置く
- 一枚のメッセージを絞るために スライド枚数 行数 ノートの分量が増えることを厭わない
- 英語では用語と主張の強さを保ち 文法と数式記号も確認する
- 概念図では実体と変換前後を見せ 比較と因果の矢印を区別する
- 参考PDFに合わせて文字サイズだけでなく 見出しと章名の位置 図の面積 比較配置 余白も揃える

章の順序や枚数は聴衆と持ち時間に合わせて調整します。表は数値や仕様の照合が目的のときに使い、説明の既定にはしません。図中の文言は英語、スライド本文と原稿は依頼の言語に合わせます。利用者が別の言語・デザイン・構成を指定した場合は、その指定を優先します。

図が証拠や関係の理解を助けるページでは図を使い、適用範囲や限界を述べるページでは文章の箇条書きも使います。図を外しても説明が変わらない場合、装飾として図を再掲しません。Summaryは短い名詞の列ではなく、条件と結論が分かる文章の箇条書きにします。

このリポジトリの配布対象はスキルの指示と設計情報です。生成したスライドや作例は含めません。

論文本文のFigはすべて本編で扱うことを出発点とし、複合図は必要な枚数へ分割し、全パネルを原著の順に本編で説明します。固定の枚数へ収めるために説明をAppendixへ押し出しません。ノートや小さな一覧画像だけでは掲載済みとしません。SupplementaryやExtended Dataは議論との関連で選びます。明示された時間や範囲の制約で本文Fig全体をAppendixに回す場合は本編から掲載先を示し、未掲載があれば理由を明記します。

参考デザインの基準は720 × 405 pt、見出し18 pt、章名と主要本文16 ptです。英語でもNoto Sans JPを使い、章名と中央見出しをほぼ同じ高さの上部に配置します。96 dpiのCSS pxを使う環境では960 × 540 pxへ換算し、最終形式の寸法と文字を確認します。

## 導入

Gitを使う場合は任意の作業フォルダで次を実行します。

```sh
git clone https://github.com/H1S4G10rc4/shinomoto_slide.git scientific-presentation-techniques
```

GitHubの「Code → Download ZIP」を使う場合は、展開したフォルダを `scientific-presentation-techniques` に改名してください。配布用ZIPに同名のフォルダが含まれている場合は、そのまま使えます。

取得した `scientific-presentation-techniques` フォルダをユーザー用のスキルフォルダに配置します。フォルダ直下に `SKILL.md` がある構造を保ってください。

Codexの現行公式ドキュメントでは、ユーザー用の配置先は `~/.agents/skills/` です。配置先や読み込み方法は利用する環境の設定を優先してください。[公式の配置先一覧](https://learn.chatgpt.com/docs/build-skills#where-codex-loads-local-skills)

macOSまたはLinuxでは、取得したフォルダの親ディレクトリで次を実行できます。既存の同名スキルがある場合はコピーを中止します。

```sh
skill_source="./scientific-presentation-techniques"
skill_destination="$HOME/.agents/skills/scientific-presentation-techniques"

if [ ! -f "$skill_source/SKILL.md" ]; then
  printf '%s\n' '取得したスキルの親ディレクトリで実行してください'
elif [ -e "$skill_destination" ] || [ -L "$skill_destination" ]; then
  printf '%s\n' '同名のスキルがあるためコピーを中止しました'
else
  mkdir -p "$(dirname "$skill_destination")" &&
    cp -R "$skill_source" "$skill_destination"
fi
```

スキルが表示されない場合はCodexを再起動してください。既存のスキルを更新する場合は、変更内容を確認し、元のフォルダを退避してから置き換えてください。

## 使い方

論文や発表資料を添付し、聴衆と持ち時間を指定します。

```text
$scientific-presentation-techniques を使って
この論文を研究室の学生向けに15分で紹介するスライドを作って
Contents Background Introductionなどの章立てを設け
本文のFigをすべて扱い 本編に収まらない補助情報はAppendixに載せ
引用図の編集と概念図を中心に説明して
全スライドにスピーカーノートを付けて Google Slidesで作って
```

既存スライドのレビューにも使えます。

```text
$scientific-presentation-techniques でこの発表をレビューして
タイトルと結論の対応 図の読み取り 用語の曖昧さを確認し
問題がある箇所に具体的な修正案を示して
```

スキル自体は指示と参考資料で構成され、追加の実行ライブラリや元動画のダウンロードを必要としません。PDFの読取りやスライド制作には利用環境側の対応ツールが必要です。`scientific-figure-design` がある場合は併用し、ない場合も同梱の作図方針で進められます。

Google Slidesでの制作には、作成・編集・ノート読取りに対応する接続ツール、または許可されたログイン済みブラウザが必要です。指定されたアカウントと保存先を確認し、既存資料の編集では指定URLを保ちます。変換後の図・配置・全ノートを読み戻す手順も含みます。このスキルに認証情報やGoogleとの接続機能そのものは含まれません。

## 適用する判断基準

- 聴衆と持ち時間から中心メッセージを定める
- タイトルの問いと結論の答えを対応させる
- 定義と単純な例から条件を変えた比較へ進む
- 図の軸や条件を残し 比較する箇所と読み取れる結果を示す
- 観測結果と解釈と限界を区別する
- スライドの文章と口頭説明を分ける

構成案では章ごとにスライドを並べ、各ページの役割、主張、図の出典と編集、原稿、目安時間を示します。論文にない結果を補ったり、固定の枚数や四部構成に当てはめたりしない設計です。

## 見出しの表記

スライドのタイトル、副題、セクション見出しでは、原則として句読点を一切使いません。和文と英文のコンマ・ピリオドを含め、途中にも末尾にも付けません。長い見出しは言い換えや改行で整理します。

小数点や略語の表記を保持する必要がある情報は本文、出典、ノートへ移します。ただし左上の `Fig.1-a` などの図識別子は参照記号としてそのまま使います。本文や図中ラベルの句読点は使用できます。利用者が個別に別の表記を指定した場合は、その指定に従います。

この表記方針は作成依頼者の希望で追加したものです。元動画の教えとして扱いません。

## 同梱ファイル

| ファイル | 内容 |
|---|---|
| [SKILL.md](SKILL.md) | 適用範囲と判断基準 |
| [agents/openai.yaml](agents/openai.yaml) | Codex向けの表示名と呼び出し例 |
| [references/application-patterns.md](references/application-patterns.md) | 構成案とレビューの具体例 |
| [references/figure-walkthrough.md](references/figure-walkthrough.md) | 原著の図順と文章の箇条書きと省略しないノート |
| [references/methods-and-story.md](references/methods-and-story.md) | 核心の数理と代表的方法の比較と発表全体の接続 |
| [references/paper-coverage.md](references/paper-coverage.md) | 本文Figとパネルの掲載範囲とAppendixの構成 |
| [references/source-analysis.md](references/source-analysis.md) | 元動画の時刻と各技法の対応 |
| [references/slide-design.md](references/slide-design.md) | レイアウトと配色の使い分け |
| [references/design-system.json](references/design-system.json) | 座標と書式の初期値 |
| [references/conceptual-diagrams.md](references/conceptual-diagrams.md) | 6報の論文図の読み解きと概念図の設計 |
| [references/figure-workflow.md](references/figure-workflow.md) | 引用図の編集と新規作図の方針 |
| [references/google-slides.md](references/google-slides.md) | Google Slidesへの実装とノートの確認 |
| [LICENSE](LICENSE) | MITライセンス全文 |

## 出典とライセンス

参照した講義は、篠本滋氏の[「プレゼンテーションの技法」](https://www.youtube.com/watch?v=Dw4khOfDGHk)です。チャンネルはShinomoto-san、公開日は2022年4月7日です。講師の説明と本スキルへの応用上の解釈は、[分析記録](references/source-analysis.md)で区別しています。本スキルは講師やチャンネルの公式配布物ではありません。

章立てとデザインには依頼者から提供された進捗報告とJournal ClubのPDFを参考にしています。内容の正しさや発表技法の模範として扱うものではありません。作図の判断基準には、依頼者が指定した `scientific-figure-design` の知見を取り入れています。

スキル本文と付属文書は[MITライセンス](LICENSE)で配布します。[ライセンス原文](https://opensource.org/license/mit)を採用しています。元動画、字幕、画面画像、参考PDF、論文、別スキルのファイルそのものは同梱せず、このMITライセンスの対象にも含めません。
