---
title: "Dynamics 365 for Finance and Operations の B2B機能"
description: "このトピックでは、Microsoft Dynamics 365 for Finance and Operations で企業間のトランザクション機能を実装する方法について説明します。"
author: sarvanisathish
manager: AnnBe
ms.date: 10/11/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-platform
ms.technology: 
ms.search.form: B2BInvitationConfiguration
audience: developer, IT Pro
ms.reviewer: sericks
ms.search.scope: Core, Operations
ms.custom: 
ms.assetid: 
ms.search.region: Global
ms.author: sarvanis
ms.search.validFrom: 2017-10-31
ms.dyn365.ops.version: Platform update 12
ms.translationtype: HT
ms.sourcegitcommit: 879eb9f2a63a8514791f74965005ed3e22bc0de7
ms.openlocfilehash: 86e99aa178c1adf68c8f93ccdbdc176de108078d
ms.contentlocale: ja-jp
ms.lasthandoff: 04/20/2018

---

# <a name="export-b2b-users-to-azure-ad"></a>B2B ユーザーの Azure AD へのエクスポート

[!include [banner](../includes/banner.md)]

企業間 (B2B) ユーザーを Azure Active Directory (Azure AD) に自動的にエクスポートすることができます。 

過去には、B2B ユーザーは .csv ファイルに手動でエクスポートされていました。 その後、Azure AD テナントの管理者は、このファイルを使用して Azure ポータルを使用してユーザーを Azure AD に手動で追加する必要があります。 

自動エクスポート機能を有効にするには、ワンタイム設定と構成プロセスを完了する必要があります。 このプロセスが完了したら、**新しいユーザーのプロビジョニング** ワークフロー タスクを使用して、Azure AD に B2B ユーザーを自動的にエクスポートできます。

1回限りの設定とコンフィギュレーションでは、次のことが必要になります。 
1. Azure AD で B2B 招待サービス アプリケーションを設定します。
2. Finance and Operations で B2B 招待サービスの設定のコンフィギュレーションをします。

### <a name="set-up-a-b2b-invitation-service-application-in-azure-ad"></a>Azure AD で B2B 招待サービス アプリケーションを設定
Azure AD テナントのテナント管理者は、以下の手順を完了する必要があります。

1. [Azure ポータル](https://portal.azure.com)にテナント管理者としてログオンします。 

2. **Azure Active Directory** > **プロパティ**をクリックします。

3. **ディレクトリ ID** (これはテナント ID) をコピーし、保存します。 これは後で必要になります。

4. **アプリの登録** > **新しいアプリケーションの登録**をクリックします。

5. 以下の情報を入力し、**作成**をクリックします。
    1. **名前**フィールドに、アプリケーションの名前を入力します。 例: **B2B 管理者アプリケーション**。
    2. **アプリケーション タイプ** フィールドで、**Web アプリ/API** を選択します。
    3. **サインオン URL** フィールドに、Finance and Operations の URL を入力します。
  
6. **アプリの登録**タブをクリックし、新しく作成したアプリケーションをクリックし、**アプリケーション ID** をコピーして保存します。 これは後で必要になります。

7. **すべての設定** > **必要なアクセス許可** > **追加**をクリックします。

8. **API アクセスの追加**ウィンドウで、次の操作を行います。
    1. **API を選択**タブをクリックします。**Microsoft Graph** をクリックし、**選択**をクリックします。
    
    2. **アクセス許可の選択**タブで、次のアプリケーションのアクセス許可を選択します。
         - **すべてのユーザーの完全なプロファイルの読み取りと書き込み**
         - **ディレクトリ データの読み取りと書き込み**
    
    3. 次の委任されたアクセス許可を選択します。
         - **サインインし、ユーザー プロファイルを読み取ります**
     
    4. **選択**および**完了**をクリックします。
    
9. **必要なアクセス許可**ブレードで、**アクセス許可の付与**をクリックしてから、**はい**をクリックしてアクセス許可を割り当てます。

10. **すべての設定** > **キー**をクリックし、次の操作を行います。 
    1. **説明**フィールドにキーの名前を入力します。
    2. **期限切れ日時** フィールドで有効期間を設定します。
  
11. **保存** をクリックします。 キーを保存すると、**値** が表示されます。 

    > [!WARNING]
    > キーを保存した後**値**キーを必ずコピーしてください。 この値はブレードを離れるときには使用できません。

### <a name="configure-the-b2b-invitation-service-settings-in-finance-and-operations"></a>Finance and Operations で B2B 招待サービスの設定のコンフィギュレーション

1. Dynamics 365 for Finance and Operations に管理者としてサインインします。

2. **B2B 招待状のコンフィギュレーション** ページに移動して、**編集**をクリックします。

3. **有効** を選択します。

4. **テナント ID** が**ディレクトリ ID** (前の手順の手順 3 でメモしたもの) と同じであることを確認します。

5. **クライアント ID** フィールドに、**アプリケーション ID** (前の手順の手順 6 でメモしたもの) を入力します。

6. 上記手順からコピーされたキー**値**を、**アプリケーション キー**フィールドに入力します。

7. 設定を**保存します**。

これで、ワークフローで**新しいユーザーのプロビジョニング** ワークフロー タスクの使用を開始して、Azure AD に B2B ユーザーを自動的にエクスポートできます。

