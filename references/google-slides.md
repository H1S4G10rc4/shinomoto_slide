# Google Slidesへの実装

## 出力先と利用環境

Google Slidesを指定された場合は、編集可能なネイティブのGoogle Slidesを納品する。PPTXをDriveに置いただけの状態をGoogle Slides版と呼ばない。新規制作か、既存のネイティブ資料の編集かを最初に区別する。

現在の `presentations` とGoogle Slides向け制作スキルが利用できれば、その振り分けとツール仕様を読む。新規制作では現在の環境が定める制作・インポート経路を使う。既存のGoogle Slidesはネイティブで編集し、テンプレートとして指定された場合はコピーに内容を反映する。接続や権限、必要な変換機能がなければ不足を説明し、構成・図・原稿の準備を進める。別形式をGoogle Slides完成版として渡さない。

このスキルは接続や認証を同梱しない。配布先にないツール名を呼び出せると仮定せず、利用可能な連携を探す。

## 新規制作と変換

2026年11月20日に確認したCodexのPresentations手順では、新規Google SlidesはローカルでPPTXを作成・確認してから、Driveの `import_presentation` 相当の操作で `upload_mode: native_google_slides` に変換する。提供するスライドには最初からノートを設定する。将来の制作スキルやユーザー指定が異なる場合は、その手順を優先する。

変換後はネイティブのファイル種別とURLを確認し、スライド順、画像、編集可能な文字・図形、ノートを読み戻す。PPTXからの変換で各要素が保存されたと仮定しない。原図の画像は保ち、見出し、章名、注釈、フローチャートの文字と線は可能な限り編集可能にする。

## スピーカーノートを書き込む

Google Slides APIでは、各スライドのノート用オブジェクトIDを取得し、そのテキストを更新する。IDの取得場所と書込み方法は[公式のノート操作](https://developers.google.com/workspace/slides/api/guides/notes)を確認する。

1. プレゼンテーションを読み、各 `slide.objectId` と `slide.slideProperties.notesPage.notesProperties.speakerNotesObjectId` を対応させる。スライド番号からIDを推測しない。
2. 生成した原稿を実際のスライドの順序とIDに対応させる。既存デッキの編集では、対象外のノートや発表者が書いた情報を不用意に消さない。
3. ノートオブジェクトが存在する場合は、そのテキストを読み、更新対象の本文を準備する。既存テキストを生成済み原稿へ置き換える箇所だけ `deleteText` と `insertText` を同じbatchUpdateに含める。ノートオブジェクトがない場合は、取得した `speakerNotesObjectId` へ `insertText` を送り、自動作成させる。ID自体が読めなければ再取得し、架空のIDを作らない。
4. 新しいrevision IDを取得できる環境では `writeControl.requiredRevisionId` 相当を使い、共同編集と競合したら再読込して差分を確認する。
5. 書込み後に同じIDのノート本文を再取得する。全スライドの原稿、図番号、出典、時間が対応しているかを確認する。

編集対象はノートのテキストであり、ノートマスターやページの配置を変更する手順にしない。[テキストの置換](https://developers.google.com/workspace/slides/api/guides/styling#replacing_text_within_a_shape)と[batchUpdate](https://developers.google.com/workspace/slides/api/reference/rest/v1/presentations/batchUpdate)も参照する。

## 図と配置の確認

全スライドのプレビュー、または連携から書き出したPDFを描画して確認する。中央見出し、左上の章名、黒と赤の文字、出典、画像の縦横比、改行、図の軸や凡例を点検する。スライドのプレビューではノートの保存は検証できないため、ノートはAPIや対応する読取り機能で別に確かめる。

段階表示は対応機能が確認できた場合に実装する。変換時のアニメーション保持を仮定しない。未対応の場合は同じ位置の図を使った連続スライドで説明順を再現し、各段階のノートを対応させる。見えない図についての説明や、存在しないクリックを原稿に残さない。

最終応答では確認したGoogle SlidesのURLを返す。Google Slides上で見た目やノートを確認できなかった場合は、その範囲を明記する。ローカルの構成確認とGoogle上での動作確認を混同しない。
