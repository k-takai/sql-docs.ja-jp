---
title: IsTestCase (DMX) |Microsoft ドキュメント
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: eefb9269a3eb0dc7a6b95e84accb4c68c6737a13
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2018
ms.locfileid: "34841795"
---
# <a name="istestcase-dmx"></a>IsTestCase (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  ケースが、指定されたデータ マイニング モデルまたはマイニング構造のテスト ケースとして使用されるかどうかを示します。  
  
## <a name="syntax"></a>構文  
  
```  
  
IsTestCase()  
```  
  
## <a name="result-type"></a>結果の種類  
 返します**true**ケースがテスト データ セットの一部である場合それ以外の場合**false**です。  
  
## <a name="remarks"></a>コメント  
 データ マイニング ウィザードを使用してマイニング構造および関連マイニング モデルを作成する場合、既定では全ケースの 30% がテスト データセットの使用のために確保されます。 残りのケースは、データ マイニング モデルのトレーニングに使用されます。 その構造に基づくすべてのモデルで同じテスト データセットを使用できます。 ただし、DMX を使用してマイニング モデルを作成する場合は、既定ですべてのデータがモデルのトレーニングに使用され、テスト セットは作成されません。 テスト データ セットの作成を有効にするには、WITH HOLDOUT 句のパラメーターを設定する必要があります。  
  
 <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxCases%2A> プロパティと <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxPercent%2A> プロパティの値を表示すると、特定のマイニング構造にテスト セットが作成されたかどうかを確認できます。  
  
> [!NOTE]  
>  IsTrainingCase または IsTestCase 関数を使用して、特定のモデルでケースに関する詳細を返す場合、モデルでドリルスルーを有効にする必要があります。 詳細については、「 [Enable Drillthrough for a Mining Model](../analysis-services/data-mining/enable-drillthrough-for-a-mining-model.md)」(マイニング モデルのドリルスルーの有効化) を参照してください。  
  
 トレーニング データ セットの一部であるケースを返すには、関数を使用[IsTrainingCase &#40;DMX&#41;](../dmx/istrainingcase-dmx.md)です。  
  
## <a name="examples"></a>使用例  
 次の例では、`Targeted Mailing`で作成されるマイニング構造、[基本的なデータ マイニング チュートリアル」](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)です。 このクエリでは、テストに使用される構造内のすべてのケースが返されます。  
  
```  
SELECT *  
FROM [Targeted Mailing].CASES  
WHERE IsTestCase()  
```  
  
 データ マイニングで使用されるケースをクエリする方法の詳細については、次を参照してください。 [SELECT FROM&#60;モデル&#62;です。ケース&#40;DMX&#41; ](../dmx/select-from-model-cases-dmx.md)と[SELECT FROM&#60;構造&#62;です。ケース](../dmx/select-from-structure-cases.md)です。  
  
## <a name="see-also"></a>参照  
 [関数&#40;DMX&#41;](../dmx/functions-dmx.md)   
 [データ マイニング クエリ](../analysis-services/data-mining/data-mining-queries.md)   
 [トレーニング データ セットとテスト データ セット](../analysis-services/data-mining/training-and-testing-data-sets.md)  
  
  
