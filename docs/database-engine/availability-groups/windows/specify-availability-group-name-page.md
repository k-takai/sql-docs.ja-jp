---
title: '[可用性グループ オプションの指定] ページ (新しい可用性グループ ウィザード/データベース追加ウィザード) | Microsoft Docs'
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.newagwizard.specifyagname.f1
- sql13.swb.adddatabasewizard.specifyagname.f1
ms.assetid: dcb6374d-becb-4c6c-b88c-5a8273f8aa38
caps.latest.revision: 13
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1938b41ea4d23bc92e0c18a5a5ec7ccbcd2f8b8e
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/05/2018
ms.locfileid: "34771348"
---
# <a name="specify-availability-group-options-page"></a>[可用性グループ オプションの指定] ページ
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 **[可用性グループ名の指定]** ページのオプションについて説明します。 このトピックの対象は、 [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] の [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] と [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]の両方です。  
  
##  <a name="PageOptions"></a> 可用性グループ オプションの指定  
 **[可用性グループ名]**  
 可用性グループの名前を指定します。 新しい可用性グループには、Windows Server フェールオーバー クラスター (WSFC) のすべての可用性グループ内で一意の、有効な [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 識別子を指定してください。 可用性グループ名の最大文字数は 128 文字です。  

 **クラスター タイプ**: 次に、クラスター タイプを指定します。 使用できるクラスター タイプは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] バージョンとオペレーティング システムによって異なります。 次の一覧からいずれかを選択します。

   * **Windows Server フェールオーバー クラスタリング**
   
      可用性グループが、高可用性とディザスター リカバリーのために、Windows Server フェールオーバー クラスターに属する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスでホストされているときに使用します。 サポートされるすべてのバージョンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に適用されます。 

   * **EXTERNAL**
      
      可用性グループが、高可用性とディザスター リカバリーのために、Linux 上の Pacemaker などの外部クラスター テクノロジで管理されている [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスでホストされているときに使用します。 [!INCLUDE[sssqlv14](../../../includes/sssqlv14-md.md)] 以降に適用されます。

   * **NONE**
      
      可用性グループが、読み取りのスケールと負荷分散のために、クラスター テクノロジで管理されていない [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスでホストされているときに使用します。 [!INCLUDE[sssqlv14](../../../includes/sssqlv14-md.md)] 以降に適用されます。 
 
   **データベース レベルの正常性検出**: このボックスをオンにすると、可用性グループのデータベース レベルの正常性検出 (DB_FAILOVER) オプションが有効になります。 何らかの問題が発生し、データベースがオンライン状態でなくなると、このデータベース正常性検出によって検知され、可用性グループの自動フェールオーバーがトリガーされます。 [SQL Server の AlwaysOn データベースの正常性検出フェールオーバー オプション](sql-server-always-on-database-health-detection-failover-option.md)に関するページをご覧ください。


[データベースの選択] ページ (新しい可用性グループ ウィザードおよびデータベース追加ウィザード)  
  
##  <a name="LaunchWiz"></a> 関連タスク  
  
-   [[新しい可用性グループ] ダイアログ ボックスの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [可用性グループへのデータベース追加ウィザードの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md)  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
