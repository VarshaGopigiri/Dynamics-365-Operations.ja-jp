---
title: "製品のコンフィギュレーションの再利用"
description: "製品の既存のコンフィギュレーションを自動的に再利用することを指定できます。 次にユーザーがコンフィギュレーション セッションを完了すると、ユーザーの選択と一致するコンフィギュレーションが既に存在するかどうかが確認されます。 一致するコンフィギュレーションが見つかった場合は、コンフィギュレーション ID、対応する部品表 (BOM)、および工順が再利用されます。"
author: cvocph
manager: AnnBe
ms.date: 06/20/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 
ms.search.form: PCProductConfigurationModelDetails
audience: Application User
ms.reviewer: yuyus
ms.search.scope: Core, Operations
ms.custom: 201813
ms.assetid: 4985e308-7824-41fc-83fd-fd0bdae888e3
ms.search.region: Global
ms.search.industry: Manufacturing
ms.author: conradv
ms.search.validFrom: 2016-02-28
ms.dyn365.ops.version: AX 7.0.0
ms.translationtype: HT
ms.sourcegitcommit: ea07d8e91c94d9fdad4c2d05533981e254420188
ms.openlocfilehash: c447440c33c1f80c6056974086b90d3b43e8499e
ms.contentlocale: ja-jp
ms.lasthandoff: 02/07/2018

---

# <a name="reuse-product-configurations"></a>製品のコンフィギュレーションの再利用

[!include [banner](../includes/banner.md)]

製品の既存のコンフィギュレーションを自動的に再利用することを指定できます。 次にユーザーがコンフィギュレーション セッションを完了すると、ユーザーの選択と一致するコンフィギュレーションが既に存在するかどうかが確認されます。 一致するコンフィギュレーションが見つかった場合は、コンフィギュレーション ID、対応する部品表 (BOM)、および工順が再利用されます。

<a name="requirements-for-reusing-configurations"></a>コンフィギュレーションを再利用するための条件
---------------------------------------

コンフィギュレーションの再利用を有効にするには、[**製品コンフィギュレーション モデルの詳細**] ページで、コンポーネントと属性の次の情報を指定する必要があります:

-   [**コンポーネントおよびサブコンポーネント**] – [**一般**] クイック タブ、[**コンフィギュレーションの再利用**] フィールドで [**有**] を選択します。
-   [**属性**] – [**属性**] クイック タブで、[**再利用に含める**] オプションを選択します。 このオプションは、関連するコンポーネントの再利用が有効になっている場合にのみ表示されます。 再利用の属性を選択しない場合、コンフィギュレーション セッション中のユーザーの選択に関係なく、コンフィギュレーションは常に再利用されます。 既存のコンフィギュレーションの属性値はユーザーの選択と一致している必要があります。 たとえば、ユーザーがコンフィギュレーション セッション中、色に [**青**] を選択すると、システムはコンポーネントの既存のコンフィギュレーションに青い色があるかどうか確認します。

## <a name="resetting-configuration-reuse"></a>コンフィギュレーション再利用をリセットします
コンフィギュレーションの再利用をリセットする場合、以前に作成したコンフィギュレーションは考慮されません。 BOM または工順が変更され、コンフィギュレーションの再利用をリセットしたい場合でも、関連する属性は変更されません。 コンポーネントの [**一般**] クイック タブで、コンフィギュレーションの再利用をリセットします。




