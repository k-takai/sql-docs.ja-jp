---
title: 階段状レポートの作成 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5933c4f0-c713-4ecb-b521-ff46c9c63fff
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7644c7d01ea8d12864cf402543f031f137aed383
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
ms.locfileid: "33021819"
---
# <a name="create-a-stepped-report-report-builder-and-ssrs"></a>階段状レポートの作成 (レポート ビルダーおよび SSRS)
階段状レポートは  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の改ページ調整されたレポートで、次の例に示すように、親グループとその下でインデントされた詳細行または子グループが、同じ列内に表示されます。  
  
 ![レンダリングされた階段状レポート](../../reporting-services/report-design/media/steppedreportrendered.gif "レンダリングされた階段状レポート")  
  
 従来の表形式のレポートでは、親グループがレポート上の隣接する列に配置されます。 新しい Tablix データ領域を使用すると、グループと、詳細行または子グループを同じ列に追加することができます。 グループ行を詳細行または子グループ行と区別するには、フォントの色などの書式設定を適用するか、詳細行にインデントを設定します。  
  
 このトピックの手順では、手動で階段状レポートを作成する方法を示しますが、新しいテーブル/マトリックス ウィザードを使用することもできます。 このウィザードには、階段状レポートのレイアウトが用意されているため、このようなレポートを簡単に作成できます。 ウィザードを完了した後、レポートをさらに拡張できます。  
  
> [!NOTE]  
>  ウィザードは、レポート ビルダーでのみ利用可能です。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-create-a-stepped-report"></a>階段状レポートを作成するには  
  
1.  テーブル レポートを作成します。 たとえば、Tablix データ領域を挿入し、データ行にフィールドを追加します。  
  
2.  レポートに親グループを追加します。  
  
    1.  テーブル内の任意の場所をクリックして選択します。 グループ化ペインに、行グループ ペインのグループの詳細が表示されます。  
  
    2.  グループ化ペインで、グループの詳細を右クリックし、 **[グループの追加]** をポイントして **[親グループ]** をクリックします。  
  
    3.  **[Tablix のグループ]** ダイアログ ボックスで、グループの名前を指定し、グループ式を入力するかドロップダウン リストから選択します。 ボックスの一覧には、レポート データ ペインで使用できる簡単なフィールド式が表示されます。 たとえば、[PostalCode] は、データセット内の PostalCode フィールドの簡単なフィールド式です。  
  
    4.  **[グループ ヘッダーの追加]** を選択します。 このオプションを選択すると、グループの上部にグループ ラベルおよびグループ合計の静的行が追加されます。 同様に、 **[グループ フッターの追加]** を選択して、グループの下に静的行を追加できます。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     これで、基本的なテーブル レポートが作成されました。 レポートが表示されると、1 つの列にグループ インスタンス値、1 つ以上の列にグループ化された詳細データが含まれています。 デザイン画面でのデータ領域の外観は次の図のようになります。  
  
     ![グループを含むテーブル データ領域](../../reporting-services/report-design/media/tabledataregionwithgroup.gif "グループを含むテーブル データ領域")  
  
     レポートを表示したときの表示データ領域の外観は次の図のようになります。  
  
     ![レンダリングされたグループ化レポート](../../reporting-services/report-design/media/tablereportrendered.gif "レンダリングされたグループ化レポート")  
  
3.  段階状レポートを作成する場合、最初の列にグループ インスタンスを表示する必要はありません。 その代わり、グループ ヘッダー セル内の値をコピーし、グループ列を削除し、グループ ヘッダー行内の最初のテキスト ボックスに貼り付けます。 グループ列を削除するには、グループ列またはセルを右クリックして、 **[列の削除]** をクリックします。 デザイン画面でのデータ領域の外観は次の図のようになります。  
  
     ![グループ ヘッダー行のあるデータ領域](../../reporting-services/report-design/media/tabledataregiongroupheader.gif "グループ ヘッダー行のあるデータ領域")  
  
4.  グループ ヘッダー行の下で、同じ列にある詳細行にインデントを設定するには、詳細データ セルの余白を変更します。  
  
    1.  インデントを設定する詳細フィールドが含まれているセルを選択します。 そのセルのテキスト ボックス プロパティがプロパティ ペインに表示されます。  
  
    2.  プロパティ ペインの **[配置]** で、 **[余白]** のプロパティを展開します。  
  
    3.  **[左]** に、新しい余白の値 ( **.5in**など) を入力します。 指定された値の余白分、セル内のテキストがインデント設定されます。 余白の既定値は 2 ポイントです。 余白のプロパティの有効な値として、0 (ゼロ) 以上の正の数の後に、サイズ指定子を入力します。  
  
         サイズ指定子は次のとおりです。  
  
        |||  
        |-|-|  
        |**in**|インチ (1 インチ = 2.54 cm)|  
        |**cm**|センチメートル|  
        |**mm**|ミリメートル|  
        |**pt**|ポイント (1 ポイント = 1/72 インチ)|  
        |**pc**|パイカ (1 パイカ = 12 ポイント)|  
  
     データ領域は次の例にようになります。  
  
     ![階段状レポートのデータ領域](../../reporting-services/report-design/media/steppedreportdataregion.gif "階段状レポートのデータ領域")  
  
     **段階状レポート レイアウトのデータ領域**  
  
     **[ホーム]** タブで **[実行]** をクリックします。 レポートに、子グループ値がインデント設定されたグループが表示されます。  
  
## <a name="to-create-a-stepped-report-with-multiple-groups"></a>複数のグループを含む階段状レポートを作成するには  
  
1.  前の手順の説明に従ってレポートを作成します。  
  
2.  追加のグループをレポートに追加します。  
  
    1.  行グループ ペインで、グループを右クリックし、 **[グループの追加]** をクリックして、追加するグループの種類を選択します。  
  
        > [!NOTE]  
        >  データ領域にグループを追加するには、いくつかの方法があります。 詳細については、「 [データ領域でのグループの追加または削除 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)」を参照してください。  
  
    2.  **[Tablix のグループ]** ダイアログ ボックスで、名前を入力します。  
  
    3.  **[グループ式]** で、式を入力するか、グループ化の対象となるデータセット フィールドを選択します。 式を作成するには、式 (**[fx]**) ボタンをクリックして **[式]** ダイアログ ボックスを開きます。  
  
    4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
3.  グループ データを表示するセルの埋め込みを変更します。  
  
## <a name="see-also"></a>参照  
 [ページ ヘッダーとページ フッター &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md)   
 [レポート アイテムの書式設定 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/formatting-report-items-report-builder-and-ssrs.md)   
 [Tablix データ領域 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [テーブル &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [マトリックス &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [一覧 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [テーブル、マトリックス、および一覧 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
