---
title: CDC インスタンスのプロパティを編集する方法 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: change-data-capture
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 7a6c719a-3735-43b7-b3ab-dfadd325eca2
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8a480e8353f501e7bd1ba7ff86df25e5ec736469
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-edit-the-cdc-instance-properties"></a>CDC インスタンスのプロパティを編集する方法
  この手順では、CDC デザイナー コンソールを使用して CDC インスタンスの構成プロパティを編集する方法について説明します。  
  
### <a name="to-edit-the-cdc-instance-configuration-properties"></a>CDC インスタンスの構成プロパティを編集するには  
  
1.  **[スタート]** メニューの **[CDC デザイナー コンソール]** をクリックします。  
  
2.  左側のペインで **[Change Data Capture]** を展開し、プロパティを編集するインスタンスが含まれているサービスを展開します。  
  
3.  プロパティを編集するインスタンスの名前を選択します。  
  
4.  CDC デザイナー コンソールの右側にある [アクション] ペインで **[プロパティ]** をクリックします。  
  
     プロパティを編集するインスタンスを右クリックして **[プロパティ]** をクリックすることもできます。  
  
5.  プロパティ エディターで、次のタブのプロパティを編集します。  
  
    -   **[Oracle]**: プロパティ エディターの **[Oracle]** タブを使用して、新しいインスタンス ウィザードの [CDC データベースの作成] ページで指定した説明を変更し、Oracle ログ マイニング データベースの接続情報を変更します。  
  
         このタブで編集できる内容の詳細については、「 [Edit the Oracle Database Properties](../../integration-services/change-data-capture/edit-the-oracle-database-properties.md)」を参照してください。  
  
    -   **[テーブル]**: Oracle ソース データベースから選択したテーブルおよび列を変更するには、 **[テーブル]** タブを使用します。  
  
         このタブで編集できる内容の詳細については、「 [Edit Tables](../../integration-services/change-data-capture/edit-tables.md)」を参照してください。  
  
    -   **[スクリプト]**: 補足ログを設定する Oracle ソース データベースでスクリプトを実行または再実行するには、 **[スクリプト]** タブを使用します。  
  
         このタブで実行できる内容の詳細については、「 [Review and Generate Supplemental Logging Scripts](../../integration-services/change-data-capture/review-and-generate-supplemental-logging-scripts.md)」を参照してください。  
  
    -   **[詳細設定]**: CDC インスタンスに特殊なプロパティを追加するには、 **[詳細設定]** タブを使用します。  
  
         このタブで実行できる内容の詳細については、「 [Edit the Advanced Properties](../../integration-services/change-data-capture/edit-the-advanced-properties.md)」を参照してください。  
  
  
