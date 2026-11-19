# 科学プレゼンの構成と推敲

研究紹介や学会発表の構成、図の見せ方、用語、発表原稿と時間配分を設計するCodex向けスキルです。篠本滋氏の講義「プレゼンテーションの技法」を画面と字幕から分析し、再利用できる判断基準に整理しました。

バージョン：1.0.0

配布元：[H1S4G10rc4/shinomoto_slide](https://github.com/H1S4G10rc4/shinomoto_slide)

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
主要な図を使い 各図の読み方と発表者ノートも付けて
```

既存スライドのレビューにも使えます。

```text
$scientific-presentation-techniques でこの発表をレビューして
タイトルと結論の対応 図の読み取り 用語の曖昧さを確認し
問題がある箇所に具体的な修正案を示して
```

スキル自体は文章による指示と参考資料で構成され、追加の実行ライブラリや元動画のダウンロードを必要としません。PDFの読取りやスライドファイルの生成には、利用環境側の対応ツールが必要です。

## 適用する判断基準

- 聴衆と持ち時間から中心メッセージを定める
- タイトルの問いと結論の答えを対応させる
- 定義と単純な例から条件を変えた比較へ進む
- 図の軸や条件を残し 比較する箇所と読み取れる結果を示す
- 観測結果と解釈と限界を区別する
- スライドの文章と口頭説明を分ける

構成案では、各スライドの役割、主張、図、口頭説明、目安時間を示します。論文にない結果を補ったり、固定の枚数や四部構成に当てはめたりしない設計です。

## 見出しの表記

スライドのタイトル、副題、セクション見出しでは、原則として句読点を一切使いません。和文と英文のコンマ・ピリオドを含め、途中にも末尾にも付けません。長い見出しは言い換えや改行で整理します。

小数点や略語の表記を保持する必要がある情報は本文、出典、ノートへ移します。本文や図中ラベルの句読点は使用できます。利用者が個別に別の表記を指定した場合は、その指定に従います。

この表記方針は作成依頼者の希望で追加したものです。元動画の教えとして扱いません。

## 同梱ファイル

| ファイル | 内容 |
|---|---|
| [SKILL.md](SKILL.md) | 適用範囲と判断基準 |
| [agents/openai.yaml](agents/openai.yaml) | Codex向けの表示名と呼び出し例 |
| [references/application-patterns.md](references/application-patterns.md) | 構成案とレビューの具体例 |
| [references/source-analysis.md](references/source-analysis.md) | 元動画の時刻と各技法の対応 |
| [LICENSE](LICENSE) | MITライセンス全文 |

## 出典とライセンス

参照した講義は、篠本滋氏の[「プレゼンテーションの技法」](https://www.youtube.com/watch?v=Dw4khOfDGHk)です。チャンネルはShinomoto-san、公開日は2022年4月7日です。講師の説明と本スキルへの応用上の解釈は、[分析記録](references/source-analysis.md)で区別しています。本スキルは講師やチャンネルの公式配布物ではありません。

スキル本文と付属文書は[MITライセンス](LICENSE)で配布します。[ライセンス原文](https://opensource.org/license/mit)を採用しています。元動画、字幕、画面画像、論文などの第三者コンテンツは同梱せず、このMITライセンスの対象にも含めません。
