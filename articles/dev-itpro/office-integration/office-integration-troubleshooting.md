---
title: "Office 統合のトラブルシューティング (タスク ガイド)"
description: "このトピックでは、Microsoft Office 統合の機能に関する質問、ヒント、およびトラブルシューティング情報への回答を示します。 説明されている質問と問題は、ユーザー、管理、および開発のシナリオにわたっています。"
author: ChrisGarty
manager: AnnBe
ms.date: 03/01/2018
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-platform
ms.technology: 
ms.search.form: OfficeAppParameters, SysEmailParameters
audience: Developer, IT Pro
ms.reviewer: sericks
ms.search.scope: Core, Operations
ms.custom: 72263
ms.assetid: 89588fed-b47f-4f01-9328-325518f016d6
ms.search.region: Global
ms.author: cgarty
ms.search.validFrom: 2016-02-28
ms.dyn365.ops.version: AX 7.0.0
ms.translationtype: HT
ms.sourcegitcommit: 879eb9f2a63a8514791f74965005ed3e22bc0de7
ms.openlocfilehash: 1c180f95e217be09c57bc50b8cda84d302dadd2b
ms.contentlocale: ja-jp
ms.lasthandoff: 04/20/2018

---

# <a name="troubleshoot-the-office-integration"></a>Office 統合のトラブルシューティング (タスク ガイド) 

[!include [banner](../includes/banner.md)]

このトピックでは、Microsoft Office 統合の機能に関する質問、ヒント、およびトラブルシューティング情報への回答を示します。 説明されている質問と問題は、ユーザー、管理、および開発のシナリオにわたっています。

## <a name="frequently-asked-questions"></a>よく寄せられる質問

### <a name="what-platforms-do-the-office-add-ins-support"></a>Office アドインはどのようなプットフォームをサポートしますか ?

Microsoft Excel アドインと Microsoft Word アドインは、Office Web/JavaScript アドイン フレームワークを使用して構築されます。 このフレームワークは最初は Microsoft Office 2013 用にリリースされましたが、Microsoft Office 2016 では重要な更新が行われました。 詳細については、[Office アドイン ホストおよびプラットフォームの可用性](http://dev.office.com/add-in-availability) を参照してください。 Excel アドインには ExcelAPI 1.2 が必要です。 したがって、Excel アドインをサポートするプラットフォームを判断するには、[[Office アドイン ホストおよびプラットフォームの可用性](http://dev.office.com/add-in-availability)] マトリックスを使用します。 多くのユーザーにとって、語句「Excel 2016 と最新の更新」で十分です。

### <a name="are-the-office-add-ins-safe"></a>Office アドインは安全ですか。

マルウェア、完全な接続、およびコンプライアンス リスクがあるうちは、完全に安全なものはありません。 ただし、他の Web サイトと同様、Web アドインは基本的に、制限のあるアプリケーション プログラミング インターフェイス (API) 経由で Office クライアント製品と対話する Web アプリケーションです。 詳細については、[Office アドインで何ができますか](https://dev.office.com/docs/add-ins/overview/office-add-ins#what-can-an-office-add-in-do) を参照してください

### <a name="does-the-excel-add-in-support-office-for-mac"></a>Excel アドインは Mac のために Office をサポートしますか。

一連番号 Apple Mac および iOS のサポートは、現在開発中です。 Office JavaScript (JS) API は、特に認証に関しては、Apple Safari と Internet Explorer で動作が異なります。 Office JS API のプラットフォーム サポートの詳細については、[Office アドイン ホストおよびプラットフォームの可用性](http://dev.office.com/add-in-availability) を参照してください。

### <a name="what-version-of-office-is-required-for-the-excel-add-in-to-support-ad-fs"></a>Excel アドインが AD FS をサポートするために必要な Office のバージョンとは

詳細については、このトピックで後述する「問題のトラブルシューティング」セクションを参照してください。

### <a name="how-can-i-force-an-update-of-office"></a>どのように Office の更新を強制できますか。

Office ビルドが更新されない場合、遅延したトラックにある場合があります ([Microsoft Office 365 ProPlus 更新チャネル オプション](https://technet.microsoft.com/en-us/library/mt455210.aspx))。 この場合、[Office 配置ツールを使用して現在のチャネルに移動する](https://technet.microsoft.com/en-us/library/jj219422.aspx?f=255&MSPPError=-2147217396) を使用するか、最新の更新プログラムがあることを保証するために [Office Insider プログラム](https://products.office.com/en-us/office-insider) にサインアップできます。 最も簡単な方法は、Office 配置ツールを使用して現在のチャネルに切り替えることです。 この場合、最新の更新プログラムはすぐにインストールされます。

### <a name="why-cant-you-tell-me-what-version-of-office-or-excel-a-particular-issue-is-fixed-in"></a>どのバージョンの Office または Excel で特定の問題が修正されたか知ることができないのはなぜですか。

Office には、多くのリリースがあります。 これらのリリースは、さまざまな時刻にアップデートを受け取り、対応しないさまざまなバージョン番号を持ちます。 頻繁に使用されるいくつかのバージョンの Office および更新メソッドは、Click to Run (C2R) Current channel、C2R Deferred、C2R First Update Deferred、Office Insider Fast、Office Insider Slow、MSI/MSO (DVD からインストール) です。 Office バージョンの詳細については、[Office 365 クライアント更新チャンネルのリリース](https://technet.microsoft.com/en-us/office/mt465751?f=255&MSPPError=-2147217396) ページを参照してください。

### <a name="why-am-i-having-trouble-signing-into-the-excel-add-in"></a>Excel アドインへのサインインに問題が生じるのはなぜですか。

Excel アドインは、Internet Explorer ウィンドウ内で動作します。 既定では、Excel アドインは Internet Explorer から保存されている資格情報を取得し、保存されている資格情報がない場合には Internet Explorer が現在の Microsoft Windows の資格情報を提供します。 適切な資格情報を使用してサインインしていることを確認します。 Excel アドインで、明示的にサインアウトしてから、適切な資格情報が使用されていることを保証するためにサインインします。

### <a name="the-excel-add-in-seems-to-be-slow-when-it-publishes-records-how-can-i-learn-more-about-what-is-occurring"></a>レコードを発行するとき、Excel アドインが遅くなったように見えます。 何が起こっているかについてもっと知るにはどうすればいいですか。

Excel アドインが実行する作業のほとんどは、サーバーで発生させる必要があります。 時間が費やされている場所を知るには、[[Fiddler (無償ダウンロード)](http://www.telerik.com/fiddler)] を使用して Excel アドインが期待通りに機能することを確認してください。

Excel アドインは、公開されているレコードを要求として送信します。 これらのレコードが処理されると、サーバーから応答が送信されます。 次に、Excel アドインは公開するレコードの次のセットを含む別のメッセージを作成し、その要求を送信します。 Excel アドインでは、サーバーからの以前の応答から、サーバーへの次の要求の間での処理時間に 5 から 10 秒を要します。

Excel アドインとサーバー/サービスの処理時間の関係を確認するには、次の手順を実行します。

1. [Fiddler](http://www.telerik.com/fiddler) を起動します。 
2. プロセスをテストするいくつかのレコードを公開します。
3. Fiddler でその要求と応答を表示できることを確認します ([HTTPS トラフィックが復号化されていることを確認します](http://docs.telerik.com/fiddler/Configure-Fiddler/Tasks/DecryptHTTPS))。
4. 多数のレコードを公開します。 
5. Fiddler では、要求から応答までに必要な時間と、応答から次の要求までに必要な時間を監視します。

    - 要求から応答までの時間が長い場合、ボトルネックはサーバー/サービスです。
    - 次の要求への応答時間が大きい場合は、ボトルネックは Excel アドイン (つまり、クライアント) です。

### <a name="why-is-the-export-to-excel-functionality-limited-to-10000-records"></a>Excel へのエクスポート機能が 10,000 レコードに制限されているのはなぜですか。

Excel へのエクスポート機能は 10,000 レコードに制限されています。 エクスポート処理では、フォーマットされた値、計算された値、および一時テーブルのデータなど、取得できないフィールドとデータを次のレコードに提供するために、データのエクスポート元のフォームが使用されるため、この制限があります。 フォームが使用されているということは、特定のコンピューターのすべてのユーザーが共有するクライアントプロセス内でエクスポートが行われることを意味します。 エクスポート中に、他のユーザーはクライアントとの対話をブロックされます。 

理想的な代替は、[Excel で開く] と Excel アドインを使用することです。 Excel アドインは、OData サービスを使用してデータを取得し、エンティティが提供するセキュリティを活用します。 データ管理フレームワーク (DMF)/データ インポート/エクスポート フレームワーク (DIXF) のインポートおよびエクスポート機能も使用できます。 ただし、DMF/DIXF は、多くの場合管理者に限定されます。 

ユーザーが Excel アドイン経由でデータにアクセスすることに懸念がある場合、レコードを更新できないようにする必要があるため、次の点を考慮します。 

- エンティティには、フォームにあるすべての検証とロジックが必要です。 所有していない場合は、バグです。 
- エンティティが保護される方法は、フォームが保護される方法と似ています。 したがって、ユーザーがそのデータを公開するフォームを使用してデータを更新または書き込みする権限を持っていない場合、ユーザーはそのデータを公開するエンティティを使用してデータを更新または書き込みする権限を持つべきではありません。 

## <a name="why-is-the-publish-button-in-the-excel-add-in-unavailable"></a>Excel アドインで公開ボタンが利用できないのはなぜですか。 

エンティティにデータを公開するには、すべてのキーおよび必須フィールドが存在する必要があります。 バインドにフィールドを追加するようにデザインを編集してみてください。 

## <a name="troubleshooting-issues"></a>問題のトラブルシューティング

### <a name="fixed-issue-during-sign-in-to-the-excel-add-in-i-receive-the-following-error-message-aadsts65001-the-user-or-administrator-has-not-consented-to-use-the-application-with-id-xyz"></a>\[固定\] 問題: Excel アドインへのサインイン中に、次のエラー メッセージが表示されます: 「AADSTS65001: ユーザーまたは管理者が ID XYZ のアプリケーションを使用することに同意していません」

**問題:** Excel アドインへのサインイン中に、次のエラー メッセージが表示されます。「AADSTS65001: ユーザーまたは管理者が ID XYZ でアプリケーションを使用することに同意しませんでした」。

**説明:** 通常、この問題は、Microsoft Azure Active Directory (Azure AD) が Excel アドインを表す Azure AD アプリケーションを検出できないために発生します。 その問題は、[Microsoft Power BI のコンフィギュレーション](../analytics/configure-power-bi-integration.md)中、アプリケーション ID URI が環境 URL に設定された Azure AD アプリケーションが追加されたために発生します。 

**修正:** Azure AD アプリケーションのアプリケーション ID URI が環境 URL に設定されていないことを確認します。 アプリ ID URI は、`https://contosoAXPowerBI` などの固有の URI で作成する必要があります。

### <a name="fixed-issue-during-sign-in-to-the-excel-add-in-i-receive-the-following-error-message-aadsts50001-the-application-named-abc-was-not-found-in-the-tenant-named-xyz"></a>\[固定\] 問題: Excel アドインへのサインイン中に、次のエラー メッセージが表示されます: 「AADSTS50001: ABC という名前のアプリケーションが XYZ という名前のテナントに見つかりませんでした」

**問題:** Excel アドインへのサインイン中に、次のエラー メッセージが表示されます。「AADSTS50001: XYZ という名前のテナントに ABC という名前のアプリケーションが見つかりませんでした」。

**説明:** この問題は、配置システムのエラーにより、環境がテナントのサービス プリンシパルのコンフィギュレーション済の一覧に追加されていない URL を取得したために発生している可能性があります。 

**修正:** 環境に関するサポート問題を提出し、問題を調査し、コンフィギュレーションを調整できるようにします。

### <a name="fixed-issue-after-the-excel-add-in-starts-and-updates-data-i-receive-the-following-error-message-an-error-occurred-while-writing-to-the-data-cache"></a>\[固定\] 問題: Excel アドインが起動してデータを更新した後、次のエラー メッセージが表示されます: 「データ キャッシュへの書き込み中にエラーが発生しました」

**問題:** Excel アドインを開始してデータを更新すると、次のエラー メッセージが表示されます。「データ キャッシュに書き込み中にエラーが発生しました」。 エラー状態の詳細は次の通りです。「引数が無効または不足している、またはフォーマットが正しくありません」 

**説明:** クライアントを Internet Explorer で開いていて、ユーザーが **Excel で開く**オプションを選択した直後に、**開く**をクリックすると、このエラー メッセージが表示されます。 Internet Explorer が一時的なインターネット ファイルを処理する方法は、Excel で問題を引き起こします。 この問題は、API 呼び出しの失敗の原因となります。 

**回避策:** Internet Explorer でブックを開く際、まず**保存**をクリックし、それから**開く**をクリックしてください。 ファイルはダウンロード フォルダーから開かれます。 別の方法として、Edge または Google Chrome ブラウザを使用します。 既定では、これらの両方のブラウザはファイルをダウンロード フォルダに保存します。 したがって、問題は発生しません。 

**長期的な修正プログラム:** Office チームと協力してこの問題を理解し、Excel で解決できるようにしています。

### <a name="issue-when-i-send-email-by-using-smtp-the-server-response-is-5760-smtp-client-does-not-have-permissions-to-send-as-this-sender"></a>問題: SMTP を使用して電子メールを送信したとき、サーバーからの応答が「5.7.60 SMTP。クライアントにはこの送信者として送信する権限がありません」となります

**問題:** SMTP (Simple Mail Transfer Protocol) を使用して電子メールを送信すると、サーバーの応答として「5.7.60 SMTP; クライアントにこの送信者として送信するアクセス許可がありません」というエラー メッセージが表示されることがあります。 または、「レポートの生成中に問題が発生しました。」 というエラー メッセージの状態かもしれません。

**説明:** この問題は、通常、電子メール アカウントの送信者アクセス許可が正しく設定されていないために発生します。 

**修正:** Office 365 管理者センター (portal.office.com/Admin) で送信者アクセス許可をコンフィギュレーションすることができます。 **ユーザー** > **有効なユーザー** > **ユーザー** > **メールボックスのアクセス許可を編集** > **このメールボックスから電子メールを送信する**の順にクリックします。 詳細については、[Office 365 - 管理者ヘルプで別のユーザーにメールボックスのアクセス許可を付与する](https://support.office.com/en-us/article/Enable-sending-email-from-another-user-s-mailbox-in-Office-365-2B828C5F-41AB-4904-97B9-3B63D8129C4E) を参照してください。 

次の図は、**電子メール パラメーター** ページでの SMTP の設定を示しています。 ここで、送信メール サーバー、ポート、ユーザー名、パスワード、および Secure Sockets Layer (SSL) の要件を指定する必要があります。 

[![電子メール パラメータ ページ上の SMTP 設定タブ](./media/smtp.png)](./media/smtp.png)

アクセス許可の SMTP ユーザー アカウントは `serviceacct@d365forops.onmicrosoft.com1` です。 

> [!IMPORTANT]
> すべてのユーザーは、SMTP アカウントに Office 365 の電子メール設定での送信者アクセス許可を与える必要があります。 この構成は、Microsoft Exchange または Office 365 Admin ポータルのメールボックスのアクセス許可で行われます。 次の図は、STMP サービスアカウントが、**Send As** セクションに追加されているテスト ユーザー アカウントの設定を示しています。 

[![Office 365 で送信者アクセス許可を付与されている SMTP アカウント](./media/o365.png)](./media/o365.png)

### <a name="fixed-issue-the-office-add-ins-dont-yet-support-ad-fs"></a>\[固定\] 問題: Office アドインでは、まだ AD FS をサポートしていない

**影響を受けるバージョン:** CTP8 と 2016 年 2 月のリリース 

**問題:** Active Directory フェデレーションサービス (AD FS) を使用する Azure AD テナントのユーザーが Office アドインにサインインしようとすると (つまり、ユーザーがアカウントを入力して Tab キーを押すか、フィールド内をクリックしてパスワードを入力すると)、別のブラウザウィンドウが開きます。 このブラウザ ウィンドウには通常、`https://az689774.vo.msecnd.net/dynamicsofficeapp/v1.2.1.0/App/DynamicsApp.html\#id\_token=` で始まる URL があります。 ユーザーがログインできません。 

**説明:** Office アドイン (Excel アドインと Word アドインの両方) へのサインイン中、テナントの AD FS サイトへのリダイレクトが発生します。 ただし、そのサイトは不明なため、許可されていないアプリケーション ドメイン (AppDomain) です。 

**長期的な修正プログラム:** 2016 年 5 月 10 日にこの問題の長期的な修正プログラムが適切に配置されました。 Office アドインは、Office チームが追加した新しいダイアログ API を使用するようになりました。 

**AD FS をサポートするアドイン アップデートを利用:** すべての Office のインストールは、**ファイル** > **アカウント** > **更新** (Click-to-Run インストールの場合) または Windows Update(MSI インストールの場合) を経由して更新する必要があります。 AD FS ダイアログ API は、5 月の更新プログラムに含められました ([16.0.6868.2060](http://answers.microsoft.com/en-us/office/forum/office_2016-office_install/may-update-16068682060-for-office-2016-on-windows/ea082237-7ec3-4b06-895b-83490980e6d2?auth=1))。 更新プログラムの詳細については、[Office 365 クライアント更新チャンネルのリリース](https://technet.microsoft.com/en-us/office/mt465751?f=255&MSPPError=-2147217396) ページを参照してください。 

Office ビルドが更新されない場合、遅延したトラックにある場合があります ([Microsoft Office 365 ProPlus 更新チャネル オプション](https://technet.microsoft.com/en-us/library/mt455210.aspx))。 この場合、[Office 配置ツールを使用して現在のチャネルに移動する](https://technet.microsoft.com/en-us/library/jj219422.aspx?f=255&MSPPError=-2147217396) を使用するか、最新の更新プログラムがあることを保証するために [Office Insider プログラム](https://products.office.com/en-us/office-insider) にサインアップできます。 また、[Office 2016 の最新バージョンをインストール](https://dev.office.com/docs/add-ins/develop/install-latest-office-version) および [管理者の Office 2016 配置ガイド](https://technet.microsoft.com/en-us/library/cc303401(v=office.16).aspx) を参照してください。 

Office の更新プログラムをインストールできない場合、次の回避策を実行するとユーザーのブロックを解除できます。

#### <a name="workaround-use-internet-explorer-to-sign-in-to-the-client-before-you-use-the-office-add-ins"></a>回避策: Office アドインを使用する前に Internet Explorer を使用してクライアントにサインイン

この回避策には、ユーザーの知識と追加の手順が必要です。 この解決策についてユーザーが教育を受けた後は、解決が容易になります。 

**ユーザー ステップ:** Excel (または Word) を開く前に、Internet Explorer を使用してクライアントにサインインする必要があります。 

**説明:** Excel または Word のアドインではサインイン コンテキストが使用され、リダイレクトは必要ありません。 Office アドインが Excel および Word の Internet Explorer ウィンドウ内で実行されるため、以前のサインインは Internet Explorer で実行する必要があります。 サインインのコンテキストは、ポリシーに応じて 6〜24 時間続きます。 したがって、Internet Explorer を介した新しいサインインが必要な場合があります。

1.  Internet Explorer および Excelを終了します。
2.  Internet Explorer を起動し、クライアントにログインします。
3.  [Excel で開く] エクスペリエンスを使用して Excel アドインをテストします。 (たとえば、**フリート管理**&gt;**顧客**&gt;**顧客**&gt; **Microsoft Office で開く** &gt;**Excel で開く**&gt;**フリート管理の顧客**をクリックします。)

### <a name="fixed-issue-the-excel-add-in-doesnt-correctly-run-or-enable-sign-in"></a>\[固定\] 問題: Excel アドインが正しく実行されず、サインインが有効にならない

**問題:** ユーザーが Excel アドインにサインインしようとすると、認証ページの代わりに空白の認証ダイアログボックスが表示されるか、エラー メッセージが表示されます。 ユーザーがログインできません。 

**説明:** Excel アドインは、Office Web JS アドイン プラットフォームを依存し、認証に Azure AD を使用します。 プロキシを使用する場合、ユーザーが Excel アドインを実行してサインインするには、いくつかの URL にアクセスできる必要があります。 また、AD FS が使用される場合は、AD FS URL が HTTPS を使用する必要があります。 

**ソリューション:** この問題は顧客固有のネットワーク問題であるため、顧客固有の解決策が必要です。 AD FS が使用される場合は、AD FS URL が HTTPS を使用していることを確認します。 また、次のすべての URL がユーザーのコンピューターからアクセスできることを確認してください。

読み込みのために次の URL にアクセスします。

- `http://az689774.vo.msecnd.net:443`
- `https://az689774.vo.msecnd.net`
- `http://appsforoffice.microsoft.com:443`
- `https://appsforoffice.microsoft.com`
- `http://secure.aadcdn.microsoftonline-p.com:443`
- `https://secure.aadcdn.microsoftonline-p.com`
- `http://az416426.vo.msecnd.net:443`
- `https://az416426.vo.msecnd.net`
- `http://telemetryservice.firstpartyapps.oaspapps.com:443`
- `https://telemetryservice.firstpartyapps.oaspapps.com`
- `http://nexus.officeapps.live.com:443`
- `https://nexus.officeapps.live.com`
- `http://browser.pipe.aria.microsoft.com:443`
- `https://browser.pipe.aria.microsoft.com`
- `http://schemas.microsoft.com`

認証のために次の URL にアクセスします。

- `http://login.windows.net:443`
- `https://login.windows.net`
- `http://login.microsoftonline.com:443`
- `https://login.microsoftonline.com`

## <a name="additional-resources"></a>その他のリソース

[Office 統合](office-integration.md)

[Office 統合のチュートリアル](office-integration-tutorial.md)

[Power BI 統合の構成](../analytics/configure-power-bi-integration.md)

