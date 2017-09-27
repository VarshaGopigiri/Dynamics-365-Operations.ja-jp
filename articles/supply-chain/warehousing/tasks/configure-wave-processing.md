--- 
title: "ウェーブ処理のコンフィギュレーション"
description: "このガイドでは、ウェーブが処理されるときに倉庫に対して生成される作業、およびウェーブが手動または自動で処理されるか判断する基準の設定方法について説明します。"
author: YuyuScheller
manager: AnnBe
ms.date: 06/07/2016
ms.topic: business-process
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 
audience: Application User
ms.reviewer: bis
ms.search.scope: Operations
ms.search.region: Global
ms.search.industry: Distribution
ms.author: mirzaab
ms.search.validFrom: 2016-06-30
ms.dyn365.ops.version: AX 7.0.0
ms.translationtype: HT
ms.sourcegitcommit: 9b947a02be981155053e33a4ef20e19bf2a194a5
ms.openlocfilehash: 50988c689995dbb957af760c9c2c3b823f557c86
ms.contentlocale: ja-jp
ms.lasthandoff: 07/27/2017

---
# <a name="configure-wave-processing"></a>ウェーブ処理のコンフィギュレーション

[!include[task guide banner](../../includes/task-guide-banner.md)]

このガイドでは、ウェーブが処理されるときに倉庫に対して生成される作業、およびウェーブが手動または自動で処理されるか判断する基準の設定方法について説明します。 販売注文、製造オーダー、またはかんばんオーダーのリリース済み明細行のあるウェーブと一致する、ウェーブ テンプレートおよびクエリを設定し、基準を指定します。 ウェーブ処理は倉庫管理モジュールで機能を使用する倉庫で使用され、在庫管理モジュールで機能を使用する倉庫では使用されません。 デモ データの会社 USMF でこの手順を確認できます。

1. [倉庫管理] > [設定] > [ウェーブ] > [ウェーブ テンプレート] の順に移動します。
2. [新規] をクリックします。
3. [ウェーブ テンプレート名] フィールドで、値を入力します。
    * ウェーブ テンプレートを設定する際は、販売注文、製造オーダー、かんばんのリリース済明細行と照合するテンプレートの順番を指定します。 明細行が倉庫または製造にリリースされる際、基準に合致する最初のウェーブ テンプレートが使用されます。 最も限定的な基準のテンプレートをリストの最初に置くことをお勧めします。 基準の範囲が広いほど、明細行が基準と合致する確率が高くなり、この結果、間違ったウェーブに明細行が割り当てられることになります。  
4. [ウェーブ テンプレートの説明] フィールドで、値を入力します。
5. [サイト] フィールドで値を入力または選択します。
    * USMF を使用している場合はサイト 2 を選択できます。  
6. [倉庫] フィールドで、値を入力または選択します。
    * USMF を使用している場合は倉庫 24 を選択できます。  
7. [ウェーブの作成を自動化] フィールドを [はい] に設定します。
    * 販売注文、製造オーダー、またはかんばんが倉庫にリリースされるときに、自動的にウェーブを作成するには、このオプションを選択します。  
8. [倉庫へのリリース時にウェーブを処理する] オプションを [はい] に設定します。 
    * 明細行が倉庫にリリースされる際に自動的にウェーブをプロセス処理し、作業を作成するには、このオプションを選択します。  
9. [ウェーブを自動的にリリースする] オプションを [はい] に設定します。 
    * 自動的にウェーブをリリースするには、このオプションを選択します。 ピッキング作業が作成され、モバイル デバイス上で利用できます。  
10. [未処理のウェーブへの割り当て] オプションを [はい] に設定します。 
    * 明細行はウェーブ テンプレートのクエリ フィルターに基づいてウェーブに割り当てられます。  
11. [しきい値に達したときにウェーブを自動処理する] オプションを [はい] に設定します。 
    * 値が [ウェーブのしきい値] フィールド グループで指定されている重量、出荷、明細行のしきい値に達したときに自動的にウェーブを処理するには、このオプションを選択します。 このオプションは、[ウェーブ テンプレート タイプ] フィールドで [出荷] が選択されている場合にのみ使用できます。  
12. [補充作業のリリースの自動化] オプションを [はい] に設定します。 
    * 要求ベースの補充作業を作成して自動的にリリースするには、このオプションを選択します。 ウェーブ テンプレートに補充ウェーブ メソッドを追加し、[ウェーブ需要] タイプの補充テンプレートを作成する必要があります。  
13. [メソッド] セクションを展開します。
    * ウェーブ テンプレートのメソッドによって各ウェーブの処理時に行われるアクションの順序を制御することができます。 たとえば、ウェーブの補充のメソッドがある場合があります。 メソッドを追加するとき、メソッドは手順の順序の適切な場所に自動的に一覧表示されます。 [補充作業のリリースの自動化] オプションを [はい] に設定している場合、ここで補充メソッドを追加する必要があります。  
    * ウェーブ属性はフィルターとして機能し、ウェーブを使用できる品目の種類を制限します。 たとえば、品目グループを指定できます。  
14. [保存] をクリックします。
15. ページを閉じます。
16. [倉庫管理] > [設定] > [倉庫管理パラメーター] の順に移動します。
17. [ウェーブ処理] セクションを展開します。
18. [ウェーブを処理するバッチ グループ] フィールドで、値を入力または選択します。
19. [ウェーブのバッチ処理] オプションを [はい] に設定します。
20. [ロックを待機 (ミリ秒)] フィールドに数値を入力します。
    * 配賦ステップが、他の配賦ステップでロックされたシステム リソースを待機する時間を、ミリ秒単位で入力します。 この時間を超えた場合、ウェーブは処理されず、エラー メッセージが表示されます。  
21. [保存] をクリックします。
22. ページを閉じます。
23. [生産管理] > [設定] > [生産管理パラメーター] の順に移動します。
24. [倉庫にリリース] フィールドで、オプションを選択します。
    * 販売注文とかんばん注文では、棚卸資産は注文が倉庫にリリースされる前に引当する必要があります。 そうしなければ、品門行または配賦行はウェーブで処理することはできません。 製造オーダーでは、[部分引当の許可] を選択するというオプションもあります。 たとえば、生産を開始する必要がある材料があり、プロセスを終了するための追加の材料が利用可能になるまで待機できる場合に役立ちます。 このオプションを選択する場合、追加の材料が使用可能になるときに、倉庫プロセスに手動でリリースを繰り返す必要があります。  
25. ページを閉じます。

