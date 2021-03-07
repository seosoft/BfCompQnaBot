# Bot アプリケーションに Q&A 機能を実装

[前のステップ](04_create_qnamaker_knowledgebase.md) で、ナレッジベースを作成、学習して Web サービスとして公開しました。

このステップでは、Bot アプリケーションに Q&A 機能を実装します。  

[1. QnA ダイアログの作成](#qna-ダイアログの作成)  
[2. QnA ダイアログへの切り替え](#qna-ダイアログへの切り替え)  
[3. Settings ファイルの編集](#settings-ファイルの編集)  
[4. Q&A ボットの動作確認](#qa-ボットの動作確認)

<br />

> アプリケーションの新規作成時に [**Create from knowledge base (QnA Maker)**] を選択することでも QnA Maker を利用した Q&A ボットを作成することもできます。この場合は、ナレッジベースの作成・管理も QnA Maker ではなくて、Bot Framework Composer を使用します。  
> 
> このハンズオンでは、より汎用的な操作方法で QnA Maker 以外の機能にも対応できるように、以下の手順で進めます。
>
> <img src="./images/05/bfcomp_create_from_kbbot.jpg" width="480px" />

<br />

---

## QnA ダイアログの作成

QnA Maker で作ったナレッジベースを呼び出すためのダイアログを作成します。

"MyQnaBot" の "Unknown intent" で QnA Maker を呼び出すこともできますが、今回は Q&A は独立した機能としてダイアログを作成することにします。

1. [**MyQnaBot**] プロジェクトで [**Add a dialog**] を選択して、QnA ダイアログを作成します。
   名前は "**Qna**" とします。

   <img src="./images/05/bfcomp_add_qna_dialog.jpg" width="540px" />
   <br />
   <img src="./images/05/bfcomp_qna_dialog_name.jpg" width="540px" />

2. [**Qna**] - [**BeginDialog**] で [**+**] - [**Access External Resources**] - [**Connect to QnA knowledgebase**] を選択します。

   <img src="./images/05/bfcomp_add_qna_action.jpg" width= "540px" />

---

## QnA ダイアログへの切り替え

ユーザーの入力を最初に受け取る "MyQnaBot" から、作成した "**Qna**" ダイアログにコンテキストを切り替えます。

オウム返し Bot では "**Unknown intent**" でユーザー入力をオウム返ししました。  
これを QnA Maker のナレッジベースを呼び出すように変更します。

1. "**MyQnaBot**" の "**Unknown intent**" を選択します。

2. [**Send a message**] アクションを削除します。

   <img src="./images/05/bfcomp_delete_action.jpg" width="540px" />

3. [**+**] - [**Dialog management**] - [**Begin a new dialog**] を選択します。

   <img src="./images/05/bfcomp_unk_trigger_begin_qna_dialog.jpg" width="540px" />

4. [**Begin a new dialog**] アクションを選択して、Property の [**Dialog name**] で "**Qna**" を選択します。

   <img src="./images/05/bfcomp_unk_trigger_dialog_name.jpg" width="540px" />

---

## Settings ファイルの編集

QnA Maker への接続情報は **Project Settings** に記述します。

1. Bot Framework Composer の [**Project Settings**] - [**MyQnaBot**] を選択します。

2. [**Advanced Settings View**] を有効化して "**qna**" セクションに [**QnA Maker を 発行した時の設定値**](04_create_qnamaker_knowledgebase.md) を設定します。  
  
  - knowledgebaseid
  - hostname
  - endpointKey

   <img src="./images/05/bfcomp_settings_qna.jpg" width="540px" />

> Settings から分かる通り、Bot Framework Compmoser では "Connect to QnA Knowledgebase" を利用した QnA Maker 利用は一つのナレッジベースのみ接続可能です。  
> 複数のナレッジベースを呼び出したい場合は "Send an HTTP Request" アクションを使うなどの工夫が必要です。

---

## Q&A ボットの動作確認

Bot アプリケーションから QnA Maker のナレッジベースを呼び出せるようになりました。

Bot Framework Emulator を使って動作確認します。

1. Bot Framework Composer の [**Build Bot**] または [**Rebuild Bot]** をクリックしてビルドします。

2. [**Test in Emulator**] で Emulator を起動します。

3. Bot Framework Emulator で動作確認します。  
   例えば "**サポートされる言語は何**" と入力して、ナレッジベースから適切な Answer が返ってくることを確認します。

   ![](./images/05/bfemu_test_qna.jpg)

4. "**ヘルプ**" と入力すると「Azure についての質問に答えます。質問を入力してください。」と応答することを確認します。  
   "ヘルプ" や "Help" を入力すると、すでに作成済みの "Help" ダイアログが応答していることが分かります。

---

以上で Bot アプリケーションに Q&A 機能を実装しました。

[Bot Framework Composer の基礎 - 2](03_composer_basic2.md) では、正規表現でユーザーの意図を認識しました。  
次のステップでは Bot アプリケーションで **LUIS** (Language UnderstandingLanguage Understanding) を利用して、ユーザーの意図を予測します。  

[前に戻る](04_create_qnamaker_knowledgebase.md) | [次に進む](06_composer_luis.md)  
[目次に戻る](../README.md)
