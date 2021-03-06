---
title: 四角形と線 (レポート ビルダーおよび SSRS) | Microsoft Docs
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
ms.assetid: d6226b0c-0398-4185-8565-96099876fc21
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 05fb8fc7b21ce2274c113582f7bf3f1cb1c61e4a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="rectangles-and-lines-report-builder-and-ssrs"></a>四角形と線 (レポート ビルダーおよび SSRS)
  四角形と線は、 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] のページ分割されたレポートに視覚効果を与えることができます。 [ホーム] タブの [罫線] セクションでこれらのレポート アイテムの表示プロパティを設定し、プロパティ ペインでその他のプロパティを設定できます。 背景色、背景画像、ツールヒント、ブックマークなどの機能を、四角形に追加できます。  
  
##  <a name="RectanglesLinesReportParts"></a> レポート パーツとしての四角形と線  
 四角形はその中にあるアイテムと共に、レポート パーツとしてレポートとは別にパブリッシュできます。 レポート パーツは、他のレポートに含めることができる、レポート サーバー上に格納された自己完結型のレポート アイテムです。  
  
 四角形内のレポート アイテムをレポート パーツとしてパブリッシュすることはできません。 レポートに四角形を追加すると、その四角形と内部のアイテムを取得できます。  [レポート パーツ](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)の詳細を参照してください。  
  
##  <a name="RectangleAsContainer"></a> コンテナーとしての四角形の使用  
 四角形は、他のアイテムのコンテナーとして使用できます。 四角形を移動すると、四角形の中にあるアイテムも合わせて移動します。 四角形の中にあるアイテムの **Parent** プロパティには、四角形の名前が表示されます。 四角形をコンテナーとして使用する方法については、「[四角形またはコンテナーの追加 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/add-a-rectangle-or-container-report-builder-and-ssrs.md)」および「[マトリックスとグラフでの同じデータの表示 &#40;レポート ビルダー&#41;](../../reporting-services/report-design/display-the-same-data-on-a-matrix-and-a-chart-report-builder.md)」を参照してください。  
  
> [!NOTE]  
>  四角形はアイテムの単なるコンテナーで、アイテムを四角形内で作成するか四角形にドラッグします。 デザイン画面に既に存在するアイテムの周囲に四角形を描画した場合、四角形はコンテナーとして機能しません。 この四角形はアイテムの Parent プロパティに表示されません。  
  
 四角形をレポート アイテムの格納に使用する場合は、レポートの表示中にアイテムが全体としてどのような影響を受けるかを考慮してください。 繰り返されるデータ行を含むレポート アイテム (たとえばテーブル) は、クエリから返されたデータに合わせて展開されるので、四角形内の他のアイテムの位置に影響を与えます。 アイテムがテーブルのデータ領域よりも下に配置されると、このテーブルによりアイテムは押し下げられます。 同じ位置にアイテムを配置するには、テーブルの下枠より上に上の枠が来るように配置された四角形の内部にレポート アイテムを配置します。 詳しくは、「[レンダリングの動作 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)」をご覧ください。  
  
##  <a name="ReportBorder"></a> レポートの罫線の追加  
 線や四角形を追加せずに、ヘッダー、フッター、およびレポート本文自体に罫線を追加することで、レポートに罫線を追加できます。 詳細については、「 [レポートへの罫線の追加 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/add-a-border-to-a-report-report-builder-and-ssrs.md)の詳細を参照してください。  
  
##  <a name="HowTo"></a> 操作方法に関するトピック  
 [レポートへの罫線の追加 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/add-a-border-to-a-report-report-builder-and-ssrs.md)  
  
 [四角形またはコンテナーの追加 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/add-a-rectangle-or-container-report-builder-and-ssrs.md)  
  
 [罫線の追加および変更 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/add-and-modify-a-line-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>参照  
 [四角形またはコンテナーの追加 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/add-a-rectangle-or-container-report-builder-and-ssrs.md)  
  
  
