---
title: "コードの移行 - コンテキスト メニュー"
description: "新しいプログラミング モデルには、コンテキスト メニュー (ショートカット メニュー) が必要です。 この記事では、Microsoft Dynamics AX 2012 から Microsoft Dynamics 365 for Finance and Operations へのコンテキスト メニュー コードのマイグレーション プロセスについて説明します。 また、コンテキスト メニューの UX ガイドラインも含まれます。"
author: jasongre
manager: AnnBe
ms.date: 06/20/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-platform
ms.technology: 
audience: Developer
ms.reviewer: robinr
ms.search.scope: Operations
ms.custom: 16301
ms.assetid: 8f3b62f2-4de6-4ea3-b3e6-1101d0fe308e
ms.search.region: Global
ms.author: jasongre
ms.search.validFrom: 2016-02-28
ms.dyn365.ops.version: AX 7.0.0
ms.translationtype: HT
ms.sourcegitcommit: 879eb9f2a63a8514791f74965005ed3e22bc0de7
ms.openlocfilehash: fc4d971ddd894d478482104c4be6c5ebcd463d9c
ms.contentlocale: ja-jp
ms.lasthandoff: 04/20/2018

---

# <a name="code-migration---context-menus"></a>コードの移行 - コンテキスト メニュー

[!include [banner](../includes/banner.md)]

新しいプログラミング モデルには、コンテキスト メニュー (ショートカット メニュー) が必要です。 この記事では、Microsoft Dynamics AX 2012 から Microsoft Dynamics 365 for Finance and Operations へのコンテキスト メニュー コードのマイグレーション プロセスについて説明します。 また、コンテキスト メニューの UX ガイドラインも含まれます。

Microsoft Dynamics AX 2012 以前のバージョンでは、開発者が **PopupMenu** クラスを使用して右クリックのコンテキスト メニュー (ショートカット メニュー) を変更していました。 このクラスは、Web 上で利用できない Microsoft Windows アプリケーション プログラミング インターフェイス (API) に依存していました。 Finance and Operations では、同様の機能を提供する代わりに **ContextMenu** API が作成されました。 以前は、**context()** メソッドと **showContextMenu()** メソッドのオーバーライドは、特定のコントロールのコンテキスト メニューを変更するためのエントリ ポイントでした。 これらの上書きには通常、コンテキスト メニューにオプションを追加したり、ユーザーの選択を処理するためのコードが含まれていました。 ユーザーの選択を処理するコードは、待機モデルを使用していました。 Finance and Operations では、これらのオーバーライドが削除され、待機モデルは消去されています。 代わりに、開発者はオプションにコンテキスト メニューを追加する **getContextMenuOptions()** およびユーザーの選択を処理する **selectedMenuOption()** の 2 つのオーバーライドを作成する必要があります。

## <a name="migrate-context-menu-code-in-finance-and-operations"></a>Finance and Operations でのコンテキスト メニュー コードの移行
**PopupMenu** API から **ContextMenu** API への移行は、3 つの主な段階に分けることができます。

### <a name="step-1-add-a-constant-for-each-menu-option-that-must-be-added"></a>手順 1 追加する必要のあるメニュー オプションごとの定数の追加

**PopupMenu** クラスの古い **insertItem()** メソッドは、追加されたメニュー オプションの識別子を返しました。 この識別子は、将来の参照のために変数に保存されました。 開発者は Finance and Operations でメニュー識別子を定義するため、各オプションの定数を定義してコードの可読性を高めることをお勧めします。

-   フォーム レベルでは、コンテキスト メニューに追加されている各メニュー オプションの定数を追加します。 値は各コンテキスト メニュー内で一意でなければなりません。 フォームまたはコントロールで別の変数と競合する場合、古い変数名を変更する必要があることに注意してください。

#### <a name="before"></a>以前

    public void context()
    {
        ...
        int listCreateRoot = listMenu.insertItem("@SYS5480");
        ...

#### <a name="after"></a>変更後

    [Form]
    public class MainAccount extends FormRun
    {
        ...
        public const int listCreateRoot = 1;
        ...

### <a name="step-2-build-the-context-menu"></a>手順 2 コンテキスト メニューの構築

サブメニューとメニュー オプションのリストを構築し、コントロールのコンテキスト メニューに追加します。

1.  コントロールの **getContextMenuOptions()** メソッドの上書きを追加します。
2.  新しいコンテキスト メニューと、メニューに追加するオプションを保持するリストを作成します。
    -   ContextMenu メニュー = 新しい ContextMenu();
    -   List menuOptions = new List(Types::Class);

3.  一覧にメニュー オプションを追加:
    -   ContextMenuOption オプション = ContextMenuOption::Create(label,identifier);
    -   menuOptions.addEnd(option);

4.  メニューにオプションのリストを追加します。
    -   menu.ContextMenuOptions(menuOptions);

5.  **return** ステートメントを変更します。
    -   return menu.Serialize();

### <a name="step-3-process-the-user-selection-from-the-context-menu"></a>手順 3 コンテキスト メニューからのユーザーの選択を処理

1.  コントロールの **selectedMenuOption()** メソッドの上書きを追加します。
2.  オプション処理用の **switch()** ステートメントを、このオーバーライドに移動します。

## <a name="code-example"></a>コードの例
このセクションでは、Dynamics AX 2012 から Finance and Operations へのコンテキスト メニューの移行について説明します。 **MainAccount** フォームが例として使用されます。

### <a name="original-code"></a>オリジナル コピー

    public void context()
    {       
        PopupMenu  listMenu        = new PopupMenu(element.hWnd());
        int        listCreateRoot  = listMenu.insertItem("@SYS5480");
        int        selectedMenu;
        selectedMenu = listMenu.draw();
        switch (selectedMenu)
        {
            case -1:
                break;
            case listCreateRoot:
                mainAccount_ds.create();
                break;
            default:
                break;
        }
    }

### <a name="migrated-code"></a>移行されたコード

    // Define new form-level constant for each context menu option
    public const int listCreateRoot = 1;
    // Define new override on the control for building the context menu
    public str getContextMenuOptions()
    {
        str ret;
        ContextMenu menu = new ContextMenu(); 
        ContextMenuOption option = ContextMenuOption::Create("@SYS5480", listCreateRoot);
        List menuOptions = new List(Types::Class); 
        // Add label and ID of menu option
        menuOptions.addEnd(option); 
        menu.ContextMenuOptions(menuOptions);
        return menu.Serialize();
    }
    // Define new override on the control for processing the user selection
    public void selectedMenuOption(int selectedOption)
    {
        switch (selectedOption)
        {
            case -1:
                break;
            case listCreateRoot:
                mainAccount_ds.create();
                break;
            default:
                break;
        }
    }

## <a name="ux-guidelines-for-context-menus"></a>コンテキスト メニューの UX ガイドライン
コンテキスト メニューを移行する際、次のガイドラインを考慮してください。

-   最も重要なコマンドは、メニューの先頭にある必要があります。
-   右クリックの対象となる要素の現在の状態に適用されないコマンドを削除します。
-   右クリックはショートカットです。 したがって、コンテキスト メニューのコマンドは、**常に**ページの他の場所で利用できる必要があります。
-   コンテキスト メニューのサブメニューを作成しないでください。 サブメニューは使いにくくタッチ対応ではありません。
-   メニュー項目の数を 5 に制限します。





