---
title: "Visual Studio Team Services へのアクセスを有効化するには、ローカル環境の名前を変更してください"
description: "複数のコンピューターにまたがる VSTS プロジェクトにアクセスするには、ローカル開発 VM の名前変更が必要です。"
author: MargoC
manager: AnnBe
ms.date: 06/20/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-platform
ms.technology: 
audience: Developer
ms.reviewer: robinr
ms.search.scope: Operations
ms.custom: 25911
ms.assetid: 4f5ff29b-9ae5-4ba2-8b6e-1e5d94e004b3
ms.search.region: Global
ms.author: tabell
ms.search.validFrom: 2016-02-28
ms.dyn365.ops.version: AX 7.0.0
ms.translationtype: HT
ms.sourcegitcommit: 879eb9f2a63a8514791f74965005ed3e22bc0de7
ms.openlocfilehash: 8e7dc968334c4e1b3f7baf865571ebe6aebfc8a0
ms.contentlocale: ja-jp
ms.lasthandoff: 04/20/2018

---

# <a name="rename-a-local-environment-to-enable-access-to-visual-studio-team-services"></a>Visual Studio Team Services へのアクセスを有効化するには、ローカル環境の名前を変更してください

[!include [banner](../includes/banner.md)]

複数のコンピューターにまたがる VSTS プロジェクトにアクセスするには、ローカル開発 VM の名前変更が必要です。

Visual Studio Team Services (VSTS) (旧名称は Visual Studio Online または VSO) はバージョン コントロールのために必要です。 開発トポロジでは、複数の VM が同じコンピューター名である場合、同じ VSTS プロジェクトにアクセスできません。 VSTS はマシン名を ID として使用します。 Microsoft Lifecycle Services (LCS) からローカル VM で開発する場合は、問題が発生する可能性があります。

- この問題を回避するには、開発を開始する前にマシンの名前を変更してリブートし、VSTS に接続します。
- これらを実行した後、SQL Server レポート サーバーもコンフィギュレーションする必要があります。 これを行うには、SQL Server レポート サーバーのデータベース接続文字列で SQL Server 名を (localhost) に変更します。

  [![4](./media/4.png)](./media/4.png)




