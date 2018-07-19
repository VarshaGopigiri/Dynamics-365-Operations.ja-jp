---
title: "オーバレイを拡張機能にリファクタリングできるように、モデルの制限を緩和する"
description: "このトピックでは、オーバーレイを拡張機能にリファクタリングできるように、モデルの制限を緩和する方法について説明します。 Microsoft Dynamics 365 for Finance and Operations 8.0 ではモデルがシールされているため、制限の緩和が必要となります。"
author: CGarty
manager: AnnBe
ms.date: 05/01/2018
ms.topic: index-page
ms.prod: 
ms.service: dynamics-ax-platform
ms.technology: 
audience: Developer
ms.reviewer: robinr
ms.search.scope: Operations
ms.custom: 268724
ms.assetid: 
ms.search.region: Global
ms.author: CGarty
ms.search.validFrom: 2018-04-01
ms.dyn365.ops.version: Platform update 14
ms.translationtype: HT
ms.sourcegitcommit: e502540bc25d62d3b75c71b45bae64a9cf4a1dd2
ms.openlocfilehash: 04b2e82185b8cc1ec2813585d6c8fb35ad2b7fc6
ms.contentlocale: ja-jp
ms.lasthandoff: 05/04/2018

---

# <a name="relax-model-restrictions-to-enable-the-refactoring-of-over-layering-into-extensions"></a><span data-ttu-id="4d2f6-104">オーバレイを拡張機能にリファクタリングできるように、モデルの制限を緩和する</span><span class="sxs-lookup"><span data-stu-id="4d2f6-104">Relax model restrictions to enable the refactoring of over-layering into extensions</span></span>

[!INCLUDE [banner](../includes/banner.md)]

## <a name="introduction"></a><span data-ttu-id="4d2f6-105">概要</span><span class="sxs-lookup"><span data-stu-id="4d2f6-105">Introduction</span></span> ##
<span data-ttu-id="4d2f6-106">Dynamics 365 for Finance and Operations 8.0 およびこれ以降のすべてのリリースでは、Microsoft のコードをカスタマイズすることはできません。</span><span class="sxs-lookup"><span data-stu-id="4d2f6-106">Dynamics 365 for Finance and Operations 8.0, and all subsequent releases, will not allow Microsoft’s code to be customized by using over-layering.</span></span> <span data-ttu-id="4d2f6-107">動作の変更や追加には、拡張機能を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4d2f6-107">Instead, extension capabilities should be used to modify and add behavior.</span></span> <span data-ttu-id="4d2f6-108">「オーバーレイを使用しない」という制限は、すべてのお客様が最新の機能と修正プログラムを利用できるように、シンプルで更新しやすく、常に最新のバージョンが実行されるクラウド ERP サービスをお客様に提供するための製品の展開において、重要な要素です。</span><span class="sxs-lookup"><span data-stu-id="4d2f6-108">The "no over-layering" restriction is a key part of the evolution of the product toward providing customers with a cloud ERP service that is simple to update and always running the most recent version possible to allow all customers to receive the benefits of the latest features and fixes.</span></span>

<span data-ttu-id="4d2f6-109">コードを 8.0 以降にアップグレードした後、コンパイルを行うと、オーバーレイを使用するカスタマイズが残っている場合、エラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="4d2f6-109">After you upgrade code to 8.0 or later, when you compile, any customizations that still use over-layering will cause errors.</span></span> <span data-ttu-id="4d2f6-110">コードのリファクタリングを行うには、オーバーレイされているモデルのモデル記述子ファイルで一時的にオーバーレイの制限を緩和できます。</span><span class="sxs-lookup"><span data-stu-id="4d2f6-110">To refactor the code, the over-layering restriction can be temporarily relaxed in the model descriptor file of the model that is being over-layered.</span></span> <span data-ttu-id="4d2f6-111">この一時的な緩和は、開発環境およびデモ環境でのみ利用できます。スタンダード承認テスト以上のサンドボックス環境や実稼働環境などのランタイム環境には適用できません。</span><span class="sxs-lookup"><span data-stu-id="4d2f6-111">This temporary relaxation only works on development and demo environments and cannot be deployed on runtime environments like Standard Acceptance Test (or higher) sandbox or production environments.</span></span> <span data-ttu-id="4d2f6-112">記述子の制限を緩和することで、段階的にコードを拡張機能へとリファクタリングし、コンパイル、実行、テストを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="4d2f6-112">Relaxing the descriptor restriction will enable the code to be gradually refactored to extensions, compiled, run, and then tested.</span></span> 

## <a name="detailed-process"></a><span data-ttu-id="4d2f6-113">詳細なプロセス</span><span class="sxs-lookup"><span data-stu-id="4d2f6-113">Detailed process</span></span> ##
<span data-ttu-id="4d2f6-114">モデルの制限を緩和するには、以下の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="4d2f6-114">Complete the following steps to relax model restrictions.</span></span> <span data-ttu-id="4d2f6-115">この手順は、クラウド環境で実行することも、ローカルの仮想マシン (VM) で実行することもできます。</span><span class="sxs-lookup"><span data-stu-id="4d2f6-115">This procedure can be completed on a cloud environment or a local virtual machine (VM).</span></span>

1. <span data-ttu-id="4d2f6-116">Dynamics 365 for Finance and Operations 8.0 の開発環境を展開します。</span><span class="sxs-lookup"><span data-stu-id="4d2f6-116">Deploy a Dynamics 365 for Finance and Operations 8.0 development environment.</span></span> 
2. <span data-ttu-id="4d2f6-117">Lifecycle Services (LCS) のコード アップグレード サービスを実行して、ソリューションをアップグレードします。</span><span class="sxs-lookup"><span data-stu-id="4d2f6-117">Run the Lifecycle Services (LCS) code upgrade service to upgrade the solution.</span></span>
3. <span data-ttu-id="4d2f6-118">コンパイルできるように、必要に応じて Microsoft のモデルでのオーバーレイを一時的に許可します。</span><span class="sxs-lookup"><span data-stu-id="4d2f6-118">Temporarily allow over-layering in Microsoft models as needed to enable compilation.</span></span>
    
    <span data-ttu-id="4d2f6-119">a.</span><span class="sxs-lookup"><span data-stu-id="4d2f6-119">a.</span></span> <span data-ttu-id="4d2f6-120">C:\AOSService\PackagesLocalDirectory フォルダーで目的のモデルを見つけます。</span><span class="sxs-lookup"><span data-stu-id="4d2f6-120">Locate the desired model within the C:\AOSService\PackagesLocalDirectory folder.</span></span>
    
    <span data-ttu-id="4d2f6-121">b.</span><span class="sxs-lookup"><span data-stu-id="4d2f6-121">b.</span></span> <span data-ttu-id="4d2f6-122">記述子のフォルダーに移動します。</span><span class="sxs-lookup"><span data-stu-id="4d2f6-122">Navigate to the descriptor folder.</span></span> <span data-ttu-id="4d2f6-123">たとえば、\Currency\Descriptor フォルダーなどです。</span><span class="sxs-lookup"><span data-stu-id="4d2f6-123">For example, \Currency\Descriptor.</span></span>
    
    <span data-ttu-id="4d2f6-124">c.</span><span class="sxs-lookup"><span data-stu-id="4d2f6-124">c.</span></span> <span data-ttu-id="4d2f6-125">XML ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="4d2f6-125">Open the XML file.</span></span> <span data-ttu-id="4d2f6-126">たとえば、Currency.xml ファイルなどです。</span><span class="sxs-lookup"><span data-stu-id="4d2f6-126">For example, Currency.xml.</span></span>
    
    <span data-ttu-id="4d2f6-127">d.</span><span class="sxs-lookup"><span data-stu-id="4d2f6-127">d.</span></span> <span data-ttu-id="4d2f6-128">**Customization** メタデータ要素を **AxModelInfo** メタデータ要素の内側に追加して、**AllowAndWarn** を指定します。ファイルの冒頭はこのようになります。</span><span class="sxs-lookup"><span data-stu-id="4d2f6-128">Add a **Customization** metadata element inside the **AxModelInfo** metadata element to indicate **AllowAndWarn** so that the start of the file now looks like this.</span></span>
            
```xml
<AxModelInfo xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
<AppliedUpdates xmlns:d2p1="http://schemas.microsoft.com/2003/10/Serialization/Arrays" />
<Customization>AllowAndWarn</Customization>
```
    
4. <span data-ttu-id="4d2f6-129">オーバーレイをリファクタリングして拡張機能にし、テストします。</span><span class="sxs-lookup"><span data-stu-id="4d2f6-129">Refactor over-layering to extensions and test.</span></span> <span data-ttu-id="4d2f6-130">​オーバーレイを削除できるように、拡張機能を利用します。</span><span class="sxs-lookup"><span data-stu-id="4d2f6-130">Make use of extension capabilities to eliminate over-layering.</span></span> <span data-ttu-id="4d2f6-131">必要な場合には、拡張機能の要求を行います。</span><span class="sxs-lookup"><span data-stu-id="4d2f6-131">If needed, make extensibility requests.</span></span>
5. <span data-ttu-id="4d2f6-132">Microsoft のモデルに対する一時的な変更を元に戻します。</span><span class="sxs-lookup"><span data-stu-id="4d2f6-132">Revert the temporary changes to Microsoft models.</span></span> <span data-ttu-id="4d2f6-133">オーバーレイを使用するモデルの展開はできなくなるため、記述子ファイルを更新することが重要です。</span><span class="sxs-lookup"><span data-stu-id="4d2f6-133">The deployment of a model that uses over-layering will not be possible, so it's important to ensure that the descriptor file is updated.</span></span>
 
## <a name="prototyping-extensibility-requests"></a><span data-ttu-id="4d2f6-134">拡張機能の要求のプロトタイピング</span><span class="sxs-lookup"><span data-stu-id="4d2f6-134">Prototyping extensibility requests</span></span> ##
<span data-ttu-id="4d2f6-135">拡張機能を使用するようにソリューションを徐々に移行していく中で、ソリューションにおける課題を解消するために拡張機能の要求が必要になることがあります。</span><span class="sxs-lookup"><span data-stu-id="4d2f6-135">As a solution gradually migrates toward extensions, there will be places where an extensibility request is required to unblock the solution.</span></span> <span data-ttu-id="4d2f6-136">ソリューションの課題を解消し、拡張機能を使用するための移行プロセスをスムーズに進めるために何が必要なのかを十分に把握するために、拡張機能のプロトタイプを別のモデルとして作成することができます。</span><span class="sxs-lookup"><span data-stu-id="4d2f6-136">To fully understand what is needed to unblock a solution and smooth the migration process toward extensions, extension capabilities can be prototyped in a separate model.</span></span>

1. <span data-ttu-id="4d2f6-137">オーバーレイをリファクタリングするために必要な拡張機能を特定します。</span><span class="sxs-lookup"><span data-stu-id="4d2f6-137">Identify the need for an extension capability to refactor some over-layering.</span></span>
2. <span data-ttu-id="4d2f6-138">拡張機能のプロトタイプを拡張機能プロトタイプ モデルに追加します。</span><span class="sxs-lookup"><span data-stu-id="4d2f6-138">Add a prototype of extension capabilities into an extension prototype model.</span></span>

   - <span data-ttu-id="4d2f6-139">列挙型の拡張については、対象の列挙型のコピーを拡張機能プロトタイプ モデルに追加して、拡張可能の設定を行います。</span><span class="sxs-lookup"><span data-stu-id="4d2f6-139">For enumeration extensibility, put a copy of the enumeration into the extension prototype model and mark it as extensible.</span></span>
    
   - <span data-ttu-id="4d2f6-140">抽出メソッドの拡張については、抽出されたメソッドとオーバーレイされたオリジナルのプロトタイプを拡張機能プロトタイプ モデルに作成します。</span><span class="sxs-lookup"><span data-stu-id="4d2f6-140">For extract method extensibility, prototype the extracted method and the overlayered original in the extension prototype model.</span></span>
    
3. <span data-ttu-id="4d2f6-141">プロトタイプの拡張機能を使用します。</span><span class="sxs-lookup"><span data-stu-id="4d2f6-141">Use the prototype extension capability.</span></span>
4. <span data-ttu-id="4d2f6-142">プロトタイプの拡張機能で問題がなければ、対応する要求を作成します。</span><span class="sxs-lookup"><span data-stu-id="4d2f6-142">If the prototype extension capability is sufficient, create a matching request.</span></span>
5. <span data-ttu-id="4d2f6-143">その拡張機能をプラットフォームやアプリケーションに実装する際には、プロトタイプの拡張機能および関連するオーバーレイはすべて、拡張機能プロトタイプ モデルから削除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4d2f6-143">When the extension capability has been implemented in the platform or application, the prototype extension capability and any associated over-layering should be removed from the extension prototype model.</span></span>
6. <span data-ttu-id="4d2f6-144">ソリューションのすべてのオーバーレイが拡張機能にリファクタリングされ、拡張機能プロトタイプ モデルが空になったら、ソリューションのリファクタリングは完了です。</span><span class="sxs-lookup"><span data-stu-id="4d2f6-144">After the solution has all over-layering refactored to extensions and the extension prototype model is empty, the solution refactoring is complete.</span></span>
