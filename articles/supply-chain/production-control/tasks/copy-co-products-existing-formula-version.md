--- 
title: "既存のフォーミュラ バージョンから連産品をコピー"
description: "この手順では、既存のフォーミュラ バージョンから、リリース済製品の別のフォーミュラ バージョンに連産品をコピーする方法を示します。"
author: YuyuScheller
manager: AnnBe
ms.date: 06/06/2016
ms.topic: business-process
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 
audience: Application User
ms.reviewer: yuyus
ms.search.scope: Operations
ms.search.region: Global
ms.search.industry: Manufacturing
ms.author: yuyus
ms.search.validFrom: 2016-06-30
ms.dyn365.ops.version: AX 7.0.0
ms.translationtype: HT
ms.sourcegitcommit: 7e0a5d044133b917a3eb9386773205218e5c1b40
ms.openlocfilehash: 80543780c423b5beac3ec57f4fa035e560aaa4ce
ms.contentlocale: ja-jp
ms.lasthandoff: 09/29/2017

---
# <a name="copy-co-products-from-an-existing-formula-version"></a>既存のフォーミュラ バージョンから連産品をコピー

[!include [task guide banner](../../includes/task-guide-banner.md)]

この手順では、既存のフォーミュラ バージョンから、リリース済製品の別のフォーミュラ バージョンに連産品をコピーする方法を示します。 連産品と関連付けられている少なくとも 1 つのフォーミュラ バージョンがあることが前提条件です。 この手順の作成に使用するデモ データの会社は USP2 です。


## <a name="find-a-released-product"></a>リリース済製品の検索
1. [リリースされた製品] に進みます。
2. [フィルターの表示] をクリックします。
    * フィルターのダイアログ ボックスで [生産] タイプのフィールドを追加しようとしています。  
3. [生産] タイプのフィールドを追加するために [フィルター フィールドの追加] をクリックします。
    * 次の手順で、[適用] を選択する前に手動で [生産タイプ] フィールドに式を入力する必要があります。 これは、リリース済製品一覧のフィルターを設定します。  
4. 手動で [生産タイプ] フィールドに式を入力します。
5. [適用] をクリックします。

## <a name="select-a-released-product"></a>リリース済製品の選択
1. 一覧で、目的のレコードを見つけ、選択します。
2. [フォーミュラ バージョン] をクリックします。
    * [技術アクション ペイン] で、[フォーミュラ バージョン] をクリックします。  

## <a name="copy-co-products"></a>連産物のコピー
1. [アクション ペイン] で、[フォーミュラ バージョン] をクリックします。
2. [連産品 (複数)] をクリックします。
3. [コピー] をクリックします。
4. [品目番号] フィールドで、値を入力または選択します。
5. [フォーミュラ バージョン] フィールドで、値を入力または選択します。
6. [OK] をクリックします。
7. ページを閉じます。


