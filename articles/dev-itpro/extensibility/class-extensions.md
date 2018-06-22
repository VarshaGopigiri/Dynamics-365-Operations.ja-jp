---
title: "クラスの拡張機能"
description: "この記事では、X++ で新しいクラス拡張モデルについて説明します。"
author: pvillads
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
ms.assetid: 271dabb1-ecb8-497f-b866-397733a954b8
ms.search.region: Global
ms.author: pvillads
ms.search.validFrom: 2016-05-31
ms.dyn365.ops.version: Platform update 1
ms.translationtype: HT
ms.sourcegitcommit: 879eb9f2a63a8514791f74965005ed3e22bc0de7
ms.openlocfilehash: b8e41fef9535cdfc98c4709b609646c28c6007b0
ms.contentlocale: ja-jp
ms.lasthandoff: 04/20/2018

---

# <a name="class-extensions"></a>クラスの拡張機能

[!include [banner](../includes/banner.md)]

この記事では、X++ で新しいクラス拡張モデルについて説明します。

オーバーレイは非常に侵入的な機能なので、使用しないことをお勧めします。 オーバーレイに代わる方法は、拡張です。 拡張子を使用すると、既存のコンポーネントを新しいモデルで拡張できます。 拡張子は維持しやすいですが、カスタマイズ時に拡張できる量は限られています。 メタデータを拡張する豊富な方法があります。 たとえば、テーブルに新しいフィールドを追加できます。 この記事では、X++ コードを拡張する方法について説明し、これらのモデルを再コンパイルせずに他のモデルで定義されているコンポーネントにメソッドと状態を追加できるようにします。 X++ 用の同様のコード拡張メカニズムが存在し、C\# で対応する機能の後でモデル化されます。 このメカニズムにより、クラスは、命名規則に従い public static メソッドをホストすることにより、拡張クラスとして指定することができます。 既存の機能では、拡張メソッドに渡される最初の引数の型は、拡張する型です。 この記事に記載する内容はその方向の次のステップであり、役に立つありのままの拡張についての説明です。 オブジェクト指向のプログラミングで、*拡張*という用語には、適切に定義された意味があります。 「クラス B がクラス A を拡張する」である場合、B が A から継承し、通常のオブジェクト指向の規則が暗示されていることを意味します。 実際、この用語は、この関係を表現するクラス宣言で使用される X++ 構文でも使用されます。 同時に複数のモデルから寄せられたメタデータについて*拡張*という用語を使用して説明します。 *拡張*という用語の過負荷を避けるために、代わりに*クラス強化*という用語を使用して、基本モデルのクラス A とそれに依存するモデルのクラス B の間の関係を指定します。ここで、B はそのモデルのコンテキストでクラス A に追加の機能を提供します。 ただし、*拡張クラス*という用語が一般的であるため、引き続き使用します。

## <a name="the-effective-class-concept"></a>有効なクラスの概念
強化されたコンポーネントのパブリック メンバー、およびそのコンポーネントを強化するすべてのクラスの拡張機能のすべてのパブリック メンバーで構成されるクラスに条件を設けるために役立ちます。 このクラスは、指定されたモデルの有効なクラスと呼ばれます。 次の図は、基本モデルで定義された、**MyArtifact** および **MyArtifact**の拡張クラスを持つ 2 つの依存モデルで定義されたコンポーネント **MyModel** を示しています。 [![ベースモデル MyModel で定義されているコンポーネント MyArtifact、および MyArtifact の拡張クラスを持つ 2 つの依存モデル](./media/extensions-11.png)](./media/extensions-11.png)この例では、有効なクラスは、すべてのオリジナルのメソッドおよび拡張クラスからのすべてのパブリック コンポーネントを含む拡張モデルのクラスです。 有効なクラスは、特定のモデルで定義されているクラスの拡張機能のみが含まれているため、すべてのモデルで同じではありません。 次の図は、**MyExtensionModel** モデルの **MyArtifact** の有効クラスを示しています。 [![MyExtensionModel で MyArtifact の有効なクラス](./media/extensions-21.png)](./media/extensions-21.png) **MyModel** という名前のモデル内の **MyClass** という名前のクラスを使用して、クラス拡張について説明します。

    class MyClass
    {
        public int mycState;
        public str mycMethod(int arg)
        {
            // ...
        }
    }

**MyModel** の上に構築される (つまり、MyModel に依存する) 拡張モデル (**MyExtensionModel**) に拡張クラスを導入することで、**MyClass** に新しいメソッドと状態を追加できます。

## <a name="extension-class-declarations"></a>拡張子のクラス宣言
拡張子クラスに **ExtensionOf** 属性によって飾られているクラスで、**\_拡張子**接尾語という名も持っています。 (この名前付けの制限は、後で削除される可能性があります。) 拡張クラスの名前は、それ以外の場合重要ではありません。 このクラスは、次の例に示すように、**ExtensionOf** 属性で指定されたコンポーネントを補強します。

    [ExtensionOf(classStr(MyClass))]
    final class MyClass_Extension
    {
        private void new()
        {
        }
    }

クラスはランタイム システムによってインスタンス化されるため、拡張クラスから派生する意味がありません。 したがって、拡張クラスは **final** としてマークする必要があります。 **classStr** コンパイル時関数は使用する必要があり、2 つの目的があります。

-   **MyClass** クラスが存在しない場合、コンパイル エラーを生成します。
-   どのような種類のコンポーネントが拡張されるかをコンパイラに知らせるために使用するコンパイル時関数。 コンポーネント名単独では、拡張するために指定されたコンポーネントを一意に識別しません。 たとえば、フォームはテーブル、クラス、および列挙として同じ名前を持つことができます。

任意の数の拡張クラスが、特定のモデル内で付与されたコンポーネントを強化することができます。 拡張子クラスは、ランタイム システムでのみプログラマが直接参照することはありません。

## <a name="extension-class-inheritance"></a>拡張子のクラス継承
拡張されたクラスから継承するクラスも、有効なクラスを継承します。 つまり、拡張機能を持つクラスから継承するクラスは、拡張クラスで定義されているメソッドを継承します。

## <a name="constructors"></a>コンストラクター
X++ はインスタンス コンストラクターおよび静的コンストラクターの両方をサポートしています。

### <a name="instance-constructors"></a>インスタンス コンストラクター

インスタンス コンストラクターは、**new** という名前のメソッドです。 拡張クラスで定義されているインスタンス コンストラクターはパラメーターを指定できません。 拡張クラスのインスタンスが作成され、ランタイム システムが使用シナリオで必要なコンストラクターを呼び出します。 これらのコンストラクターは、コードによって明示的に呼び出されることはありません。 コンストラクターは、拡張オブジェクトの状態を初期化するのに便利です。 拡張機能クラスのインスタンス メソッドまたはインスタンスの状態にアクセスする前に、拡張機能クラスに提示されているコンストラクターが 1 回呼び出されることが保証されます。 ただし、そのような参照が行われない場合、コンストラクタは呼び出されません。

### <a name="static-constructors"></a>静的コンストラクター

静的コンストラクターは、**typenew** と呼ばれるパラメーターなしの静的メソッドです。 静的コンストラクターは、拡張クラスで定義することができます。 ランタイム システムが拡張機能の種類を最初に参照する前にコンストラクターを呼び出すことが保証されます。 拡張子のセットの間での静的コンストラクションの呼び出しの特定の任意の順序を想定することはできません。

## <a name="methods"></a>メソッド
拡張クラスで定義されているパブリック メソッドは、拡張クラスが定義されているモデルのコンテキストで、拡張クラスに追加の機能を提供します。 この方法で、パブリック メソッドだけが公開されます。 パブリック メソッドの実装に役立てるためにプライベート メソッドを定義することができますが、これらのプライベート メソッドは有効なクラスの一部ではありません。 拡張クラスは最終的なものなので、メソッドを**保護された**ものとしてマークすることはできません。

### <a name="instance-methods"></a>インスタンス メソッド

次の例では、**ExtensionMethod** という名前の拡張メソッドを定義し、**MyClass** を補強します。

    [ExtensionOf(classStr(MyClass))]
    final class MyClass_Extension
    {
        private void new()
        {
        }
        public int ExtensionMethod(int arg)
        {
        }
    }

パブリック インスタンス メソッド (**ExtensionMethod**) は、拡張クラスで定義されます。 したがって、拡張クラスが定義されているモデルのコンテキストで **MyClass** で定義されているかのように使用できます。 次の例は、モデル内のメソッドを呼び出す方法を示しています。

    MyClass c = new MyClass();
    print c.ExtensionMethod(32);

拡張クラスで定義されているインスタンス メソッドは、強化されたコンポーネントのインスタンス メソッドとして使用されることに注意してください。 拡張メソッドは、それが補強するコンポーネントからのみパブリック メンバーにアクセスできます (プラットフォーム更新プログラム 9 またはそれ以降を使用している場合、保護されたメソッドおよびメンバーへのアクセスもサポートされています)。 この動作は仕様です。 コンポーネントは、**private**、または **internal** キーワードを通じて明示的に非表示にされる状態およびメソッドと直接やり取りできるようにする必要はありません。 それ以外の場合、明示的に非表示な状態とメソッドを直接操作すると、それらのコンポーネントの重要な実装の前提条件を無効にすることで障害が発生する可能性があります。 メソッドとメソッド本体のステートメントは、**this** キーワードを使用できます。 このコンテキストでは、**this** の型は強化されたコンポーネントの有効なクラスです。

### <a name="static-methods"></a>静的メソッド

拡張クラスでパブリックおよび静的として定義されているメソッドは、強化されているコンポーネントの静的メソッドとして使用できます。

    [ExtensionOf(classStr(MyClass))]
    final class MyClass_Extension
    {
        private void new()
        {
        }
        public int method1(int arg)
        {
        }
        public static real CelsiusToFahrenheit(real celsius)
        {
            return (celsius * 9.0 / 5.0) + 32.0;
        }
    }

次の例は、モデル内のメソッドを呼び出す方法を示しています。

    var temp = MyClass::CelsiusToFahrenheit(20.0);

静的メソッドは、パブリックの静的メソッドおよび強化されたコンポーネントの有効なクラスの状態にアクセスできます。 興味深い副作用として、**グローバル** クラスの静的拡張メソッドは接頭語なしで利用できる関数として言語で使用可能になります。

## <a name="state"></a>行政単位 (区画)
成果物に対する静的およびインスタンス メソッドを提供することに加えて、インスタンス状態と静的状態を追加できます。

### <a name="instance-state"></a>インスタンスの状態

コンポーネントの特定のインスタンスに関連する状態であるインスタンスの状態は、拡張クラスで指定できます。 次の例では、**state** という名前の状態を定義しています。

    [ExtensionOf(classStr(MyClass))]
    final class MyClass_Extension
    {
        public int state;
        private void new()
        {
        }
    }

次の例は、コード内で **state** を使用する方法を示しています。

    MyClass c = new MyClass();
    c.state = 12;

### <a name="static-state"></a>静的な状態

静的状態は、タイプのインスタンスではなくタイプに適用されます。 次の例は、静的な拡張状態を示しています。

    [ExtensionOf(classStr(MyClass))]
    final class MyClass_Extension
    {
        public int state;
        public static int staticState;
        static void TypeNew()
        {
            staticState = 77;
        }
    }



