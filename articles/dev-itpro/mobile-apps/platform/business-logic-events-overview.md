---
title: "ビジネス ロジック イベントの概要"
description: "ビジネス ロジックで実行されるコードは、ページ、アクション、コントロールのメタデータにランタイム変更を加えることができます。"
author: makhabaz
manager: AnnBe
ms.date: 08/14/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-platform
ms.technology: 
audience: Developer, IT Pro
ms.reviewer: robinr
ms.search.scope: Operations
ms.custom: 255544
ms.assetid: 
ms.search.region: Global
ms.author: makhabaz
ms.search.validFrom: 2016-11-30
ms.dyn365.ops.version: Platform update 3
ms.translationtype: HT
ms.sourcegitcommit: 879eb9f2a63a8514791f74965005ed3e22bc0de7
ms.openlocfilehash: 9167b539f2d48dbbdeb3f53901255ba20f8418ef
ms.contentlocale: ja-jp
ms.lasthandoff: 04/20/2018

---

# <a name="business-logic-events-overview"></a>ビジネス ロジック イベントの概要

[!include [banner](../../includes/banner.md)]

モバイル ワークスペースのビジネス ロジック イベントは、開発者が能力を高めるためにワークスペースの構成を指定する場所を提供し、業務シナリオ固有の動作を実装します。 モバイル アプリのプロセスで、すべてのモバイル ビジネス ロジックを実行した場合、ビジネス ロジック実行フローは Operations モバイル アプリ フレームワークによって制御されます。 

ビジネス ロジックで実行されるコードは、ページ、アクション、コントロールのメタデータにランタイム変更を加えることができます。 これらの実行時の変更は、アプリにキャッシュされている静的メタデータをオーバーレイしますが、変更はキャッシュされた静的メタデータを直接変更するものではなく、サーバーに格納されている静的メタデータにも影響しません。 これらのランタイム変更は、アプリケーションが終了するまで続きます。 

アプリケーションのビジネス ロジックで実行されるコードは、アプリケーションに格納されているビジネス データにランタイム変更を加えることができます。 これらの変更 (正しいプラクティスに従って実行される場合) は、アプリ内の他のビジネス データとして通常のデータ処理フレームワークに参加します。 これは、オフライン優先機能とフレームワークによって提供される非同期保存動作に従うことを意味します。


