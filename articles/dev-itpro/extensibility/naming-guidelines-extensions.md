---
title: "モデルの拡張機能の名前付けガイドライン"
description: "このトピックでは、モデル拡張機能の名前付けガイドラインについて説明します。 モデル内の要素は、インストール時にすべてのモデルで一意の名前が必要です。"
author: LarsBlaaberg
manager: AnnBe
ms.date: 06/20/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-platform
ms.technology: 
audience: Developer
ms.reviewer: robinr
ms.search.scope: Operations
ms.custom: 89563
ms.assetid: 
ms.search.region: Global
ms.author: pvillads
ms.search.validFrom: 2017-07-01
ms.dyn365.ops.version: Platform update 9
ms.translationtype: HT
ms.sourcegitcommit: 879eb9f2a63a8514791f74965005ed3e22bc0de7
ms.openlocfilehash: 374a2b7f12b59806ee59abdadeec7c0a943e3cba
ms.contentlocale: ja-jp
ms.lasthandoff: 04/20/2018

---

# <a name="naming-guidelines-for-model-extensions"></a>モデルの拡張機能の名前付けガイドライン

[!include [banner](../includes/banner.md)]

## <a name="naming-model-elements"></a>モデル要素に名前を付ける
モデル内のすべての要素は、インストール時にすべてのモデルで一意の名前が必要です。 ただし、インストール時に、すべてのモデルの名前がわからず、モデルが一緒にインストールされる場合があります。 この状況に対応するには、すべての要素名に、ソリューション固有の接頭辞を含める必要があります。 モデルの要素に名前を付ける場合にこの接頭語を含めることで、名前の競合のリスクを大幅に軽減します。

+ モデルに複数のソリューションが含まれている場合は、さまざまな接頭語によって、モデルでは、各ソリューションを識別できます。 
+ 他の関係者からの他のモデルがそれらの要素に同じ接頭語を使用するリスクを最小限する接頭語を慎重に選択する必要があります。

他のモデル内の機能を拡張するとき、拡張される要素には接頭語がすでに含まれています。 ただし、拡張要素に接頭語を追加しません。名前には複数の連続した接頭語が含まれるようにします。 代わりに、拡張要素の名前を付けるときに、接頭語またはその他の語句、省略形をインフィックスとして含める必要があります。

## <a name="naming-extensions"></a>拡張機能に名前を付ける

拡張要素は、テーブル拡張子、ビュー拡張子、またはフォーム拡張子など、他のモデルの拡張子と競合のリスクを最小限にする一意の名前を付ける必要があります。 競合のリスクを最小限に抑えるために、名前には、拡張機能を他のモデル内の同じ要素の他の拡張機能と区別するための用語、省略形、または接中辞が含まれている必要があります。

+ 拡張子要素があるモデルの名前、または拡張子が関連付けられている接頭語のいずれかを含めます。 たとえば、ウェアハウジング モジュールは HCMWorker テーブルを拡張し、他のすべての要素の名前で **WHS** 接頭語を使用します。 この場合、拡張機能に **HCMWorker.WHSExtension** という名前が付けられます。 モジュール内の他の要素に名前を付けるために使用される接頭語が、接中辞として挿入されることを確認します。 別の例として、拡張子がアプリケーション スイート モデルからの ContactPerson テーブルへのすべての拡張機能を含むことを意図している場合、アプリケーション スイート モデルの ContactPerson テーブルの拡張子は、**ContactPerson.ApplicationSuiteExtension** という名前が付けられます。
+ 末尾に **Extension** という用語を付けます。 たとえば、InventLocation テーブルの拡張子は、**InventLocation.&lt;モデル&gt;拡張子**のパターンに従う必要があります。
+ 拡張子名を **&lt;Element that is being extended&gt;.Extension** としないでください。 たとえば、競合のリスクが大きすぎるため、InventLocation テーブルの拡張クラスには、**InventLocation.Extension** という名前を付ける必要はありません。

## <a name="naming-extension-classes"></a>拡張クラスの名前を付ける

テーブル、クラス、または他の要素のロジックを拡張するために使用される拡張子クラスは、すべてのモデルとタイプの間で一意の名前が必要です。 可能であれば、拡張クラスには、拡張されているタイプの名前を含める必要があります。 ただし、名前には、用語、省略形、またはクラスを他のタイプと区別する接頭語も含まれる必要があります。

+ 拡張クラスの名前を強化される型の名前で開始し、**\_Extension** という用語で名前を終了します。
したがって、ContactPerson テーブルを拡張する拡張クラスは、**ContactPerson** という名前で始まり、**\_Extension** で終わる必要があります。 たとえば、1 つの拡張クラスに **ContactPersonWHS\_拡張**という名前が付けられます。
+ 拡張子要素があるモデルの名前、または拡張子が関連付けられている接頭語のいずれかを含めます。 たとえば、ウェアハウジング モジュールは ContactPerson テーブルを拡張する拡張クラスを使用し、他のすべての要素の名前で **WHS** 接頭語を使用します。 この場合、拡張クラスに **ContactPersonWHS\_Extension** という名前が付けられます。 モジュール内の他の要素に名前を付けるために使用される接頭語が、接中辞として挿入されることを確認します。 別の例として、拡張クラスがアプリケーション スイート モデルの ContactPerson テーブルのすべての拡張機能を含むことを意図している場合、アプリケーション スイート モデルの ContactPerson テーブル を増補する拡張クラスは、**ContactPersonApplicationSuite\_拡張子**という名前が付けられます。
+ 拡張子名を **&lt;Element that is being extended&gt;\_Extension** としないでください。 たとえば、競合のリスクが大きすぎるため、InventLocation テーブルを補強する拡張クラスには、**InventLocation\_拡張子**という名前を付ける必要はありません。

## <a name="naming-fields-field-groups-indexes-relations-and-other-metadata-nodes-in-extension-elements"></a>拡張要素のフィールド、フィールド グループ、インデックス、関係およびその他のメタデータ ノードに名前を付ける

拡張要素のフィールド、インデックス、関係、およびその他のメタデータ要素は、拡張されておりその他の拡張要素両方の要素間で一意である名前を持っている必要があります。 したがって、これらのメタデータ ノードには、モデル間の競合のリスクを最小限にする用語、省略形、接頭辞のいずれかが含まれている必要があります。

+ メタデータ ノードの名前の先頭に接頭語、用語、または省略形を含めます。 たとえば、承認する作業者の外部キー フィールドはテーブルの拡張機能の一部として追加され、**WHS** はホスト モデル内の他の要素に専用である接頭語の 1 つです。 この場合、フィールドに **WHSApprovingWorker** という名前が付けられます。

## <a name="naming-members-in-extension-classes"></a>拡張クラス内のメンバーの名前を付ける
クラス レベルの変数および拡張クラスのメソッドは、拡張される型、および同じ型を拡張するその他の拡張クラスの両方で一意の名前を持つ必要があります。

+ メンバー名の先頭に接頭語、用語、または省略形を含めます。 たとえば、**WHS** がモデル内の他の要素で使用される接頭語の 1 つである場合、承認する作業者のクラス レベルの変数には、**WHSApprovingWorker** という名前が付けられます。 **approveWork** メソッドの名前を **WHSApproveWork** とつける場合 **WHS** はホスティング モデルでその他の要素によって使用される接頭語の 1 つです。

