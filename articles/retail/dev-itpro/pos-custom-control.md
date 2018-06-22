---
title: "POS ビューへのカスタム コントロールの追加"
description: "このトピックでは、カスタム コントロールを追加することで、Dynamics 365 for Retail の [POS] ビューに表示される情報を改善する方法について説明します。"
author: mugunthanm
manager: AnnBe
ms.date: 09/15/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-365-retail
ms.technology: 
audience: Developer
ms.reviewer: robinr
ms.search.scope: Operations, Retail
ms.custom: 83892
ms.search.region: Global
ms.author: mumani
ms.search.validFrom: 2017-09-15
ms.dyn365.ops.version: AX 7.0.0, Retail September 2017 update
ms.translationtype: HT
ms.sourcegitcommit: 879eb9f2a63a8514791f74965005ed3e22bc0de7
ms.openlocfilehash: d1344d730d917e7e526ffdb0d8d3a2c765700c68
ms.contentlocale: ja-jp
ms.lasthandoff: 04/20/2018

---


# <a name="add-a-custom-control-to-a-pos-view"></a>POS ビューへのカスタム コントロールの追加

[!include [banner](../../includes/banner.md)]

Microsoft Dynamics 365 for Retail POS のビューに表示される情報を改善するために、カスタム コントロールを追加することができます。 カスタム コントロールを使用すると、既存の POS のビューにカスタム情報を追加できます。 カスタム コントロールは、POS 拡張フレームワークを使用して実装できます。

カート ビューでは、POS 画面レイアウト デザイナーを使用してカスタム コントロールを追加できます。 この場合、カスタム コントロールを任意の場所までドラッグして、コントロールの高さと幅を設定することもできます。 次に、拡張機能プロジェクトに拡張機能ロジックを記述します。

たとえば、次の図では、3 つのカスタム コントロールは画面レイアウト デザイナーを使用して追加されました。

![買い物カゴでの POS 画面レイアウト デザイナー](media/pos-custom-control-1.png)

現在、カート ビューのみでスクリーン レイアウ トデザイナーを使用してカスタム コントロールを追加できます。 その他のすべての画面については、拡張機能プロジェクトでレイアウトを行う必要があります。 画面レイアウト デザイナーを使用するメリットの 1 つは、画面の任意の場所にカスタム コントロールをドラッグできることです。 他の画面では、位置は固定されていますが、高さと幅を指定することで位置を変更できます。

## <a name="custom-control-matrix"></a>カスタム コントロール マトリックス

次のテーブルは、POS のカスタム コントロールをサポートするビューを示しています。

| POS ビュー                   | カスタム コントロールのサポート | 画面レイアウト デザイナーのサポート |
|----------------------------|--------------------------|---------------------------------|
| カート ビュー/トランザクション ページ | 有                      | 有                             |
| 顧客の詳細表示      | 有                      | 無                              |
| 製品詳細表示       | 有                      | 無                              |
| 顧客の追加/編集表示     | はい (仕掛品)   | 無                              |
| アドレスの追加/編集表示      | はい (仕掛品)   | 無                              |

> [!NOTE]
> カスタム コントロールは、次の製品バージョンでのみサポートされます。
> - **画面レイアウト デザイナーに基づいていないビューの場合:** Microsoft Dynamics 365 for Finance and Operations アプリケーション更新プログラム 3 および Microsoft Dynamics 365 for Retail アプリケーション更新プログラム 3
> - **画面レイアウト デザイナーに基づくビューの場合:** Microsoft Dynamics 365 for Finance and Operations アプリケーション更新プログラム 4 および Microsoft Dynamics 365 for Retail アプリケーション更新プログラム 4

## <a name="create-a-custom-control"></a>カスタム コントロールの作成

次の例は、既存の POS ビューの 1 つにカスタム コントロールを追加するために拡張機能を使用する方法を示しています。 この例では、製品の詳細ビューで表示される製品使用可能性についての情報が必要です。 この情報を表示するために、**場所**、**在庫**、**予約**、**注文**の 4 つの列を持つカスタム データ リストを追加します。 同じ手順を使用して、POS ビューにその他のカスタム情報を表示することができます。

1. 開発者仮想マシン (VM) で、Microsoft Visual Studio 2015 を起動します。
2. **ModernPos.sln** ファイルを RetailSDK\\POS から開きます。
3. **POS.Extensions** プロジェクトに新しいフォルダーを追加し、**SampleExtensions** と名前を付けます。
4. 新しい **SampleExtensions** フォルダーで、別のフォルダーを追加して **ViewExtensions** と名前を付けます。
5. **ViewExtensions** フォルダーで、別のフォルダーを追加して **SimpleProductDetails** と名前を付けます。

    > [!NOTE]
    > ビューを拡張する場合は、ナビゲーションとコードのメンテナンスを容易にするために、フォルダーの名前をビューと同じ名前にする必要があります。

6. **SimpleProductDetails** フォルダーで、新しい .html ファイルを追加し、**ProductAvailabilityPanel.html** と名前を付けます。 また新しい .ts ファイルを追加し、**ProductAvailabilityPanel.ts** という名前をつけます。 .html ファイルで、カスタム コントロールに表示したい情報すべてを追加できます。 .ts ファイルで、対応するロジックを追加します。

    カスタム コントロールは、カスタム情報を含む単純な HTML ページです。

7. **ProductAvailabilityPanel.html** ファイルを開いて、次のコードを貼り付けます。

    ```
    <!DOCTYPE html>
    <html lang="en" xmlns="http://www.w3.org/1999/xhtml">
        <head>
            <meta charset="utf-8" />
            <title></title>
        </head>
        <body>
            <!-- Note: The element ID differs from the ID that is generated by the POS extensibility framework. This 'template' ID isn't used by the POS extensibility framework. -->
            <script id="Microsot\_Pos\_Extensibility\_Samples\_ProductAvailabilityPanel" type="text/html">
                <h2 class="marginTop8 marginBottom8" data-bind="text: title"></h2>
                <div class="width400 grow col">
                    <div id="Microsot\_Pos\_Extensibility\_Samples\_ProductAvailabilityPanel\_DataList" data-bind="msPosDataList: dataList"></div>
                </div>
            </script>
        </body>
    </html>
    ```

    ファイルで、POS データ リスト コントロールを追加して製品の可用性情報を表示します。 また、コントロールの幅を指定します。

    完全なコードは RetailSDK\\Code\\POS\\Extensions\\SampleExtensions\\ViewExtensions\\SimpleProductDetails\\ProductAvailabilityPanel.html からコピーすることができます。

8. **ProductAvailabilityPanel.ts** ファイルを開いて、次のコードを貼り付けます。

    ```
    /**
        SAMPLE CODE NOTICE
        THIS SAMPLE CODE IS MADE AVAILABLE AS IS. MICROSOFT MAKES NO WARRANTIES, WHETHER EXPRESS OR IMPLIED,
        OF FITNESS FOR A PARTICULAR PURPOSE, OF ACCURACY OR COMPLETENESS OF RESPONSES, OF RESULTS, OR CONDITIONS OF MERCHANTABILITY.
        THE ENTIRE RISK OF THE USE OR THE RESULTS FROM THE USE OF THIS SAMPLE CODE REMAINS WITH THE USER.
        NO TECHNICAL SUPPORT IS PROVIDED. YOU MAY NOT DISTRIBUTE THIS CODE UNLESS YOU HAVE A LICENSE AGREEMENT WITH MICROSOFT THAT ALLOWS YOU TO DO SO.
    **/

    import {
        SimpleProductDetailsCustomControlBase,
        ISimpleProductDetailsCustomControlState,
        ISimpleProductDetailsCustomControlContext
    } from "PosApi/Extend/Views/SimpleProductDetailsView";
    import { ProxyEntities } from "PosApi/Entities";
    import { ArrayExtensions } from "PosApi/TypeExtensions";
    import { DataList, SelectionMode } from "PosUISdk/Controls/DataList";
    ```

    カスタム ロジックを書くために、POS のアプリケーション プログラミング インターフェイス (API) からコントロールやその他のデータ オブジェクトのリストをインポートしました。

次に、コンストラクターを追加して、製品の可用性情報でデータ リストを初期化する必要があります。 この方法で、ページに移動するときに、製品の可用性情報が読み込まれます。

> [!NOTE]
> ここではソース コードをコピーしませんでしたが、RetailSDK\\Code\\POS\\Extensions\\SampleExtensions\\ViewExtensions\\SimpleProductDetails\\ProductAvailabilityPanel.ts から完全なコードをコピーすることができます。

1. **SampleExtensions** フォルダーで新しい .json ファイルを追加し、**manifest.json** と名前を付け、次のコードを貼り付けます。

    ```
    {
        "$schema": "../manifestSchema.json",
        "name": "Pos_Extensibility_Samples",
        "publisher": "Microsoft",
        "version": "7.2.0",
        "minimumPosVersion": "7.2.0.0",
        "components": {
            "resources": {
                "supportedUICultures": [ "en-US" ],
                "fallbackUICulture": "en-US",
                "culturesDirectoryPath": "Resources/Strings",
                "stringResourcesFileName": "resources.resjson",
                "cultureInfoOverridesFilePath": "Resources/cultureInfoOverrides.json"
            },
            "extend": {
                "views": {
                    "SimpleProductDetailsView": {
                        "controlsConfig": {
                            "customControls": [
                                {
                                    "controlName": "productAvailabilityPanel",
                                    "htmlPath": "ViewExtensions/SimpleProductDetails/ProductAvailabilityPanel.html",
                                    "modulePath": "ViewExtensions/SimpleProductDetails/ProductAvailabilityPanel"
                                }
                            ]
                        }
                    }
                }
            }
        }
    }
    ```

    ランタイム中に、マニフェストはカスタム制御が **SimpleProductDetailsView** に追加されたことを POS に通知します。 前のコード例では、コントロールを読み込むために POS が必要とするすべてのメタデータを含めました。

    - **拡張** - 既存の POS 機能の拡張機能があることを POS に通知します。
    - **ビュー** – 拡張された既存の POS ビューを指定します。
    - **名前を表示** – 拡張されているビューを指定します。
    - **コンフィギュレーションのコントロール** - 追加するコントロールを指定します (例: **カスタム コントロール**)。
    - **コントロール メタデータ** - 名前、.html ファイル パスのパス、および typescript モジュールのパス (つまり、.ts ファイル) を指定します。

3. **extensions.json** ファイルを開いて、次のコードを貼り付けます。

    ```
    {
        "extensionPackages": [
            {
                "baseUrl": "SampleExtensions"
            }
        ]
    }
    ```

    extensions.json ファイルで、手持ちのさまざまな拡張機能を指定します。 この場合、新しい拡張フォルダーを追加しました。 したがって、そのフォルダーを指定する必要があります。
    
    > [!NOTE]
    > 各拡張子フォルダーまたは指定したパッケージには、マニュフェストが必要です。

4. **tsconfig.json** ファイルを開いて、拡張子を含めます。 次のコードをファイルに貼り付けます。

    ```
    "extends": "../tsconfigs/tsmodulesconfig",
    "exclude": [
        // "SampleExtensions"
    ],
    ```

## <a name="test-the-extension"></a>拡張のテスト

1. F5 キーを押し、POS を展開してカスタマイズをテストします。
2. POS が開始された後にサインインします。 次に、任意の製品を検索し、製品詳細ビューを開きます。 追加したカスタム コントロールが表示されました。 次に例を示します。

    ![製品の詳細ビューに表示された製品の可用性情報](media/pos-custom-control-2.png)

このサンプルの完全なコードは RetailSDK\\Code\\POS\\Extensions\\SampleExtensions\\ViewExtensions\\SimpleProductDetails からコピーすることができます。
