---
title: "アクセス インスタンス"
description: "このトピックでは、開発インスタンスへのアクセス、オンプレミス開発 VM の構成、および開発者と管理者にとって重要な構成設定を見つける方法について説明します。"
author: robadawy
manager: AnnBe
ms.date: 12/01/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-platform
ms.technology: 
audience: Developer
ms.reviewer: robinr
ms.search.scope: Operations
ms.custom: 10031
ms.assetid: 4be8b7a1-9632-4368-af41-6811cd100a37
ms.search.region: Global
ms.author: robadawy
ms.search.validFrom: 2016-02-28
ms.dyn365.ops.version: AX 7.0.0
ms.translationtype: HT
ms.sourcegitcommit: 879eb9f2a63a8514791f74965005ed3e22bc0de7
ms.openlocfilehash: 57c334fdb7d16c53d521e3c0671d7bec6f99ea58
ms.contentlocale: ja-jp
ms.lasthandoff: 04/20/2018

---

# <a name="deploy-and-access-development-environments"></a>開発環境の配置とアクセス 

[!INCLUDE [banner](../includes/banner.md)]

このトピックでは、開発インスタンスへのアクセス、オンプレミス開発 VM の構成、および開発者と管理者にとって重要な構成設定を見つける方法について説明します。

<a name="definitions"></a>定義
-----------

| 期間      | 定義                                                                                                                                                                                                                                       |
|-----------|------------------------------------------|
| エンド ユーザー  | Web クライアントを使用してインスタンスにアクセスするユーザー。 エンド ユーザーは、インスタンスにアクセスするには Microsoft Azure Active Directory (Azure AD) の資格情報が必要で、そのインスタンスのユーザーとしてプロビジョニングまたは追加する必要があります。 |
| 開発者 | Microsoft Visual Studio 環境でコードを開発するユーザー。 開発者は、開発環境 (VM) へのリモート デスクトップ アクセスが必要です。 開発者アカウントは、VM の管理者である必要があります。      |


## <a name="deploying-cloud-development-environments"></a>クラウド開発環境の配置

クラウドホスト環境を展開するプロセスは、LCS トライアルまたはパートナー プロジェクトと、LCS 顧客実装プロジェクトで異なります。

**試用版**または**パートナー**プロジェクト用:

1. LCS プロジェクトと Azure サブスクリプションの間に接続を作成します。 Azure サブスクリプション ID が必要であり、サブスクリプションの使用を承認します。

2. 配置する **環境** の下で **+** を選択します。

    ![LCS Onboard の方法](media/access-instances-5.jpeg)

3. アプリケーションとプラットフォーム バージョンを選択します。

4. 環境のトポロジを選択します。 クラウドにホストされている環境の使用、または VHD のダウンロードのいずれかを選択することができます。 詳細については、[プレビュー サブスクリプションのサインアップ](sign-up-preview-subscription.md) を参照してください。

    ![環境のトポロジの選択](media/access-instances-2.jpeg)

5. クラウドでホストされている環境を選択した場合は、使用する Azure コネクタを選択します。 **配置** を選択します。

    ![環境の配置](media/access-instances-3.jpeg)

6. クラウド ホスト環境を選択しなかった場合は、ダウンロードする VHD を選択します。

**顧客実装**プロジェクト用:

1. LCS 実装プロジェクトにログオンします。

2. **構成** を選択して配置します。

    ![開発、テスト、およびコンフィギュレーション](media/access-instances-6.jpeg)

3. アプリケーションとプラットフォーム バージョンを選択します。

4. 設定を指定し、**保存** を選択します。

    ![配置設定](media/access-instances-7.jpeg)

顧客には、Microsoft の Azure サブスクリプションでホストされている無料の「開発とテスト」環境が 1 つ提供されます。 「開発およびテスト」には、**開発**と**ビルドおよびテスト**の 2 種類の環境があります。 開発およびカスタマイズ活動については、**開発**環境をコンフィギュレーションします。 **ビルドおよびテスト**標準的な開発活動では環境はサポートされていません。 代わりに、日単位ビルドおよびテストの自動化に使用されます。 詳細については、[ビルドとテストの自動化](../perf-test/continuous-build-test-automation.md) を参照してください。  

追加の開発とビルド環境は、ユーザー自身の Azure サブスクリプションで購入またはホストすることができます。 独自のサブスクリプションに環境を展開するには、**クラウド ホスト環境** ページに移動します。

![クラウド ホスト インスタンス](media/CloudHostedPicture.JPG)

## <a name="cloud-environment-that-is-provisioned-through-lcs"></a>LCS を通じてプロビジョニングされるクラウド環境
クラウド環境が LCS を通じてプロビジョニングされると、次の操作が行われます。

-   クラウド環境を要求するユーザーは、その環境内の管理者としてプロビジョニングされます。
-   ユーザー アカウントは開発用 VM にプロビジョニングされ、リモート デスクトップ経由での環境へのアクセスを許可します。これらの資格情報は LCS の環境ページからアクセスできます。

### <a name="accessing-an-instance-through-a-url"></a>URL を試用したインスタンスへのアクセス

エンド ユーザーはシステムにアクセスできます。 管理者は、インスタンスの **ユーザー** ページを使用して、このシステムにユーザーを追加することができます。 これらの追加のユーザーは LCS 内のユーザーである必要はないことに注意してください。 LCS プロジェクト サイトからは、クラウド環境のベース URL を取得します。

1.  LCS プロジェクト ページに移動します。
2.  **環境**セクションで、配置された環境をクリックします。
3.  環境ページが開くと、右上隅で、**ログイン** &gt; **Finance and Operations にログオン** をクリックして、アプリケーションにアクセスできます。
4.  有効なエンド ユーザー資格情報を使用して、アプリケーションにサインインします。 現在の LCS ユーザーが最初に環境を展開したユーザーである場合は、そのユーザーは有効な終了ユーザーおよびアプリケーションの管理者である可能性があります。
5.  ブラウザーで、サインインした後にベース URL を記録します。 たとえば、ベース URL は、**https://dynamicsAx7aosContoso.cloud.dynamics.com** である可能性があります。

### <a name="accessing-the-cloud-instance-through-remote-desktop"></a>リモート デスクトップを使用したクラウド インスタンスへのアクセス

クラウド環境は、エンド ユーザーおよび開発者の両方としてアクセスできます。 開発者は、リモート デスクトップの資格情報を使用してシステムにアクセスできます。 リモート デスクトップの資格情報は、LCS プロジェクト サイトの環境ページから取得されます (このトピックの前の図を参照してください)。

![制限された管理者アクセス](media/restricted-admin.png)

配置された**プラットフォーム更新プログラム 12 以前**の環境の対象:
1.  VM 名をクリックします。
2.  表示されているローカル管理者のユーザー名とパスワードを使用して、リモート デスクトップ経由でクラウド VM に接続します。 目のアイコンをクリックしてパスワードを表示することができます。

配置された**プラットフォーム更新プログラム 12 以降**の任意の環境については、特徴的アカウント、開発者アカウントおよび管理者アカウントがあります。 顧客が、Microsoft サブスクリプションで実行されている開発環境またはビルド環境の仮想マシン (VM) 管理者アカウントにアクセスすることはできません。 したがって、環境が Azure サブスクリプションで実行されていない限り、管理者アカウントは非表示になります。 

リモート デスクトップを通じて環境にサインインした後、ブラウザーからローカル アプリケーションにアクセスできるようにする場合、リモート コンピューターからアプリケーションにアクセスするために使用するのと同じベース URL を使用します。 上記のセクションは、このベース URL を LCS から取得する方法について説明します。


## <a name="vm-that-is-running-on-premises"></a>オンプレミスで実行されている VM
環境仮想ハード ディスク (VHD) は LCS からダウンロードができるようになり、ローカル コンピューター上に設定可能です。 このシステムは、開発者が使用することをその目的としています。

1.  LCS プロジェクトのメイン ページの、**環境**セクションで、プラス記号 (**+**) をクリックし、**ローカル**をクリックします。 接続サイトに運ばれます。
2.  **ダウンロード**ページに移動して、最新の VHD をダウンロードします。
3.  Microsoft Hyper-V マネージャーで、ダウンロードした VHD からローカル VM を作成します。 VM に推奨されている 16 ギガバイト (GB) のメモリと 2 つの仮想プロセッサを付与することをお勧めします。 動的なメモリ割り当てを使用しないでください。

### <a name="retail-configuration"></a>Retail コンフィギュレーション

Retail もコンフィギュレーションしている場合は、このセクションの手順に従います。

ダウンロード可能な VHD を POS のカスタマイズに使用するには、次の手順も実行する必要があります。

-   ホスト コンピューターで、入れ子になった VM サポートを有効にします。 詳細については、[入れ子仮想化の仮想マシンで Hyper-v を実行](https://msdn.microsoft.com/en-us/virtualization/hyperv_on_windows/user_guide/nesting) を参照してください。

### <a name="running-the-virtual-machine-vm-locally"></a>仮想マシン (VM) をローカルで実行

Hyper-V マネージャーから VM を実行するには、これらの手順に従います。

1. VM を起動するには、**開始** をクリックします。
2. ウィンドウで VM を開くには、**接続** をクリックします。
3. ツール バーで **Ctrl + Alt + Delete** ボタンをクリックしてください。 VM は、ほとんどのキーボード コマンドを受け取りますが、その中に Ctrl + Alt + Del は含まれていません。 したがって、ボタンまたはメニュー コマンドを使用する必要があります。
4. 次の資格情報を使用して VM にログインします。
   - ユーザー名: **管理者**
   - パスワード: <strong>pass@word1</strong>

   **ヒント:** 画面解像度を変更することにより、VM ウィンドウのサイズを変更することができます。 VM でデスクトップを右クリックし、**画面の解像度** をクリックします。 ディスプレイに適した解像度を選択します。
5. 管理者ユーザーを準備します。 詳細については、次のセクションを参照してください。
6. バッチ マネージャー サービスを起動します。 このステップは、バッチ ジョブまたはワークフローを実行している場合に必要です。
   1.  管理者として**コマンド プロンプト** ウィンドウを開きます。
   2.  **net start DynamicsAxBatch** と入力し、Enter キーを押します。

   また、サービスを **サービス** ウィンドウから開始することができます。

#### <a name="retail-configuration"></a>Retail コンフィギュレーション

POS カスタマイズで、ゲスト VM でもこれらの手順に従う必要があります。

1.  [Microsoft Emulator for Windows 10 Mobile Anniversary Update](https://www.microsoft.com/en-us/download/details.aspx?id=53424) をダウンロードしてインストールします。
2.  Hyper-V ホスト サービスを起動します。 詳細については、[Hyper-V: Hyper-V 仮想マシン管理サービスを実行している必要があります](https://technet.microsoft.com/en-us/library/ee956894(v=ws.10).aspx) を参照してください。 起動中にエラーが発生した場合は、ゲスト VM で Hyper-V ロールをアンインストールし、再インストールすることもできます。

### <a name="provisioning-the-administrator-user"></a>管理者ユーザーを準備

開発者がアクセスするには、インスタンスで管理者である必要があります。 管理者としての資格情報をプロビジョニングするには、デスクトップにある管理者プロビジョニング ツールを実行し、ツールにメール アドレス (Azure AD 資格情報) を入力します。

1.  デスクトップから、管理者として管理者ユーザーのプロビジョニング ツールを実行します (アイコンを右クリックし、**管理者として実行**をクリックします)。
2.  電子メール アドレスを入力し、**送信**をクリックします。

### <a name="retail-configuration"></a>Retail コンフィギュレーション

Retail もコンフィギュレーションしている場合は、このセクションの手順に従います。

#### <a name="for-dynamics-365-for-operations-version-1611"></a>Dynamics 365 for Operations バージョン 1611 用

1.  RetailTenantUpdateTool を実行します。
    -   このツールのアイコンは、デスクトップ上で使用できます。
    -   このツールは、次の場所から使用することもできます: C:\windowsSystem32WindowsPowerShellv1.0PowerShell.exe-ファイルC:\RetailSDKToolsRetailTenantUpdateTool.ps1

2.  このツールを開始するには、アイコンをダブルクリックします。 自身の Azure AD 資格情報を求められます。 管理者ユーザーのプロビジョニング ツールで以前使用したものと同じ資格情報を使用する必要があります。

#### <a name="for-dynamics-365-for-operations-70"></a>Dynamics 365 for Operations 7.0 用

1.  [IT プロフェッショナル用 Microsoft Online Services サインイン アシスタント RTW](http://go.microsoft.com/fwlink/?LinkID=286152) をインストールします。
2.  [Windows PowerShell 用 Azure Active Directory モジュール (64 ビット バージョン)](http://go.microsoft.com/fwlink/p/?linkid=236297) をインストールします。
3.  テナントとユーザー ID の Azure AD を照会します。 Windows PowerShell 統合スクリプト環境 (ISE) ウィンドウを管理者権限で開き、次のコマンドを実行します。 Azure AD 資格情報を求められます。 以前に管理者プロビジョニング ツールで使用したのと同じユーザー アカウントを使用します。

        $msocred = Get-Credential 
        Connect-MsolService -Credential $msocred 
        $company = Get-MsolCompanyInformation 
        Write-Host "TenantID: $($company.ObjectId)" 
        $msocred.UserName 
        $users = Get-MsolUser -SearchString "$($msocred.username)" 
        foreach($u in $users) 
        { 
            if($u.SignInName -eq $msocred.UserName) 
            { 
               Write-Host "SignInName:$($u.SignInName) UserId: $($u.ObjectId)" 
            } 
        }
    [![Windows PowerShell ISE ウィンドウのコマンド](./media/retailconfig02-1024x529.png)](./media/retailconfig02.png)

4.  次の SQL スクリプトを更新し、その環境の AXDB で実行します。 上記の Windows PowerShell スクリプト出力から次のパラメーターの値を指定します。

    -   **TenantID** – c83429a6-782b-4275-85cf-60ebe81250ee を例に取ります。
    -   **UserId** – 例えば、a036b5d8-bc8c-4abe-8eec-17516ea913ec

    <!-- -->

        DECLARE @TenantId NVARCHAR(1024)         DECLARE @UserId NVARCHAR(1024) 
        SET @TenantId = ‘‘ 
        SET @UserId = ‘‘ 
        IF(LEN(@TenantId) > 0 AND LEN(@UserId) > 0) 
            BEGIN 
            UPDATE AxDBRAIN.dbo.SYSSERVICECONFIGURATIONSETTING SET [VALUE] = @TenantId WHERE [NAME] = ‘TENANTID’ 
            UPDATE RetailHoustonStore.ax.SYSSERVICECONFIGURATIONSETTING SET [VALUE] = @TenantId WHERE [NAME] = ‘TENANTID’ 
            UPDATE AxDBRAIN.dbo.RETAILSTAFFTABLE SET EXTERNALIDENTITYID = @TenantId, EXTERNALIDENTITYSUBID = @UserId WHERE STAFFID = ‘000160’
            END 
        ELSE 
            BEGIN 
            RAISERROR (15600, -1, -1, ‘TenantId and UserId must be set before running this script’) 
            END

5.  管理者特権の**コマンド プロンプト** ウィンドウで **IISRESET** を実行することにより、インターネット インフォメーション サービス (IIS) をリセットします。
6.  新しい管理者ユーザーを使用するようにリアルタイム サービス プロファイルを更新します。
    1.  **小売** &gt; **本社の設定** &gt; **小売用スケジューラ** &gt; **Real-time Service プロファイル**の順にクリックします。
    2.  **小売** &gt; **本社の設定** &gt; **小売用スケジューラ** &gt; **Real-time Service プロファイル**の順にクリックします。
    3.  以前に使用したユーザーを使用するように JBB レコードを編集します (たとえば、**administrator@contosoax7.onmicrosoft.com**)。
    4.  既定のチャネル データベースの CDX ジョブ 1070 (スタッフ) を実行します。
    5.  クライアント上の **ダウンロード セッション** ページを表示して、ジョブが成功したことを確認します。

### <a name="base-url-of-the-local-application"></a>ローカル アプリケーションの基本 URL

ユーザーが管理者としてプロビジョニングされると、そのユーザーは次のベース URL に移動してコンピュータ上のインスタンスにアクセスできます: https://usnconeboxax1aos.cloud.onebox.dynamics.com。もしバージョン コントロールを使用し、複数の開発VM を同じ Visual Studio Team Services (VSTS) プロジェクトに接続する計画がある場合は、ローカル VM の名前を変更してください。 手順については、[Visual Studio Team Services へのアクセスを有効化するには、ローカルの名前を変更してください](../migration-upgrade/vso-machine-renaming.md) を参照してください。

#### <a name="retail-configuration"></a>Retail コンフィギュレーション

Retail Cloud POS アプリの URL は <https://usnconeboxax1pos.cloud.onebox.dynamics.com/> です。構成手順を完了した後に、この VM が Azure AD テナントでプロビジョニングされます。 Azure AD 管理者アカウントは、デモ データ内のレジ担当者アカウントにマップされます。 この環境の Retail POS デバイスを簡単にアクティブにするには、このレジ担当者アカウントを使用できます。

-   出納係ユーザー ID: **000160**
-   出納係パスワード: **123**
-   出納係 LE: **USRT**
-   出納係ストア: **ヒューストン**

## <a name="location-of-packages-source-code-and-other-aos-configurations"></a>パッケージ、ソース コード、およびその他の AOS コンフィギュレーションの場所
VM で、AOSWebApplication の web.config file を開くことによって、ほとんどのアプリケーション コンフィギュレーションが表示されます。

1.  IIS を起動します。
2.  **サイト** &gt; **AOSWebApplication** に移動します。
3.  右クリックしてから、**エクスプローラー** をクリックしてエクスプローラーを開きます。
4.  メモ帳や他のテキスト エディターで web.config ファイルを開きます。 多くの開発者や管理者にとって、次のキーが重要です。
    -   **Aos.MetadataDirectory** - このキーは、プラットフォームとアプリケーションのバイナリを含むパッケージ フォルダの場所、およびソースコードをポイントします。 (ソース コードは、開発環境でのみ使用できます。) 一般的な値は、c:\packages、c:\AosServicePackagesLocalDirectory、および J:AosServicePackagesLocalDirectory です。
    -   **DataAccess.Database** - このキーは、データベースの名前を保持します。
    -   **Aos.AppRoot** - このキーは、Application Object Server (AOS) Web アプリケーションのルート フォルダーをポイントします。

### <a name="retail-configuration"></a>Retail コンフィギュレーション

Retail ソフトウェア開発キット (SDK) は、C:\RetailSDK にあります。 小売アプリケーションの使用およびカスタマイズ方法の詳細については、次のトピックを参照してください。
-   [Retail SDK の概要](../../retail/dev-itpro/retail-sdk/retail-sdk-overview.md)
-   [Retail POS デバイスのライセンス認証](../../retail/dev-itpro/retail-device-activation.md)

## <a name="redeploying-or-restarting-the-runtime-on-the-vm"></a>VM でのランタイムの再配置または再起動
ローカルのランタイムを再起動して、すべてのパッケージを再配置するには、次の手順を実行します。

1.  ファイル エクスプローラーを開き、C:\CustomerServiceUnit に移動します。
2.  **AOSDeploy.cmd** を右クリックして**管理者として実行** をクリックします。

このプロセス時間がかかる場合があります。 cmd.exe ウィンドウが終了すると、プロセスが完了します。 ランタイムを再配置せずに AOS を再起動するのみの場合は、管理者の **Command Prompt** ウィンドウから **iisreset** を実行するか、IIS から AOSWebApplication を再起動します。




