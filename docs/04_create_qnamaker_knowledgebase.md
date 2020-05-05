# QnA Maker でナレッジベース作成

[前のステップ](03_composer_basic2.md) までで Bot Framework Composer の基本的な操作を理解しました。

以下の手順では一旦 Bot Framework Composer を離れて、[**QnA Maker**](https://www.qnamaker.ai/) で Bot で使うナレッジベースを作成します。

[1. QnA Maker リソースの作成](#qna-maker-%e3%81%a7%e3%83%8a%e3%83%ac%e3%83%83%e3%82%b8%e3%83%99%e3%83%bc%e3%82%b9%e4%bd%9c%e6%88%90)  
[2. ナレッジベースの作成](#%e3%83%8a%e3%83%ac%e3%83%83%e3%82%b8%e3%83%99%e3%83%bc%e3%82%b9%e3%81%ae%e4%bd%9c%e6%88%90)  
[3. ナレッジベースのトレーニングとテスト](#%e3%83%8a%e3%83%ac%e3%83%83%e3%82%b8%e3%83%99%e3%83%bc%e3%82%b9%e3%81%ae%e3%83%88%e3%83%ac%e3%83%bc%e3%83%8b%e3%83%b3%e3%82%b0%e3%81%a8%e3%83%86%e3%82%b9%e3%83%88)  
[4. QnA の発行](#qna-%e3%81%ae%e7%99%ba%e8%a1%8c)

> ナレッジベースとしては [**Azure サポートに関する FAQ**](https://azure.microsoft.com/ja-jp/support/faq/) を利用します。  
> QnA Maker を使うと、このようなページの Q&A を取り込んでナレッジベースにすることができます。
>
> <img src="./images/04/azure_support_page.jpg" width="400px" />

---

## QnA Maker リソースの作成

QnA Maker のリソースを Azure ポータルで作成します。

1. [**QnA Maker**](https://www.qnamaker.ai/) にサインインします。

   <img src="./images/04/qna_signin.jpg" width="480px" />

2. [**Create a knowledge base**] をクリックします。

   <img src="./images/04/qna_create_kb.jpg" width="480px" />

3. [**Create a QnA service**] をクリックします。  
   なお QnA Maker のタブは **閉じずにそのまま開いて** おきます。

   <img src="./images/04/qna_create_qna_service.jpg" width="480px" />

4. 自動的に Azure ポータルが開くので、以下の入力・選択をして QnA Maker を作成します。

   |項目名|値|
   |---|---|
   |名前|任意|
   |サブスクリプション|任意|
   |価格レベル|任意。選択可能ならハンズオンの範囲では F0|
   |リソースグループ|任意の名前で新規作成|
   |Azure Search 価格レベル|任意。選択可能ならハンズオンの範囲では F|
   |アプリ名|任意。固有の名前が必要なので、例えば "AzureFaq" に自分の名前や日付などを付けたもの|

   <br />
   <img src="./images/04/azure_create_qna.jpg" width="560px" />

5. 作成したリソースグループを開いて "**App Service プラン**" を選択します。

   <img src="./images/04/azure_rg.jpg" width="560px" />

6. App Service プランが表示されたら [**スケールアップ**] を選択します。  
   続いて [**開発/テスト**] - [**F1**] を選択して最後に [**適用**] をクリックします。

   <img src="./images/04/azure_appsrv_plan_to_f1.jpg" width="540px" />

以上で、Azure ポータルでの手順は終了です。  
続いて QnA Maker に戻ってナレッジベースを作成します。

---

## ナレッジベースの作成

Azure で作成した QnA Maker のリソースに、QnA Maker で接続してナレッジベースを作成します。

1. QnA Maker のタブに戻ります。

2. "STEP 2" の [**Refresh**] をクリックします。  
   すぐ前の手順で作ったばかりの QnA Maker のリソースを選択します。  
   [**Language**] は "**Japanese**" を選択します。

   <img src="./images/04/qna_select_resource.jpg" width="540px" />

3. "STEP 3" では任意の名前を付けます。ここでは "**Azure QnA**" とします。

4. "STEP 4" の [**URL**] には "**https://azure.microsoft.com/ja-jp/support/faq/**" と入力します。  
   [Chit-chat] は今回は "None" のままにします。

   <img src="./images/04/qna_populate_kb.jpg" width="540px" />

   > "Chit-chat" は応答にキャラクター付けするものですが、今回は何もしません。

5. このページの一番下の [**Create your KB**] をクリックして、ナレッジベースを作成します。

   <img src="./images/04/qna_create_kb_button.jpg" width="540px" />

6. ナレッジベースが作成されると [EDIT] 画面に遷移します。  

   <img src="./images/04/qna_kb_created.jpg" width="540px" />

> 一般にはここで、正しく質問と回答とが取り込めているかを確認します。  
> 今回は正しく取り込めることが分かっているサイトなので特に何もしません。  
>
> 必要に応じて、内容を確認したり、質問・回答の文言を修正したりします。

---

## ナレッジベースのトレーニングとテスト

QnA Maker 内に Q&A を取り込んでナレッジベースを作成できたので、これをトレーニングします。  
さらに品質を確認するために QnA Maker ポータル内でテストします。

1. [**Save and train**] をクリックして、ナレッジベースのトレーニングを始めます。

   <img src="./images/04/qna_save_and_train.jpg" width="540px" />

2. トレーニングが終了したら、[**Test**] をクリックします。  
   テストクライアントが表示されたら何か質問（入力）して、回答を
   確認します。

   例えば、以下のような質問をしてみます。

   ```txt
   サポートされる言語は何
   サポートプラン
   ```

   <img src="./images/04/qna_test.jpg" width="540px" />

3. （オプション）回答の品質を数値でチェックしたい場合、または最適ではない回答を返してくる場合などは、[**Inspect**] をクリックすることで回答の詳細を確認・変更できます。

   <img src="./images/04/qna_test_inspect.jpg" width="540px" />

---

## QnA の発行

1. QnA Maker で [**PUBLISH**] - [**Publish**] を選択します。

   <img src="./images/04/qna_publish.jpg" width="540px" />

2. 発行に成功すると Web サービスの設定値が表示されます。  
   これらの値をメモしておきます。

   |項目名|メモする値|
   |---|---|
   |Knowledge Id|1行目の "/knowledgebases/" と "/generateAnswer" の間の値
   |Host|2行目の "https://～/qnamaker"|
   |Endpoint Key|3行目全部|

   <img src="./images/04/qna_published_settings.jpg" width="540px" />

---

以上でナレッジベースを学習して Web サービスとして公開しました。  

次のステップでは、Bot アプリケーションに、ここで開発したナレッジベースを呼び出す機能を追加します。

[前に戻る](03_composer_basic2.md) | 次に進む  
[目次に戻る](../README.md)
