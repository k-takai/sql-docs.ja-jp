---
title: 通貨の種類ディメンションを作成 |Microsoft ドキュメント
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 73c44e299e448606ce37848ee8f58dd0e15aea76
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/10/2018
ms.locfileid: "34027089"
---
# <a name="database-dimensions---create-a-currency-type-dimension"></a>データベース ディメンション -、通貨ディメンションの種類を作成します。
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] では、通貨ディメンションとは、通貨を財務報告用に一覧にした属性を持つディメンションを指します。  
  
 通貨ディメンションによって、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のキューブに通貨換算機能を追加できます。 キューブに通貨換算を追加するには、ビジネス インテリジェンス ウィザードを使用して、クライアント アプリケーションのロケールに対応する値に通貨メジャーを変換する多次元式 (MDX) スクリプト コマンドを定義します。 この MDX スクリプトを作成するには、ビジネス インテリジェンス ウィザードで次の情報を指定する必要があります。  
  
-   現地通貨を表す通貨ディメンション (このディメンションが換算元通貨ディメンションになります)。  
  
-   使用する換算レートを表すメジャー グループ。  
  
 ビジネス インテリジェンス ウィザードは、これらの情報に基づいて、適切な換算先通貨ディメンション (換算先の通貨を表す通貨ディメンション) を指定する通貨換算プロセスをデザインします。 ビジネス インテリジェンス ウィザードでは、使用するビジネス インテリジェンス ソリューションに必要な通貨換算の数に応じて、複数の換算先通貨ディメンションを定義できます。 通貨換算の定義の詳細については、「[通貨換算 &#40;Analysis Services&#41;](../../analysis-services/currency-conversions-analysis-services.md)」を参照してください。  
  
 ディメンションを通貨ディメンションとして指定するには、ディメンションの **Type** プロパティを **Currency** に設定します。  
  
## <a name="dimension-structure"></a>[ディメンション構造]  
 通貨ディメンションには、少なくとも、その通貨ディメンションのディメンション テーブル内で個々の通貨を識別するキー属性が含まれています。 キー属性の値は、換算元通貨ディメンションと換算先通貨ディメンションで異なります。  
  
-   属性を換算元通貨ディメンションのキー属性として指定するには、属性の **Type** プロパティを **CurrencySource**に設定します。  
  
-   属性を換算先通貨ディメンションとして指定するには、属性の **Type** プロパティを **CurrencyDestination**に設定します。  
  
 必要に応じて次の属性を換算元通貨ディメンションと換算先通貨ディメンションに含めると、レポート作成に使用できます。  
  
-   通貨名を表す属性  
  
     属性を通貨名属性として指定するには、属性の **Type** プロパティを **CurrencyName**に設定します。  
  
-   換算元通貨を表す属性  
  
     属性を換算元通貨の属性として指定するには、属性の **Type** プロパティを **CurrencySource**に設定します。  
  
-   国際標準化機構 (ISO) 通貨コード  
  
     属性を ISO 通貨コード属性として指定するには、属性の **Type** プロパティを **CurrencyIsoCode**に設定します。  
  
 属性の種類の詳細については、「 [属性の種類の構成](../../analysis-services/multidimensional-models/attribute-properties-configure-attribute-types.md)」を参照してください。  
  
## <a name="defining-account-intelligence-with-the-business-intelligence-wizard"></a>ビジネス インテリジェンス ウィザードを使用した勘定科目インテリジェンスの定義  
 勘定科目ディメンションを定義し、定義したディメンションをキューブに追加したら、ビジネス インテリジェンス ウィザードを使用して、勘定科目の種類の特定とマップなどの勘定科目インテリジェンス機能をディメンションに追加することができます。 詳細については、「 [ディメンションへの勘定科目インテリジェンスの追加](../../analysis-services/multidimensional-models/bi-wizard-add-account-intelligence-to-a-dimension.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [属性と属性階層](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [ビジネス インテリジェンス ウィザードの F1 ヘルプ](http://msdn.microsoft.com/library/155ac80c-63ae-47aa-9e86-9396e3d920eb)   
 [ディメンションの種類](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)  
  
  
