---
title: "DataAggregation 要素 (ASSL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DataAggregation Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DataAggregation element
ms.assetid: baf6d2c9-54f6-4a6d-95f7-e1e758be458d
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 92556b6af8a3d56f647fcbea8b34e197fb8ce663
ms.contentlocale: ja-jp
ms.lasthandoff: 09/01/2017

---
# <a name="dataaggregation-element-assl"></a>DataAggregation 要素 (ASSL)
  インスタンスが永続化されたデータまたはのキャッシュされたデータを集計できるかどうかを判断、 [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)です。  
  
## <a name="syntax"></a>構文  
  
```xml  
  
<MeasureGroup>  
   ...  
   <DataAggregation>...</DataAggregation>  
   ...  
</MeasureGroup>  
```  
  
## <a name="element-characteristics"></a>要素の特性  
  
|特性|説明|  
|--------------------|-----------------|  
|データ型と長さ|String (列挙型)|  
|既定値|*DataAndCacheAggregatable*|  
|Cardinality|0-1 : 省略可能な要素で、出現する場合は 1 回だけの出現が可能です|  
  
## <a name="element-relationships"></a>要素の関係  
  
|リレーションシップ|要素|  
|------------------|-------------|  
|親要素|[メジャー グループ](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|  
|子要素|なし|  
  
## <a name="remarks"></a>解説  
 この要素の値は、次の表のいずれかの文字列に制限されます。  
  
|値|Description|  
|-----------|-----------------|  
|*なし*|このメジャー グループに対して集計は実行されません。|  
|*DataAggregatable*|このメジャー グループに対して持続データが集計されます。|  
|*CacheAggregatable*|このメジャー グループに対してキャッシュされたデータが集計されます。|  
|*DataAndCacheAggregatable*|このメジャー グループに対して、持続データとキャッシュされたデータの両方が集計されます。|  
  
 親に対応する要素**DataAggregation**分析管理オブジェクト (AMO) オブジェクト モデルは<xref:Microsoft.AnalysisServices.MeasureGroup>します。  
  
## <a name="see-also"></a>参照  
 [Cube 要素 & #40 です。ASSL &#41;](../../../analysis-services/scripting/objects/cube-element-assl.md)   
 [Dimension 要素 & #40 です。ASSL &#41;](../../../analysis-services/scripting/objects/dimension-element-assl.md)   
 [プロパティ & #40 です。ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  