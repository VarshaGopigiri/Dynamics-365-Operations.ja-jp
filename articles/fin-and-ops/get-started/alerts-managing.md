---
title: "警告のバッチの実行"
description: "このトピックでは、Microsoft Dynamics 365 for Finance and Operations の警告のバッチ処理に関する情報を提供します。"
author: tjvass
manager: AnnBe
ms.date: 06/08/2018
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 
audience: Application user
ms.reviewer: sericks
ms.search.scope: Operations
ms.search.region: Global
ms.author: tjvass
ms.search.validFrom: 2018-3-30
ms.dyn365.ops.version: Platform update 15
ms.translationtype: HT
ms.sourcegitcommit: 454368ab5a467002ebf973db97fd98e31885dfe0
ms.openlocfilehash: f4c874c148dc10ac658f659896009981962a5802
ms.contentlocale: ja-jp
ms.lasthandoff: 03/23/2018

---

# <a name="batch-processing-for-alerts"></a>警告のためのバッチ処理
[!include [banner](../includes/banner.md)]

警告は、Microsoft Dynamics 365 for Finance and Operations のバッチ処理機能により処理されます。 警告を通知するには、事前にバッチ処理を設定しておく必要があります。

Finance and Operations は、2 種類のイベントをサポートしています。

- 変更ベースのイベントによってトリガーされたイベント。 これらのイベントは、作成/削除および更新イベントと呼ばれることもあります。
- 期日に発生するイベント。

各イベント タイプごとにバッチ処理を設定できます。
        
## <a name="batch-processing-for-change-based-events"></a>変更ベースのイベントのバッチ処理
Finance and Operations は、バッチ処理が最後に実行されてから発生したすべての変更ベースのイベントを読み取ります。 変更ベースのイベントには、フィールドの更新、レコードの削除、およびレコードの作成が含まれます。 これらのイベントは、警告ルールに設定された条件と比較されます。 イベントがルールの条件と一致すると、バッチ処理により警告が生成されます。

### <a name="frequency-for-change-based-events"></a>変更ベースのイベントの頻度
変更ベースのイベントについては、システムによってイベントが記録された直後にそのイベントの処理をトリガするバッチ ジョブを設定することができます。 より頻繁に繰り返すバッチ ジョブを設定する場合、変更が行われると直ちにユーザーは警告を受け取ります。 ただし、バッチ処理の頻度の高さは、システム パフォーマンスに悪影響を与える可能性があります。

一方で、繰り返し頻度が低く、システム負荷が低いときにスケジュールされるバッチ ジョブは、システム パフォーマンスを向上させることがあります。 ただし、バッチ処理の頻度が低いと、時間どおりの警告についてのユーザーの要求を満たさない可能性があります。

したがって、変更ベースのイベントのバッチ処理の頻度を設定する際は、警告の適時性とシステム全体のパフォーマンス間のバランスを考慮する必要があります。 警告ルールを作成するユーザーの数が増えるほど、この点を考慮する必要性が高くなります。 頻度は、処理する必要があるイベント数に影響しません。 ただし、ルールを作成するユーザーが増えると、処理が必要なチェックも増加します。 このようなタイプのデータ交換はシステムのパフォーマンスに影響を与えることがあります。

#### <a name="the-risks-of-low-batch-frequency"></a>バッチ処理の処理頻度が低いことのリスク
変更ベース イベントのバッチ処理の頻度を低く設定すると、バッチが処理される前に警告ルールの条件に該当するデータが変更される場合があります。 したがって、警告を受信できなくなる場合があります。

たとえば、イベントが [顧客連絡先の変更] で条件が [顧客 = BB] を満たす場合に、警告をトリガーするように警告ルールを設定したとします。 つまり、顧客の連絡先が顧客 BB のために変更されると、イベントが記録されます。 ただし、バッチ処理システムは、バッチ処理の頻度がデータ入力より低くなるように設定されます。 イベント処理前に顧客名が **BB** から **AA** に変更される場合、データベース内のデータはルール **顧客 = BB** の条件に一致しなくなります。 したがって、イベントが最終的に処理されても、警告が生成されません。

### <a name="set-up-processing-for-change-based-alerts"></a>変更ベースの警告処理を設定する
1. [システム管理] &gt; [定期処理タスク] &gt; [警告] &gt; [変更に基づく警告] に移動します。
2. [変更に基づく警告] ダイアログ ボックスで、適切な情報を入力します。

## <a name="batch-processing-for-due-date-events"></a>期日イベントに関するバッチ処理
Finance and Operations のデータは、期日によって発生したすべてのイベントを検出し、これらのイベントは警告ルールに設定された条件と比較されます。 イベントがルールの条件と一致するとき、バッチ処理により警告が生成されます。

### <a name="frequency-for-due-date-events"></a>期日イベントの頻度
期日イベントの場合は、夜間または特定の時間帯に実行されるバッチ ジョブを設定して、システム負荷を分散できます。 毎日少なくとも 1 回実行するバッチ ジョブを設定することをお勧めします。 できるだけ早く警告が送信される必要がある場合、システム日付が変わった直後にバッチ処理を実行するよう設定します。 バッチ ジョブによって警告がすでに処理された後に発生する期日イベントのために警告を生成する必要がある場合は、同じ日に再度バッチ ジョブを実行することができます。

たとえば、バッチ ジョブは特定の日付に実行されています。 次に、その日に警告を発生させる必要がある期日がある発注書を作成します。 その日に警告を受信するには、発注書の作成後にバッチ ジョブを再度実行する必要があります。 ただし、その日に再度バッチ ジョブを実行しない場合、翌日のバッチ ジョブは、前日までに処理されなかった期日イベントを検出します。

> [!NOTE]
> バッチ処理を 1 日に複数回実行しても、同じ期日イベントおよび条件によって警告が繰り返されることはありません。 前回のバッチの実行後にシステム内に発生した変更によって期日に達した日付に対してのみ警告が生成されます。

### <a name="batch-processing-window"></a>バッチ処理ウィンドウ
法人の警告ルールの処理は、さまざまな理由で停止できます。 これらの理由には、休暇、システム エラー、またはしばらくの間バッチ ジョブの実行を妨げる他の問題が含まれます。

バッチ ジョブが数日間動いていないために、期日の警告が確実でなくなることを避けるため、バッチ処理ウィンドウを設定できます。 バッチ処理ウィンドウにより、指定した日数の間、バッチ ジョブが実行されないようにすることができます。

バッチ処理ウィンドウを設定する場合、期日の基準で定義された時間制限を警告が超過しても、警告ルールが処理されるときに警告が送信されます。 この時間制限およびバッチ処理ウィンドウで定義された期間を超えていなければ、警告が送信され続けます。 ただし、時間制限およびバッチ処理ウィンドウで定義された期間を超える場合、警告は送信されなくなります。

### <a name="set-up-processing-for-due-date-alerts"></a>期日の警告処理を設定する
1. [システム管理] &gt; [定期処理タスク] &gt; [警告] &gt; [期日の警告] に移動します。
2. [期日の警告] ダイアログ ボックスで、適切な情報を入力します。

