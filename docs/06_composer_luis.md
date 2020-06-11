# LUIS でユーザーの意図を予測

[前のステップ](05_composer_qna.md) で、QnA Maker を使った Q&A 機能を Bot アプリケーションに 追加しました。

このステップでは、[LUIS (Language Understanding)](https://azure.microsoft.com/ja-jp/services/cognitive-services/language-understanding-intelligent-service/) を使って、ユーザーの意図を予測するように変更します。  
（[Bot Framework Composer の基礎 - 2](03_composer_basic2.md) では、正規表現でユーザーの意図を認識しました）

[1. LUIS 利用の準備 (Settings ファイルの変更)](#luis-%e5%88%a9%e7%94%a8%e3%81%ae%e6%ba%96%e5%82%99-settings-%e3%83%95%e3%82%a1%e3%82%a4%e3%83%ab%e3%81%ae%e5%a4%89%e6%9b%b4)  
[2. Recognizer Type の変更](#recognizer-type-%e3%81%ae%e5%a4%89%e6%9b%b4)  
[3. help Trigger のフレーズの入力](#help-trigger-%e3%81%ae%e3%83%95%e3%83%ac%e3%83%bc%e3%82%ba%e3%81%ae%e5%85%a5%e5%8a%9b)  
[4. LUIS への接続と Bot の再起動](#luis-%e3%81%b8%e3%81%ae%e6%8e%a5%e7%b6%9a%e3%81%a8-bot-%e3%81%ae%e5%86%8d%e8%b5%b7%e5%8b%95)  
[5. Bot Framework Emulator で動作確認](#bot-framework-emulator-%e3%81%a7%e5%8b%95%e4%bd%9c%e7%a2%ba%e8%aa%8d)  

LUIS (Language Understanding) とは、自然言語の入力に対して、

- 全体の意味を予測
- 関連性のある詳細な情報を引き出す

サービスです。  

このハンズオンでは、ヘルプを呼び出す範囲で LUIS を使用するだけなので効果が実感しづらいですが、実装手順を理解することを目的とします。

> "Language Understanding" はプレビューでは "LUIS" と呼ばれていました。  
> GA して Language Understanding と名称が変わりましたが、ドキュメントやライブラリにも LUIS という表記が残っていたり、サービスが GA した後も LUIS と呼ばれることが多くあります。

> Bot Framework Composer v1.0.1 では日本語対応した LUIS アプリケーションは作成されません。  
> 必ず "en-us" になります。  
>
> 以下では、今後の日本語対応を見越した手順を記載しています。

---

## LUIS 利用の準備 (Settings ファイルの変更)

Bot Framework Composer は、デフォルトの言語が "**en-us**" です。  
すでに確認したように、このままでも日本語を問題なく利用できますが、LUIS を利用するにはまず言語の変更しておく必要があります。  
手順を忘れることがないように最初に行っておきます。

1. Bot Framework Composer で [**Settings**] - [**Bot Settings**] を選択します。

2. [**luis**] セクションの [**defaultLanguage**] を "**ja-jp**" に変更します。  

   > あとで動作確認した際に Help Intent に該当する入力を正しく処理できない場合は、"**en-us**" に戻してみてください。

   <img src="./images/06/bfcomp_settings_luis.jpg" width="540px" />

3. ここで一緒に [**luis**] -[**name**] を "**MyQnaBot**" に変更しておきます。（必須ではありません）

---

## Recognizer Type の変更

"MyQnaBot" の **Recognizer Type** (＝ユーザー意図の識別方法) は、[Bot Framework Composer の基礎 - 2](03_composer_basic2.md) では "Regular Expression" にしました。

ここで "**LUIS**" に変更して、もう少し自然な言語処理でユーザー意図を識別するように変更します。

1. [**Design Flow**] - [**MyQnaBot**] を選択して、Property の [**Recognizer Type**] を "**LUIS**" に変更します。

   ![](./images/06/bfcomp_set_rectype.jpg)

> LUIS は、このハンズオンで利用するよりもさらに高度な言語処理が可能です。  
> このハンズオンでは LUIS 利用方法を理解するために手順に組み込みました。

---

## help Trigger のフレーズの入力

help ダイアログにコンテキストを切り替える契機となるフレーズを入力します。

1. "**MyQnaBot**" の "**Help**" Trigger を選択します。

2. Property の [**Trigger Phrases**] に以下の入力をします。

   ```txt
   - help
   - ヘルプ
   - このBotの使い方
   - ボットの機能
   ```

   ![](./images/06/bfcomp_help_trigger_phrases.jpg)

   "Trigger Phrases" では、類義語を登録したり、英語・日本語を組み合わせると認識精度が上がることがあります。  
   例えば  

   - "使い方" と "機能"
   - "help" と "ヘルプ"
   - "Bot" と "ボット"  

   などです。  
   こうすると、"このボットの使い方" や "Botの機能を教えて" などの表現の揺らぎを吸収してくれます。

   > Bot Framework Composer v1.0.1 では、上記の日本語対応ができていません。  
   > このあとの操作では必ず "en-us" の LUIS アプリケーションが作成されます。
   >
   > Preview では "ja-jp" の LUIS アプリケーションを生成できていたため、今後修正されるものと考えて上記の手順を記載しています。

3. [**Condition**] に以下の入力をします。

   ```txt
   #Help.Score > 0.8
   ```

   ユーザーの入力が "Help" インテントである可能性が 80% より高い場合に Help ダイアログにコンテキストを切り替えることを意味します。  
   それ以下の場合は、ユーザーの入力は "Unknown intent" で処理されるので、Qna ダイアログに切り替えられます。

   ![](./images/06/bfcomp_help_trigger_condition.jpg)

---

## LUIS への接続と Bot の再起動

Bot アプリケーションを LUIS に接続して Bot 再起動します。

1. ブラウザーで [**LUIS**](https://www.luis.ai/) に接続してログイン（またはサインイン）します。

2. [**User Settings**] - [**Settings**] を選択します。

   ![](./images/06/luis_user_settings_1.jpg)
   ![](./images/06/luis_user_settings_2.jpg)

3. [**Starter_Key**] セクションの [**Primary Key**] をクリップボードにコピーします。  
   この後すぐに使います。

   ![](./images/06/luis_user_settings_3.jpg)

4. Bot Framework Composer に戻って、[**Start Bot**] または [**Restart Bot**] をクリックします。

5. [**Publish LUIS models**] ダイアログが開いたら、[**LUIS Primary Key**] に LUIS ポータルでコピーした "Primary Key" を貼り付けて、[**OK**] をクリックします。

   ![](./images/06/bfcomp_publish_luis_models.jpg)

6. [**Test in Emulator**] が表示されれば、LUIS への発行と Bot の再起動が完了しています。

   > "ja-jp" の LUIS アプリケーションを生成できるようになると、例えば「このボットの使い方」のような入力でも Help Intent で処理されるようになります。  
   > Bot Framework Composer 1.0.1 では "en-us" の LUIS アプリケーションのみ生成されます。

---

## Bot Framework Emulator で動作確認

1. Bot Framework Emulator で何か入力してみます。

   - ヘルプ
   - サポートされる言語は何

   など、LUIS または QnA Maker で処理されます。

   ![](./images/06/bfemu_test_qna_and_luis.jpg)

---

以上で LUIS と QnA Maker とを組み合わせて利用できるようになりました。  
Q&A Bot アプリケーションを開発は完了です。

次のステップでは、作成したアプリケーションをクラウドに発行します。

[前に戻る](05_composer_qna.md) | [次に進む](07_deploy_bot.md).md)  
[目次に戻る](../README.md)
