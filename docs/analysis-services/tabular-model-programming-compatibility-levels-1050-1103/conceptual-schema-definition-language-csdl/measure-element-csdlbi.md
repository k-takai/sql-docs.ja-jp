---
title: メジャー要素 (CSDLBI) |Microsoft ドキュメント
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 31bcb52bb9d1d0cf90b81ddc39ea838b00ece02f
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/10/2018
---
# <a name="measure-element-csdlbi"></a>Measure 要素 (CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Measure 要素は CSDL Property 要素に基づく複合型です。 CSDLBI 注釈によって、ビジネス インテリジェンス データ モデルで使用される複雑な式の定義をサポートする属性が追加されます。  
  
## <a name="elements-and-attributes"></a>要素と属性  
 次の表に、Measure 要素を定義する要素と属性、および Property 要素に適用される属性を示します。  
  
|名前|必須かどうか|Description|  
|----------|-----------------|-----------------|  
|Kpi|いいえ|KPI として使用されるメジャーに対してのみ必要な要素。 すべてのメジャーが KPI ではありませんが、すべての KPI はメジャーの定義に基づく必要があります。<br /><br /> [KPI 要素 & #40 です。CSDLBI & #41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/kpi-element-csdlbi.md)|  
|IsSimpleMeasure|いいえ|メジャーで使用される数式が単純な集計 (SUM、COUNT、MIN、MAX、AVG、DistinctCount) であるかどうかを示す true または false の値。<br /><br /> 既定値は trueです。|  
  
## <a name="example"></a>例  
 **表形式**  
  
 CSDLBI Version 1.1 における次の例では、AdventureWorks のテーブル モデル サンプルからの 2 つのメジャーを示します。 2 番目のメジャーは、KPI 要素を追加することで KPI に変換されています。  
  
```  
  
<Property   
    Name="Order_Lines_Count"   
    Type="Int64">  
<bi:Measure   
    Caption="Order Lines Count"   
    ReferenceName="Order Lines Count"   
    Width="0"   
    IsSimpleMeasure="false" />  
</Property>  
  
<Property   
    Name="Total_Current_Quarter_Sales_Performance"   
    Type="Double">  
<bi:Measure   
    Caption="Total Current Quarter Sales Performance"   
    ReferenceName="Total Current Quarter Sales Performance"   
    Width="0"   
    IsSimpleMeasure="false">  
    <bi:Kpi   
    StatusGraphic="Three Signs Colored">  
      <bi:KpiGoal>  
        <bi:PropertyRef Name="Measures___Total_Current_Quarter_Sales_Performance_Goal_" />  
      </bi:KpiGoal>  
      <bi:KpiStatus>  
        <bi:PropertyRef Name="Measures___Total_Current_Quarter_Sales_Performance_Status_" />  
      </bi:KpiStatus>  
    </bi:Kpi>  
  </bi:Measure>  
</Property>  
```  
  
## <a name="example"></a>例  
 **Multidimensiona です。**  
  
 CSDLBI Version 1.1 における次の例では、KPI として使用されている Contoso Operations キューブからのメジャーを示します。  
  
```  
  
<Property   
    Name="Sum_of_SalesAmount"   
    Type="Decimal" Precision="19" Scale="4">  
<Documentation>  
<Summary>KPI Description</Summary>  
</Documentation>  
<bi:Measure   
    Caption="Sum of SalesAmount"   
    ReferenceName="Sum of SalesAmount"   
    FormatString="\$#,0.00;(\$#,0.00);\$#,0.00">  
<bi:Kpi   
    StatusGraphic="Three Circles Colored">  
    <bi:KpiGoal>  
        <bi:PropertyRef Name="v_Sum_of_SalesAmount_Goal" />  
    </bi:KpiGoal>  
    <bi:KpiStatus>  
        <bi:PropertyRef Name="v_Sum_of_SalesAmount_Status" />  
    </bi:KpiStatus>  
</bi:Kpi>  
</bi:Measure>  
</Property>  
```  
  
## <a name="see-also"></a>参照  
 [CSDL への BI 注釈のテクニカル リファレンス](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)  
  
  
