---
title: "メッセージ センター、メッセージ バー、およびメッセージ詳細のよく寄せられる質問"
description: "このトピックでは、Microsoft Dynamics AX 2012 で使用されていた Infolog ウィンドウに代わる強力なメッセージング システムについて説明します。"
author: RobinARH
manager: AnnBe
ms.date: 11/09/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-platform
ms.technology: 
audience: Developer
ms.reviewer: robinr
ms.search.scope: Operations
ms.custom: 50401
ms.assetid: ce9d2312-c02e-4649-a7e4-33c3a06dfbd4
ms.search.region: Global
ms.author: tlefor
ms.search.validFrom: 2016-02-28
ms.dyn365.ops.version: AX 7.0.0
ms.translationtype: HT
ms.sourcegitcommit: 879eb9f2a63a8514791f74965005ed3e22bc0de7
ms.openlocfilehash: 695a2cfea75a3f9343c27eeff2f016d75bbc7ea6
ms.contentlocale: ja-jp
ms.lasthandoff: 04/20/2018

---

# <a name="message-center-message-bar-and-message-details-faq"></a>メッセージ センター、メッセージ バー、およびメッセージ詳細のよく寄せられる質問

[!include [banner](../includes/banner.md)]

このトピックでは、Microsoft Dynamics AX 2012 で使用されていた Infolog ウィンドウに代わる強力なメッセージング システムについて説明します。

Microsoft Dynamics AX 2012 は汎用ウィンドウを使用して、最近報告された情報のメッセージ、警告、またはエラーの一覧を表示します。 このウィンドウは、適切かつ一般的には情報ログまたは Infolog と呼ばれます。 情報ログは場合によっては有益なツールですが、「one size fits all」アプローチはメッセージの重要度を区別し、ユーザーを中断する必要性において効果がないと判断されました。 より豊富で強力なメッセージング システム:

-   コンテキストのあるメッセージの関連性強化
-   中断のレベル (なし、軽微、および中断) の強化
-   メッセージの種類間での明確さの強化
-   メッセージを表示する確定的な手段

## <a name="should-i-show-the-user-a-notification-a-warning-or-an-error"></a>通知、警告、またはエラーをユーザーに表示する必要がありますか。
これまで、**情報**、**警告** (**checkfailed**)、および**エラー**のステータスはシナリオ間で常に一貫して使用されていませんでした。 メッセージは、あるシナリオでは警告として、別のシナリオではエラーとして報告される場合があります。 表す状態を決定するとき、次の定義を使用します。

-   **通知** – 通知は、現在のユーザー活動に関係する可能性のあるイベントまたは関係しない可能性のあるイベントについてユーザーに通知します。 この通知は、ユーザー アクションまたはシステム イベントによって発生する場合があります。または、有用なプログラムからの情報を提供することができます。 通知は通常、即時のユーザー操作を必要としません。 **info()** アプリケーション プログラミング インターフェイス (API) を使用してユーザーに通知します。
-   **警告** – 警告は、今後問題が発生する可能性のある状態についてユーザーに警告します。 具体的には、警告は無効な状態のデータに使用されます。 無効なデータを使用しようと試みるとエラーが発生するかもしれませんが、現在のデータの状態が正しくないという事実はエラー状態ではありません。 *したがって、データの誤った状態についてユーザーに警告する必要があります*。 データ検証の問題を表現するには、**warning()** または **checkfailed()** API を使用します。
-   **エラー** - すでに発生した問題についてエラーがユーザーに警告します。 失敗したユーザー アクションは、エラー状態です。 エラーには、*非中断* (*パッシブ*) または*中断*を使用できます。 中断のないエラーでは、ユーザーは問題の修正を試みる前に他のアクティビティを実行できます。 中断エラーでは、ユーザーはエラー状態を修正するまで続行したりタスクを完了したりできません。 パッシブ (非中断) エラーを表現するには、**error()** API を使用します。 中断エラーを表現するには、**box::** API を使用します。

## <a name="how-do-i-determine-where-my-messages-are-shown"></a>メッセージがどこに表示されるかをどのように決定しますか。
メッセージング システムは、*確定的* です。 つまり、ユーザーにメッセージを表示するための最善の方法を決定するために、メッセージング システムは呼び出しのコンテキストを使用します。 メッセージは、ページの上部に表示されるメッセージ バーまたはナビゲーション バーに表示されるメッセージ センターに表示されます。 メッセージの場所は、メッセージの送信元コードによって異なります。

-   メッセージが同期のページ アクション (つまり、ユーザーが結果を待つ必要がある) によって発生した場合、結果は現在のページのメッセージ バーに表示されます。 (例外は、アクションが開始された後すぐに終了したスライダー ダイアログです。 スライダー ダイアログのメッセージが親のページにバブル アップします。)
-   メッセージが同期のアクション (切断) によって発生し、ユーザーが他のタスクを実行できる場合、またはそのアクションの処理中にも別のタスクにさえ移動できる場合は、結果はメッセージ センターに表示されます。

## <a name="how-do-i-change-my-existing-code-to-use-the-new-messaging-system"></a>新しいメッセージング システムを使用して既存のコードをどのように変更できますか。
*多くの場合、変更は必要ありません。* メッセージング フレームワークは、多くの一般的なシナリオの下位互換性を革新し維持するように設計されています。 場合によっては、プログラムがメッセージの内容を改善させることがあります。 または、使用法のガイダンスに合わせるために**警告()** の代わりに**エラー()**、または**エラー()** の代わりに**警告()** を使用するかもしれません (警告は無効なデータ、エラーは失敗したアクションのためのものです)。 それ以外の場合、スライダーのダイアログに表示されるメッセージが親ページに適していると判断できる場合があります。

### <a name="messaging-that-is-used-in-validation"></a>検証に使用されるメッセージング

Dynamics AX 2012 では、ユーザーが無効とみなされるデータまたは見つからないデータを入力した場合、前の有効な値がフィールドに返され、そのページから別のウィンドウの情報ログにフォーカスが移動します。 ユーザーがヘッド ダウン データ入力を行い、停止する必要がある場合、無効な値を保有するフィールドにフォーカスを戻し、対応しているエントリを入力します。 また、無効な値クリアされるので、ユーザーが単一の番号を入れ替えたり、単一の文字を誤って入力した場合でも、全体の値を再入力する必要があります。 「無効な値」メッセージが画面に残り、ユーザーは手動でクエリにする必要があります。 ただし、Dynamics の現在のバージョンでは、ページ上のメッセージ バーに検証メッセージ (同じ API を使用する) が表示されます。 無効な値は残っていますが、無効なフラグが立てられています。 ユーザーは引き続きデータを入力でき、データが保存される前の任意の時点で検証の問題を修正することができます。 検証の問題が修正されると、メッセージ バーのメッセージは無効になり、メッセージング システムがメッセージを削除します。

### <a name="legacy-api-support-info-warningcheckfailed-and-error"></a>旧 API サポート: info()、warning()/checkfailed()、および error()

従来の **info()**、**warning()**、および **error()** API はまだサポートされています。 ただし、これらの API がフレームワークの新しいメッセージング システム上に配置されるようになり、宛先が確定的になります。 簡単に言うと、API の使用がページから生成された場合、そのメッセージが同じページ上のメッセージ バーで表示されます。 (ドロップ ダイアログおよびスライダー ダイアログはどちらもページとみなされます。) 次の図は、ページ アクションに対応する**情報**、**警告**/**checkfailed**、および**エラー**のメッセージ バーまたは、**info()**、**warning()**、および**error()** から同期作成したメッセージを示しています。 

[![Messaging\_MessageBarTypes](./media/messaging_messagebartypes.jpg)](./media/messaging_messagebartypes.jpg) 

**注記:** スライダー ダイアログからメッセージング API が呼び出されても、メッセージが表示される前にそのスライダー ダイアログが閉じられると、メッセージはスライダー ダイアログの親ページのメッセージ バーに表示されます。 メッセージが表示される前にそのスライダー ダイアログ ボックスを閉じ、親ページが存在しない場合 (つまり、親とは、ワークスペース)、メッセージは、メッセージ センターにルーティングされます。 メッセージング API は必ずメッセージを表示します。 適切なホスト ページが見つからない場合は、メッセージがメッセージ センターに送信されます。

## <a name="the-message-api-for-explicit-add-and-remove-messages"></a>明示的なメッセージの追加および削除の Message() API
メッセージング システムは、従来の検証メッセージ API (**info()**、**warning()**/**checkfailed()**、および **error()**) をサポートしており、メッセージを確定的にメッセージバーまたはメッセージセンターに送信します。 メッセージング システムは、検証が再実行されたときにデータ検証に関連するメッセージ バー メッセージもクリアします。 また、メッセージング システムには、開発者が明示的にメッセージを追加したり削除したりする新しい **Message()** API が含まれます。 この API は、データ検証に必ずしも関連しないユーザー エクスペリエンスに関する情報メッセージを表示するのに便利です。 この場合、メッセージは現在のレコードが表示されるときに表示する必要があります。 ![メッセージング\_SingleMessageBarInfo](./media/messaging_singlemessagebarinfo.jpg)

    messageId = Message::Add(MessageSeverity::Info, "The customer is marked as inactive");

新しいレコードがページに表示されると、メッセージはクリアされます。

    Message::Remove(messageId);

以下のメッセージタイプがサポートされています: **MessageSeverity::Info**、**MessageSeverity::Warning**、および**MessageSeverity::Error**。 また、**Message()** API を使用するメッセージは確定的となります。 メッセージ バーまたはメッセージ センターにルーティングできます。

## <a name="the-messaging-api-and-batch-jobsasynchronouslong-running-background-tasks"></a>メッセージング API とバッチジョブ (非同期/実行時間の長いバックグラウンド タスク)
**info()**、**warning()**/**checkfailed()**、または **error()** が非同期プロセス (たとえば、SysOp を使用するバッチ ジョブ) から呼び出された場合、考慮するページ コンテキストはありません。 したがって、メッセージはメッセージ センターにルーティングされます。 

![Messaging\_EmptyMessageCenter](./media/messaging_emptymessagecenter.jpg)

### <a name="the-message-center"></a>メッセージ センター

メッセージ センターには、最大で 500 件のメッセージを保持できます。 その後、メッセージは最初に表示されたものから順にサイクルします。

#### <a name="why-are-asynchronous-tasks-messages-sent-to-the-message-center"></a>非同期タスク メッセージがメッセージ センターに送信されるのはなぜですか。

ページ上部にあるメッセージ バーは、何時間も前に開始されたバックグラウンド タスクではなく、現在のページに関する情報を表示するために使用されるため、(潜在的に) 長時間実行されているタスクはユーザーにメッセージ バーを表示しません。 場合によっては、多くのバックグラウンド タスクを実行しているユーザーは、タスクを完了しているときにページ間を移動し続けます。 したがって、現在のページに表示され、バックグラウンド タスクについてユーザーに通知されるメッセージは、見落とされたり無視されたりします。 したがって、設計上、バックグラウンド タスクはメッセージ センターにメッセージを送信します。 メッセージ センターに新しいメッセージが表示されると、非同期タスクの結果を待っている可能性のあるユーザーにお知らせが通知されます。

## <a name="error-should-i-interrupt-the-user"></a>エラー: ユーザーを中断する必要がありますか。
(バッチ ジョブまたはその他の操作) のタスクが失敗した場合は、ユーザーに受動的に通知することが適切な場合があります。 ユーザーはいつでも問題を修正して操作を再試行できるので、すぐに通知する必要はありません。 そのような場合、**error()** API は適切であり、ユーザーは割り込みダイアログを受け取りません。 ただし、それ以外の場合、ユーザーは問題が修正されるまでは続行できません。 たとえば、まだ無効なデータを保持しているページをユーザーが保存しようとする場合、クライアントはエラー ダイアログを表すことにより、ユーザーを中断させます。 これらのケースでは、ダイアログを提示することにより、ユーザーを中断させる方が適切である場合、**box::** API を使用する必要があります。 

![Messaging\_BoxAPI](./media/messaging_boxapi.jpg)

## <a name="the-message-center--messages-from-asynchronous-tasks"></a>メッセージ センター - 非同期タスクからのメッセージ
メッセージ センターは、ナビゲーション ウィンドウに表示されます。 ユーザーによる迅速なアクションを必要とせず、現在の作業を続行するために必要ではないメッセージが含まれています。 一般的な例にとしては、バッチ ジョブやレポート完了などのバック グラウンド処理からのフィードバックがあります。 メッセージ センターでは、**情報**、**警告**、および**エラー**のステータスを表示できます。 開かれる前に、メッセージ センターは前回開いたときから受信したメッセージの数を示します。

## <a name="message-bars--messages-for-synchronous-tasks-on-the-current-page"></a>メッセージ バー – 現在のページの同期タスクのメッセージ
メッセージ バーは、基本ページやドロップ ダイアログおよびスライダー ダイアログで利用できます。 メッセージ バーは、主にデータ検証に使用されます。 また、日付有効性のために使用されるメッセージなど、ページまたはデータの状態に関するメッセージの通信にも使用できます。 メッセージ バーでは、**情報**、**警告**、および**エラー**のステータスを表示できます。 すぐにユーザーの注意を求めるメッセージに、メッセージ バーを使用しないください。 メッセージ バーは、メッセージが最初に受け取られたときに表示されます。また、現在のページについてのみメッセージを伝達するのに使用する必要があります。 メッセージ バーに送信されるメッセージは、現在のページに関連付けられます。 したがって、ユーザーがメッセージ バーを含むページから離れて移動すると、それらのメッセージは新しいページに表示されません。 ただし、ユーザーが元のページに戻ってくる場合、ページのメッセージが再度表示されます。 メッセージに次の情報を含めます。

-   このメッセージを生成した条件。
-   ユーザーがメッセージを生成した状態を解決せずに続行した場合の結果。

**例**

-   この顧客は、非アクティブとしてマークされています。
-   コンテナーの検証に失敗しました。
-   伝票のトランザクションはバランスが残高が一致しません。

**プレゼンテーション** 

![Messaging\_MessageBarTypes](./media/messaging_messagebartypes.jpg)

## <a name="message-boxes--errors-and-immediate-notification-completed-synchronous-operations"></a>メッセージ ボックス – エラーや即時の通知 (完了した同期操作)
メッセージ ボックスを使用して、すぐに注意が必要な問題についてユーザーに警告します。 メッセージ ボックスはメッセージが読み取られたり消されるまでユーザーの続行が妨げられるため、ユーザーが後で処理できないメッセージに対してのみ使用する必要があります。 メッセージ ボックスに表示されるエラー メッセージに次の情報を含めます。

-   発生したエラー。
-   エラーの原因。
-   エラーを解決する方法に関する情報。

エラー メッセージは次の 2 つのコンポーネントを含める必要があります。

-   **主要な命令** – このテキストは太字で表示されます。
-   **メッセージの詳細** – このテキストは主要な命令の下に表示されます。

**例**

-   参照番号がバージョン %1 で使用されるので、参照番号を削除することはできません。
-   このエクスポートを実行するのに十分な権限があります。
-   カタログ インポート処理用のルート フォルダーが構成されていません。 仕入先カタログ インポート パラメータ フォームを使用してルート フォルダをコンフィギュレーションします。

**プレゼンテーション** 

![Messaging\_BoxAPI](./media/messaging_boxapi.jpg) 

**エラー** タイプのメッセージでは、メッセージを含むモーダルの「明るい色のボックス」で現在のページにオーバーレイすることでユーザーの操作をブロックします。

## <a name="messaging-from-dialogs-and-slider-dialogs"></a>ダイアログおよびスライダー ダイアログからのメッセージング
確定的なメッセージング システムが、現在のページにメッセージを送信しようとします。 ただし、すべてのダイアログまたはスライダー ダイアログからの呼び出しが、そのダイアログまたはスライダーにルーティングされるわけではありません。 場合によっては、メッセージング システムが代わりに親ページにメッセージを送信します。 この現象は、ダイアログまたはスライダが閉じられているときにメッセージング システムが呼び出されると発生する可能性があります。 場合によっては、ダイアログまたはスライダーが閉じるプロセスを開始するときにメッセージング システムを呼び出せますが、クライアントが有効な理由から閉じるプロセスを中断します。 したがって、「不可逆地点」があり、その時点を過ぎると、メッセージング システムはもはやダイアログまたはスライダー にメッセージを送信しようとせず、メッセージを親ページに送信します。 ユーザーがフォーム上の **OK** ボタンクリックすると、下記のコード例に示すように、終了シーケンスに入ります。

    closeOK()
    {
        // current form
        super(); // calls close()
        // parent or message center
    }
    Close()
    {
        // current form
        super();// point of no return
        // parent or message center
    }

クライアントが **closeOK()** または **close()** を直接呼び出す場合、最終的な結果がページまたは親ページである可能性があります。

## <a name="detailed-multi-result-messaging-that-uses-setprefix-and-the-message-details-pane"></a>SetPrefix() とメッセージの詳細ウィンドウを使用する詳細な複数結果のメッセージング
**SetPrefix()** の結果は、積極的にユーザーを中断しません。 代わりに、結果は収集され、保存されて、メッセージ バーまたはメッセージ センターの通知がユーザーに表示されます。 このメッセージ バーまたはメッセージ センターの通知は、関連するタスクが完了し、ユーザーが確認するメッセージがある可能性があることを示します。 *結果の通知*メッセージは、タスクによる **SetPrefix()** の最初の呼び出しを使ってメッセージをフレーム化します。 (この動作は、最初の呼び出しが結果の「タイトル」である Dynamics AX 2012 の動作に似ています。) 次の例では、テキスト「転記の結果」が **SetPrefix()** の最初の呼び出しから取得されます。 

![Messaging\_MessageDetailsMessageBar](./media/messaging_messagedetailsmessagebar.jpg) 

ユーザーは、メッセージ バーの **メッセージの詳細** リンクをクリックして、**メッセージの詳細** ウィンドウを開くことができます。 

![Messaging\_MessageDetailsPane](./media/messaging_messagedetailspane.jpg)

## <a name="setprefix--creating-a-collection-of-related-messages"></a>SetPrefix() – 関連メッセージのコレクションの作成
**SetPrefix()** を使用して、関連メッセージのコレクションを作成します。 この API は主に下位互換性がありますが、中断のない方法で表示されます。 結果ウィンドウは、直接開かれません。 代わりに、ユーザーは、結果メッセージをコレクションにグループ化するために **SetPrefix()** API を使用するタスクを開始したページにメッセージ バーを表示することで受動的に中断されます。 ユーザーにメッセージ コレクションの存在を通知するメッセージ バーには、コレクション内の最も重要なメッセージの重大度が反映されます。 たとえば、コレクションにエラーまたは警告が含まれていない場合、メッセージ バーは**情報**タイプです。 

![Messaging\_MessageDetailsMessageBar](./media/messaging_messagedetailsmessagebar.jpg) 

コレクションに 1 つまたは複数の **warning()** への呼び出しが含まれている場合、メッセージ バーは、**警告**タイプです。 

![Messaging\_MessageDetailsWarningMessageBar](./media/messaging_messagedetailswarningmessagebar.jpg) 

コレクションに 1 つまたは複数の **error()** への呼び出しが含まれている場合、メッセージ バーは、**エラー** タイプです。 

![Messaging\_MessageDetailsErrorMessageBar](./media/messaging_messagedetailserrormessagebar.jpg) 

**例**

    myMethod()
    {
        Setprefix("Posting Results");
        Setprefix("Invoice Account: DE-001);
        Info("Invoice FTI-000002 has been posted);
    }

**注記:** コレクションに親メッセージと単一のメッセージのみが含まれている場合、その単一のメッセージはメッセージ バーに送信され、SetPrefix ウィンドウは使用されません。

## <a name="setprefix-and-asynchronous-processes"></a>SetPrefix() および非同期プロセス
**SetPrefix()** の使用も確定的です。 つまり、**SetPrefix()** を使用して、ページ コンテキスト (たとえば、非同期バッチ操作) が存在しない場合、結果の通知はページに関連付けられていないメッセージ センターに送信されます。



