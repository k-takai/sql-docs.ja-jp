---
title: OnlineMode 要素 (ASSL) |Microsoft ドキュメント
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: e02252c66333e6d75bb72871105604f35cd688c5
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/10/2018
ms.locfileid: "34038826"
---
# <a name="onlinemode-element-assl"></a>OnlineMode 要素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  キャッシュの再構築の開始時に直ちにデータベースをオンラインに戻すか、キャッシュの再構築の完了時にのみデータベースをオンラインに戻すかを指定します。  
  
## <a name="syntax"></a>構文  
  
```xml  
  
<ProactiveCaching>  
   ...  
   <OnlineMode>...</OnlineMode>  
   ...  
</ProactiveCaching>  
```  
  
## <a name="element-characteristics"></a>要素の特性  
  
|特性|説明|  
|--------------------|-----------------|  
|データ型と長さ|String (列挙型)|  
|既定値|*イミディ エイト*|  
|Cardinality|0-1 : 省略可能な要素で、出現する場合は 1 回だけの出現が可能です|  
  
## <a name="element-relationships"></a>要素の関係  
  
|リレーションシップ|要素|  
|------------------|-------------|  
|親要素|[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)|  
|子要素|なし|  
  
## <a name="remarks"></a>解説  
 この要素の値は、次の表の一覧に示す文字列のいずれかに限定されています。  
  
|値|Description|  
|-----------|-----------------|  
|*イミディ エイト*|データベースは、キャッシュの再構築の開始時に直ちにオンラインに戻ります。|  
|*OnCacheComplete*|データベースは、キャッシュの再構築の完了時にのみオンラインに戻ります。|  
  
 許可される値に対応する列挙**OnlineMode**分析管理オブジェクト (AMO) オブジェクト モデルは<xref:Microsoft.AnalysisServices.ProactiveCaching>します。  
  
## <a name="see-also"></a>参照  
 [ProactiveCaching 要素&#40;ASSL&#41;](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)  
  
  
