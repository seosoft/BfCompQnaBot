# 開発環境の構築

ハンズオンの最初に [**Bot Framework Composer**](https://docs.microsoft.com/ja-jp/composer/) で Bot 開発のための環境を構築します。

このハンズオンでは、[**Bot Framework Composer v2.0.0**](https://techcommunity.microsoft.com/t5/azure-ai/build-2021-conversational-ai-update/ba-p/2375203) を使用します。  
ハンズオン実施の時期によっては画面の構成などが一部異なる可能性があります。

> Bot Framework Composer は [ソースコードからビルドする](https://docs.microsoft.com/ja-jp/composer/install-composer#build-composer-from-source) も紹介します。  
> 不具合修正や機能追加・変更が、アプリケーション版より早いタイミングで行われる可能性があります。  
興味がある方はソースコードからビルドする方法を検討してください。

---

## デスクトップアプリケーション版をインストール

Bot Framework Composer を使用するには、構築が簡単なデスクトップアプリケーション版をお勧めします。  
Windows 版、macOS 版、Linux 版が用意されています。

1. **Bot Framework Emulator インストール**  
   [**Bot Framework Emulator**](https://github.com/microsoft/BotFramework-Emulator/releases) をダウンロードしてインストールします。  

   <img src="./images/01/bfemu_install_01.jpg" width="400px" />
   <br />
   <img src="./images/01/bfemu_install_02.jpg" width="400px" />

   Bot Framework Emulator は Bot 開発の **テスト用クライアント** として使用します。

2. **.NET Core 3.1 SDK インストール**  
   [**.NET Core 3.1 SDK**](https://dotnet.microsoft.com/download/dotnet-core/3.1) をダウンロードしてインストールします。

   <img src="./images/01/dncore_install_01.jpg" width="400px" />
   <br />
   <img src="./images/01/dncore_install_02.jpg" width="400px" />

3. **Bot Framework Composer インストール**  
   使用している OS にあわせて、**Bot Framework Composer** のインストーラーをダウンロードしてインストールします。

   |OS|インストーラーのアドレス|
   |---|---|
   |Windows|[https://aka.ms/bf-composer-download-win](https://aka.ms/bf-composer-download-win)|
   |macOS|[https://aka.ms/bf-composer-download-mac](https://aka.ms/bf-composer-download-mac)|
   |Linux|[https://aka.ms/bf-composer-download-linux](https://aka.ms/bf-composer-download-linux)|

   <img src="./images/01/bfcomp_install_01.jpg" width="480px" />
   <br />
   <img src="./images/01/bfcomp_install_02.jpg" width="480px" />

4. **Bot Framework Composer 起動確認**  
   確認のために Bot Framework Composer を起動します。

   <img src="./images/01/bfcomp_start.jpg" width="540px" />

5. **ngrok インストール**  
   [**ngrok**](https://ngrok.com/download) をダウンロードして、ZIP ファイル内の "ngrok.exe" をローカル PC の任意のフォルダーにコピーします。  
   インストーラーはないので exe ファイルをコピーするだけです。パスが通ったフォルダーでなくてもかまいません。  

   ngrok は [ステップ 6](06_composer_luis.md) までの Bot アプリケーション開発の範囲では不要です。  
   [ステップ 7](07_deploy_to_azure.md) で Bot アプリケーションを Azure に発行したあとの動作確認に使用します。

   > Bot Framework Composer で開発する場合、以下のケースで ngrok が必要になります。
   > - Azure に発行した Bot アプリケーションを Bot Framework Emulator でテストしたい場合
   > - ローカルで実行している Bot アプリケーションに他のマシンから接続したい場合

以上で、Bot アプリケーション開発環境の構築は完了です。  

---

以上で、Bot Framework Composer のインストールが完了しました。  
次のステップでは、Bot Framework Composer 操作の超基礎を理解するために、Echo Bot を作ります。

[次に進む](02_composer_basic.md)  
[目次に戻る](../README.md)
