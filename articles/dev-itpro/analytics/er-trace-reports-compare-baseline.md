---
title: "生成されたレポート結果を追跡し、ベースライン値と比較する"
description: "このトピックでは、ベースライン レポート値で生成された ER レポートの結果を比較する方法に関する情報を提供します。"
author: NickSelin
manager: AnnBe
ms.date: 05/25/2018
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-platform
ms.technology: 
audience: Application User, Developer, IT Pro
ms.reviewer: kfend
ms.search.scope: Core, Operations
ms.custom: 220314
ms.assetid: 2685df16-5ec8-4fd7-9495-c0f653e82567
ms.search.region: Global
ms.author: nselin
ms.search.validFrom: 2018-04-01
ms.dyn365.ops.version: Release 8.0
ms.translationtype: HT
ms.sourcegitcommit: 2fc887668171175d436b9eb281a35c1c9d089591
ms.openlocfilehash: 1a598d0bd053c60c3f8df6b05ecb7ff15addfaa3
ms.contentlocale: ja-jp
ms.lasthandoff: 05/25/2018

---

# <a name="trace-generated-report-results-and-compare-them-with-baseline-values"></a><span data-ttu-id="b6a68-103">生成されたレポート結果を追跡し、ベースライン値と比較する</span><span class="sxs-lookup"><span data-stu-id="b6a68-103">Trace generated report results and compare them with baseline values</span></span>

[!include[banner](../includes/banner.md)]

<span data-ttu-id="b6a68-104">送信する電子ドキュメントを生成する ER 形式の結果を追跡できます。</span><span class="sxs-lookup"><span data-stu-id="b6a68-104">You can trace the results of ER formats that generate outgoing electronic documents.</span></span> <span data-ttu-id="b6a68-105">トレースの生成が有効である場合 (ER ユーザー パラメーター**デバッグ モードで実行**)、ER レポートが実行されるたびに ER 形式実行ログで新しいトレース レコードが生成されます。</span><span class="sxs-lookup"><span data-stu-id="b6a68-105">When trace generation is turned on (ER user parameter **Run in debug mode**), a new trace record is generated in the ER format execution log every time that an ER report is run.</span></span> <span data-ttu-id="b6a68-106">生成される各トレースには、次の情報が格納されます。</span><span class="sxs-lookup"><span data-stu-id="b6a68-106">The following details are stored in each trace that is generated:</span></span>

- <span data-ttu-id="b6a68-107">検証ルールによって生成されたすべての警告</span><span class="sxs-lookup"><span data-stu-id="b6a68-107">All warnings that were generated by validation rules</span></span>
- <span data-ttu-id="b6a68-108">検証ルールによって生成されたすべてのエラー</span><span class="sxs-lookup"><span data-stu-id="b6a68-108">All errors that were generated by validation rules</span></span> 
- <span data-ttu-id="b6a68-109">トレース レコードの添付ファイルとして格納されるすべての生成されたファイル</span><span class="sxs-lookup"><span data-stu-id="b6a68-109">All generated files that are stored as attachments of the trace record</span></span>

<span data-ttu-id="b6a68-110">任意の ER 形式の個々のベースライン アプリケーション ファイルを格納できます。</span><span class="sxs-lookup"><span data-stu-id="b6a68-110">You can store individual baseline application files for any ER format.</span></span> <span data-ttu-id="b6a68-111">ファイルは、実行されるレポートの予期される結果の説明時にベースライン ファイルと見なされます。</span><span class="sxs-lookup"><span data-stu-id="b6a68-111">Files are considered baseline files when they describe the expected results of reports that are run.</span></span> <span data-ttu-id="b6a68-112">トレースの生成がオンである間に実行された ER 形式に対してベースライン ファイルが使用可能な場合、トレースは、前述した詳細内容に加えて、ベースライン ファイルに生成された電子ドキュメントの比較の結果を格納します。</span><span class="sxs-lookup"><span data-stu-id="b6a68-112">If a baseline file is available for an ER format that was run while trace generation was turned on, the trace stores, in addition to the details that were mentioned earlier, the result of the comparison of the generated electronic document to the baseline file.</span></span> <span data-ttu-id="b6a68-113">ワンクリックで、生成された電子ドキュメントおよびそのベースライン ファイルを単一の zip ファイルで取得することもできます。</span><span class="sxs-lookup"><span data-stu-id="b6a68-113">In one click, you can also get the generated electronic document and its baseline file in a single zip file.</span></span> <span data-ttu-id="b6a68-114">Windiff などの外部ツールを使用して詳細な比較を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="b6a68-114">You can then do detailed comparison by using an external tool such as Windiff.</span></span>

<span data-ttu-id="b6a68-115">生成される電子ドキュメントが予想されるコンテンツを含むかどうかを分析するトレースを評価できます。</span><span class="sxs-lookup"><span data-stu-id="b6a68-115">You can evaluate the trace to analyze whether the electronic documents that are generated include the expected content.</span></span> <span data-ttu-id="b6a68-116">コード ベースが変更されたとき (たとえば、アプリケーションの新しいインスタンスに移行したとき、修正プログラム パッケージをインストールしたとき、またはコード変更を配置したとき)、ユーザー受け入れテスト (UAT) 環境でこの評価を行うことができます 。</span><span class="sxs-lookup"><span data-stu-id="b6a68-116">You can do this evaluation in a user acceptance testing (UAT) environment when the code base has been changed (for example, when you migrated to a new instance of the application, installed hotfix packages, or deployed code modifications).</span></span> <span data-ttu-id="b6a68-117">この方法で、評価は使用される ER レポートの実行に影響しないことを確認できます。</span><span class="sxs-lookup"><span data-stu-id="b6a68-117">In this way, you can make sure that the evaluation doesn't affect the execution of ER reports that are used.</span></span> <span data-ttu-id="b6a68-118">多くの ER レポートについては、無人モードで評価を実行できます。</span><span class="sxs-lookup"><span data-stu-id="b6a68-118">For many ER reports, the evaluation can be done in unattended mode.</span></span>

<span data-ttu-id="b6a68-119">この機能の詳細については、**7.5.4.3 IT サービス/ソリューションのテスト (10679)** 業務プロセスの一部である、**ER レポートの生成および結果の比較 (第 1 部)** および **ER レポートの生成および結果の比較 (第 2 部)** タスク ガイドを再生し、[Microsoft ダウンロード センター](https://go.microsoft.com/fwlink/?linkid=874684) からダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="b6a68-119">To learn more about this feature, play the **ER Generate reports and compare results (Part 1)** and **ER Generate reports and compare results (Part 2)** task guides, which are part of the **7.5.4.3 Test IT services/solutions (10679)** business process, and can be downloaded from the [Microsoft Download Center](https://go.microsoft.com/fwlink/?linkid=874684).</span></span> <span data-ttu-id="b6a68-120">これらのタスク ガイドでは、生成される電子ドキュメントを評価するためにベースライン ファイルを使用して、ER フレームワークを構成するプロセスについて説明します。</span><span class="sxs-lookup"><span data-stu-id="b6a68-120">These task guides walk you through the process of configuring the ER framework to use baseline files to evaluate generated electronic documents.</span></span>
