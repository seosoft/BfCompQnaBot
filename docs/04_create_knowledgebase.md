# ナレッジベース作成

[前のステップ](03_composer_basic2.md) までで Bot Framework Composer の基本的な操作を理解しました。

この手順では Bot Framework Composer 組み込みの機能でナレッジベースを作成します。

[1. QnA Maker の設定](#qna-maker-の設定)  
[2. ナレッジベースの作成](#ナレッジベースの作成)  
[3. ナレッジベースの編集](#ナレッジベースの編集)  
[4. QnA の発行](#qna-の発行)

> ナレッジベースとして [**Surface の保証: よくある質問**](https://support.microsoft.com/ja-jp/surface/surface-%E3%81%AE%E4%BF%9D%E8%A8%BC-%E3%82%88%E3%81%8F%E3%81%82%E3%82%8B%E3%81%94%E8%B3%AA%E5%95%8F-1217913a-2692-424e-a5c4-0eb0de84f05a) を利用します。  
>
> <img src="./images/04/surface_warrantyfaq_page.jpg" width="400px" />

QnA Maker のナレッジベースは、QnA Maker ポータルで作成して Composer から接続する方法もあります。  
これについては [付録](./ap01_create_qnamaker_kb.md) で手順を紹介します。

---

## QnA Maker の設定

Bot Framework Composer の設定画面で QnA Maker のセットアップを行います。

1. [**Configure**] - [**Development resources**] を開いて [**Set up QnA Maker**] をクリックします。  
   
   <img src="./images/04/bfcomp_setup_qnamaker.jpg" width="480px" />

2. [**Create and configure new Azure Resources**] を選択して [Next] を選択します。  
     
   <img src="./images/04/bfcomp_create_qna_resource.jpg" width="400px" />

3. Azure の認証を求められたらサインインします。
4. QnA Maker のリソースを作成する Azure アカウントとサブスクリプションとを選択します。  
   
   <img src="./images/04/bfcomp_select_qna_subscription.jpg" width="400px" />

5. リソースグループ、リージョン、価格プランを入力・選択します。続いて [Next] をクリックします。   
   
   |項目名|値|
   |---|---|
   |Azure resource group|ドロップダウンを開いて [+ Create new] を選択|
   |Resource group name|任意の名前で新規作成 (上で "Create new" するまでは非表示)|
   |Region|West US|
   |QnA Maker resouce name|任意の名前で新規作成|
   |Pricing tier|任意|
   
   <img src="./images/04/bfcomp_set_qna_name.jpg" width="400px" />

6. しばらく待つと QnA Maker のリソースが作成されます。  
   リソース作成に成功するとキーが取得されて [QnA Maker Subscription key] に自動的に表示されます。  

   <img src="./images/04/bfcomp_qna_key.jpg" width="400px" />

---

## ナレッジベースの作成

Web ページをインポートしてナレッジベースを作成します。

1. Composer のナビゲーションで [**Knowledge base**] を選択して [**Create new KB**] をクリックします。  

   <img src="./images/04/bfcomp_create_kb.jpg" width="400px" />

2. [**Add Qna Maker knowledge base**] でナレッジベースの名前（任意）を入力して、[**FAQ website (source)**] に FAQ ページのアドレスを入力します。  
   今回は "https://support.microsoft.com/ja-jp/surface/surface-%E3%81%AE%E4%BF%9D%E8%A8%BC-%E3%82%88%E3%81%8F%E3%81%82%E3%82%8B%E3%81%94%E8%B3%AA%E5%95%8F-1217913a-2692-424e-a5c4-0eb0de84f05a" と入力します。

   > [Surface の保証: よくあるご質問](https://support.microsoft.com/ja-jp/surface/surface-%E3%81%AE%E4%BF%9D%E8%A8%BC-%E3%82%88%E3%81%8F%E3%81%82%E3%82%8B%E3%81%94%E8%B3%AA%E5%95%8F-1217913a-2692-424e-a5c4-0eb0de84f05a)
   
   <img src="./images/04/bfcomp_add_kb.jpg" width="540px" />

3. 少し待つとナレッジベースが作成されます。  
   
   <img src="./images/04/bfcomp_kb_created.jpg" width="540px" />

   > ナレッジベース作成時に先頭の数個だけ表示されて全体の作成には失敗していることがあります。  
   > この場合は [**Delete knowledge base**] または [**Import new URL and overwrite**] でナレッジベースを作成しなおします。  
   >
   > <img src="./images/04/bfcomp_delete_kb.jpg" width="400px" />


---

## ナレッジベースの編集

Q&A の内容を確認して、必要に応じて質問や回答の文言を修正・追加・削除します。  
実際に次の操作でナレッジベースを編集してみます。

> ここで使用する FAQ ページの内容は随時更新されます。Q&A の内容が以下とは異なるかもしれません。  
> その場合は以下の操作を参考に適宜適切な編集をしてください。

1. 不要な Q&A ペアを [ごみ箱] アイコンで削除します。  
   ここでは先頭の Q&A ペアが適切ではないので削除します。 (ページ表示コントロールのスクリプト部分を回答として認識しています)

   <img src="./images/04/bfcomp_delete_qapair.jpg" width="480px" />

2. この後のステップで利用する質問を追加します。  
   ひとつの回答に対して複数の質問を定義する形にします。

   > ここで追加する質問は Help メッセージの追加の応答として **Suggested Action** で利用します。

   |追加箇所|追加の質問|
   |---|---|
   |使用中のデバイスの保証契約条件は、どこで確認することができますか? - 保証に関してよく寄せられる質問|保証内容を確認|
   |サポートに連絡する方法を教えてください。 - サービスに関してよく寄せられる質問|サポートに連絡|

   <img src="./images/04/bfcomp_add_qna_phrase1.jpg" width="480px" />
   <img src="./images/04/bfcomp_add_qna_phrase2.jpg" width="480px" />

---

以上で、ナレッジベースを作成して。

次のステップでは、ここで開発したナレッジベースを呼び出す機能を Bot アプリケーションに追加します。

[前に戻る](03_composer_basic2.md) | [次に進む](05_composer_qna.md)  
[目次に戻る](../README.md)
