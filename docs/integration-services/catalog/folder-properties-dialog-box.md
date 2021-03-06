---
title: '[フォルダーのプロパティ] ダイアログ ボックス | Microsoft Docs'
ms.custom: ''
ms.date: 08/26/2016
ms.prod: sql
ms.prod_service: integration-services
ms.component: service
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.ssis.ssms.isfolderprop.permissions.f1
- sql13.ssis.ssms.iscreatefolder.f1
- sql13.ssis.ssms.isfolderprop.general.f1
ms.assetid: d9a2bfae-fcc8-46be-b588-4a9db03f7e45
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7900eb74181b04de940793b2ae2d384a1a4e2e0c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="folder-properties-dialog-box"></a>[フォルダーのプロパティ] ダイアログ ボックス
  フォルダーには、 **SSISDB** カタログ内のプロジェクトおよび環境が含まれます。 フォルダーごとに、フォルダーの内容に適用される権限を定義します。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] の権限の詳細については、「[catalog.grant_permission &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-grant-permission-ssisdb-database.md)」をご覧ください。  
  
## <a name="to-set-folder-description-and-permissions"></a>フォルダーの説明と権限を設定するには  
  
1.  フォルダーを右クリックし、 **[プロパティ]** をクリックします。  
  
2.  **[全般]** ページで、 **[全般]** の下にある **[説明]** を選択して説明を入力します (省略可)。  
  
3.  **[権限]** ページで、 **[参照]** をクリックし、1 つ以上のデータベース プリンシパルを選択して **[OK]** をクリックします。  
  
4.  **[ログインまたはロール]** で名前を選択し、 **[権限]** で適切な権限を指定します。  
  
5.  **[OK]** をクリックして変更を受け入れ、 **[フォルダーのプロパティ]** ダイアログ ボックスを閉じます。  
  
## <a name="see-also"></a>参照  
 [Integration Services &#40;SSIS&#41; サーバー](../integration-services-ssis-packages.md)   
 [catalog.grant_permission &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-grant-permission-ssisdb-database.md)  
  
  
