---
title: "申請"
description: "アプリケーションの実行時のインスタンスを表します。"
author: shadykdc
manager: AnnBe
ms.date: 08/01/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 
audience: Developer
ms.reviewer: robinr
ms.search.scope: 
ms.search.region: Global
ms.author: kashea
ms.search.validFrom: 
ms.dyn365.ops.version: 
ms.translationtype: HT
ms.sourcegitcommit: 879eb9f2a63a8514791f74965005ed3e22bc0de7
ms.openlocfilehash: d0d2d60c033ff5cdd0a17b6b2aa476c170e388c3
ms.contentlocale: ja-jp
ms.lasthandoff: 04/20/2018

---

# <a name="application-type"></a>Application タイプ

[!include [banner](../../../../includes/banner.md)]

アプリケーションの実行時のインスタンスを表します。

### <a name="hierarchy"></a>階層

申請 <br>

## <a name="index"></a>指数

### <a name="properties"></a>プロパティ

* [minVersion](services-application-iapplication.md#minversion)

### <a name="methods"></a>メソッド

* [appInit](services-application-iapplication.md#appinit)

## <a name="properties"></a>プロパティ

### <a name="minversion"></a>minVersion

minVersion: string (省略可) 

このコンポーネントで必要な最小プラットフォーム バージョンを示すオプション マーカーです。 これが指定され、プラットフォームの以前のバージョンへのコンポーネントの読み込みが試行されるとき、対応するワークスペースは読み込まれず、ユーザーはプラットフォームの新しいバージョンのインストールを指示されます。


## <a name="methods"></a>メソッド

### <a name="appinit"></a>appInit


appInit(metadata: [ApplicationMetadata](services-application-iapplicationmetadata.md)): any

このメソッドは、アプリケーションが実行される時点で呼び出され、アプリケーション メタデータのインスタンスが読み込まれます。
渡されたメタデータは、このメソッドが戻る前に動作を変更するために変更できます。


#### <a name="parameters"></a>パラメーター

| 氏名 | 種類 | 説明 |
| ---- | ---- | ----------- |
| metadata|[ApplicationMetadata](services-application-iapplicationmetadata.md)||

#### <a name="returns-any"></a>any を返します


