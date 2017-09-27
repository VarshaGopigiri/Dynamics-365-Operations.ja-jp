--- 
title: "リソース能力の定義"
description: "リソースの能力は、リソースがどのような工程を行えるかを示します。"
author: sorenva
manager: AnnBe
ms.date: 10/27/2016
ms.topic: business-process
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 
audience: Application User
ms.reviewer: yuyus
ms.search.scope: Operations
ms.search.region: Global
ms.search.industry: Manufacturing
ms.author: sorenand
ms.search.validFrom: 2016-06-30
ms.dyn365.ops.version: AX 7.0.0
ms.translationtype: HT
ms.sourcegitcommit: 9b947a02be981155053e33a4ef20e19bf2a194a5
ms.openlocfilehash: 4a7d342eeb16fd76f2dde58151bfc7973de76e2d
ms.contentlocale: ja-jp
ms.lasthandoff: 07/27/2017

---
# <a name="define-resource-capabilities"></a>リソース能力の定義

[!include[task guide banner](../../includes/task-guide-banner.md)]

リソースの能力は、リソースがどのような工程を行えるかを示します。 スケジューリング中に、それぞれの職務や工程の要件と、利用可能なリソースの能力とを照合します。 このタスク ガイドでは、能力の作成、およびリソースへの割り当て方法を確認できます。 このタスクの作成に使用するデモ データの会社は USMF です。


## <a name="create-a-resource-capability"></a>リソース能力の作成
1. [リソース能力] に移動します。
2. [新規] をクリックします。
3. [能力] フィールドで、リソース能力の ID を入力します。
    * ある工程について、能力 ID を使用すると、工程の実行にその能力を持つリソースが必要であることを指定することができます。  
4. [説明] フィールドに、能力の説明を入力します。

## <a name="assign-capability-to-a-resource"></a>リソースへの能力の割り当て
1. [追加] をクリックします。
2. [リソース] フィールドで、リソースの ID を入力します。
    * リソースの能力は、1 つ以上のリソースに割り当てることができます。  
3. [有効期限] フィールドで、日付を入力します。
    * 限られた期間だけリソースに能力があることを指定する場合にも、このフィールドを使用できます。  
4. [優先順位] フィールドに数値を入力します。
    * 職務および工程をスケジュールするとき、優先順位によってリソースを選択するかどうかを指定できます。 これを選択し、かつ 2 つ以上のリソースが期日までに職務や工程を行うことができる場合、要求能力に応じて優先順位の最も低いリソースが選択されます。  
5. [レベル] フィールドに数値を入力します。
    * ジョブや工程が特定の機能を要求することを指定する場合は、必要な最低レベルを指定することができます。 能力レベルを使用すると、同じ職務を遂行することができるリソースについて、速度、強み、サイズなどの違いによる区別を行うことができます。  

