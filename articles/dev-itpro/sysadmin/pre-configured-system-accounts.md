---
title: "コンフィギュレーション済みのシステム アカウント"
description: "このトピックでは、Microsoft Dynamics 365 for Finance and Operations 環境で事前設定されているシステム アカウントについて説明します。"
author: manalidongre
manager: AnnBe
ms.date: 11/07/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-platform
ms.technology: 
ms.search.form: 
audience: IT Pro
ms.reviewer: kfend
ms.search.scope: Operations
ms.custom: 
ms.assetid: 
ms.search.region: Global
ms.author: manado
ms.search.validFrom: 2017-11-01
ms.dyn365.ops.version: Platform update 13
ms.translationtype: HT
ms.sourcegitcommit: 879eb9f2a63a8514791f74965005ed3e22bc0de7
ms.openlocfilehash: be9b719a158bf613d6680b9758a8d06e33ae2f82
ms.contentlocale: ja-jp
ms.lasthandoff: 04/20/2018

---

# <a name="pre-configured-system-accounts"></a>コンフィギュレーション済みのシステム アカウント

[!include [banner](../includes/banner.md)]

構成済みのシステム アカウントは、Microsoft が Dynamics 365 for Finance and Operations サービスを管理および運用し、特定の機能をユーザーに提供できるように、配置された環境に含まれます。 次のテーブルは、アカウントの目的とユース ケースを含む、各アカウントに関する情報を示しています。  

> [!IMPORTANT] 
> システム アカウントを削除しないでください。 これらの勘定を削除すると、Microsoft が提供する主要な機能が中断されます。

|                               口座の詳細                               |                                                                    アカウントの目的/ユース ケース                                                                    |
|----------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                  Axrunner                                  |                                   このアカウントは、環境の稼働状態を監視し、必要に応じて警告を提供するために使用されます。                                    |
|                               FRServiceUser                                | これは、財務諸表サービスのユーザー アカウントで、Management Reporter アプリケーションが Dynamics 365 for Unified Operations に使用します。 |
|                            RetailServiceAccount                            |                              このアカウントは、Retail サービスで Dynamics 365 for Unified Operations 環境に接続するために使用されます。                              |
| SysHealthServiceUser または Axping (展開された製品バージョンによって異なる) |                           このアカウントは、環境の可用性と稼働状態を監視し、必要に応じて警告を提供するために使用されます。                           |


