---
title: Translation 要素 (XMLA) |Microsoft ドキュメント
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8b6c50664cdce599128be9f0ad15a10e33b77ec6
ms.sourcegitcommit: cfe5b2af733e7801558b441b4b9427cfe4c26435
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2018
ms.locfileid: "34576634"
---
# <a name="translation-element-xmla"></a>Translation 要素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  属性メンバーに対する翻訳を定義します。  
  
## <a name="syntax"></a>構文  
  
```xml  
  
<Translations>  
   ...  
   <Translation>  
      <Language>...</Language>  
      <Name>...</Name>  
   </Translation>  
   ...  
</Translations>  
```  
  
## <a name="element-characteristics"></a>要素の特性  
  
|特性|説明|  
|--------------------|-----------------|  
|データ型と長さ|なし|  
|既定値|なし|  
|Cardinality|0-n : 省略可能な要素で、出現する場合は複数回の出現が可能です|  
  
## <a name="element-relationships"></a>要素の関係  
  
|リレーションシップ|要素|  
|------------------|-------------|  
|親要素|[翻訳](../../../analysis-services/xmla/xml-elements-properties/translations-element-xmla.md)|  
|子要素|[言語](../../../analysis-services/xmla/xml-elements-properties/language-element-xmla.md)、[名](../../../analysis-services/xmla/xml-elements-properties/name-element-xmla.md)|  
  
## <a name="remarks"></a>コメント  
 A**翻訳**要素中に特定の属性に対して定義されている翻訳を属性メンバーを関連付けに必要な情報を定義する、[挿入](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)または[更新](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)コマンド。  
  
## <a name="see-also"></a>参照
 [プロパティ&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
