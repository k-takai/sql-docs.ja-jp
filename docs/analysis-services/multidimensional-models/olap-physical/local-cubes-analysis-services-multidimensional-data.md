---
title: ローカル キューブ (Analysis Services - 多次元データ) |Microsoft ドキュメント
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 11c4a7b2917d7baa4860137fa0764026264024a8
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/10/2018
ms.locfileid: "34025749"
---
# <a name="local-cubes-analysis-services---multidimensional-data"></a>ローカル キューブ (Analysis Services - 多次元データ)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  ローカル キューブを作成、更新、または削除するには、ASSL スクリプトまたは AMO プログラムを作成して実行する必要があります。  
  
 ローカル キューブおよびローカル マイニング モデルは、クライアント ワークステーションがネットワークから切断されている間も分析が可能です。 たとえば、次の図のように、クライアント アプリケーションが OLE DB for OLAP 9.0 Provider (MSOLAP.3) を呼び出すと、このプロバイダーはローカル キューブ エンジンを読み込み、ローカル キューブを作成してクエリを実行します。  
  
 ![ローカル キューブとモデルのクライアント アーキテクチャ](../../../analysis-services/multidimensional-models/olap-physical/media/as-localcubearch9.gif "ローカル キューブとモデルのクライアント アーキテクチャ")  
  
 ADMOD.NET および分析管理オブジェクト (AMO) もまた、ローカル キューブとやり取りするときにローカル キューブ エンジンを読み込みます。 ローカル キューブ エンジンはローカル キューブと接続するときにローカル キューブ ファイルを排他的にロックするため、ローカル キューブ ファイルには同時に 1 つのプロセスしかアクセスできません。 1 つのプロセスにつき、5 つまでの同時接続が可能です。  
  
 .cub ファイルには、2 つ以上のキューブまたはデータ マイニング モデルが含まれる場合があります。 ローカル キューブおよびデータ マイニング モデルに対するクエリは、ローカル キューブ エンジンによって処理されるので、[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] インスタンスへの接続は必要ありません。  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] および [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] をローカル キューブの管理に使用することはできません。  
  
## <a name="local-cubes"></a>ローカル キューブ  
 ローカル キューブを作成し、いずれかの既存のキューブから取得されます、[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]インスタンスまたはリレーショナル データ ソース。  
  
|ローカル キューブ用データのソース|作成方法|  
|------------------------------------|---------------------|  
|サーバーベースのキューブ|CREATE GLOBAL CUBE ステートメントを使用することができます、または[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]スクリプト言語 (ASSL) スクリプトを作成し、サーバー ベースのキューブからキューブを入力します。 詳細については、次を参照してください。[グローバル キューブの作成ステートメント&#40;MDX&#41; ](../../../mdx/mdx-data-definition-create-global-cube.md)または[Analysis Services スクリプト言語&#40;の ASSL を XMLA&#41;](../../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)です。|  
|リレーショナル データ ソース|ASSL スクリプトを使用して、OLE DB リレーショナル データベースからキューブを作成して設定します。 ASSL を使用してローカル キューブを作成するには、ローカル キューブ ファイル (*.cub) に接続して、サーバー キューブを作成するときに [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] インスタンスで ASSL スクリプトを実行するのと同じ要領で ASSL スクリプトを実行するだけです。 詳細については、「[Analysis Services スクリプト言語 (XMLA 用 ASSL)](../../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)」を参照してください。|  
  
 ローカル キューブを再構築してデータを更新するには、REFRESH CUBE ステートメントを使用します。 詳細については、次を参照してください。 [CUBE ステートメントの更新 & #40 です。MDX と #41 です。](../../../mdx/mdx-data-definition-refresh-cube.md)  
  
### <a name="local-cubes-created-from-server-based-cubes"></a>サーバーベースのキューブから作成されたローカル キューブ  
 サーバーベースのキューブからローカル キューブを作成する場合は、次の点に注意してください。  
  
-   個別のカウント メジャーはサポートされていません。  
  
-   メジャーを追加する場合は、追加するメジャーに関連するディメンションも最低 1 つ追加する必要があります。 メジャー グループ ディメンションのリレーションシップの詳細については、次を参照してください。[ディメンション リレーションシップ](../../../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)です。  
  
-   親子階層を追加すると、親子階層のレベルやフィルターは無視されて、親子階層全体が追加されます。  
  
-   メンバー プロパティは作成されません。  
  
-   準加法メジャーを含める場合、Account ディメンションおよび Time ディメンションでのスライスは許可されていません。  
  
-   参照ディメンションは常に具体化されます。  
  
-   多対多ディメンションを含める場合は、次の規則が適用されます。  
  
    -   多対多ディメンションをスライスすることはできません。  
  
    -   中間メジャー グループのメジャーを追加する必要があります。  
  
    -   多対多リレーションシップに関係する 2 つのメジャー グループに共通するディメンションはスライスすることができません。  
  
-   ローカル キューブに追加されたメジャーおよびディメンションに依存する計算されるメンバー、名前付きセット、および割り当てだけがローカル キューブに表示されます。 無効な計算されるメンバー、名前付きセット、および割り当ては自動的に除外されます。  
  
### <a name="security"></a>セキュリティ  
 ユーザーがサーバー キューブからローカル キューブを作成するためには、ユーザーに許可する必要があります**ドリルスルーとローカル キューブ**サーバー キューブに対する権限。 詳細については、次を参照してください。[キューブまたはモデルのアクセス許可を与える&#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)です。  
  
 ローカル キューブは、サーバー キューブのようにロールを使用してセキュリティで保護されていません。 ローカル キューブ ファイルへのファイル レベルのアクセス権を持っていれば、ローカル キューブ ファイル内のキューブに対してクエリを実行できます。 使用することができます、**暗号化パスワード**接続ファイルのプロパティをローカル キューブに、ローカル キューブ ファイルにパスワードを設定します。 ローカル キューブ ファイルにパスワードを設定すると、以後クエリを実行するためにローカル キューブ ファイルに接続するときにそのパスワードが必要になります。  
  
## <a name="see-also"></a>参照  
 [CREATE GLOBAL CUBE ステートメント&#40;MDX&#41;](../../../mdx/mdx-data-definition-create-global-cube.md)   
 [Services スクリプト言語の分析の使用による開発&#40;ASSL&#41;](../../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [更新の CUBE ステートメント&#40;MDX&#41;](../../../mdx/mdx-data-definition-refresh-cube.md)  
  
  
