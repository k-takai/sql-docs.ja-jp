---
title: マルチサーバー環境に適したエージェント サービス アカウントの選択 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, service accounts
- multiserver environments [SQL Server], SQL Server Agent service account behavior
ms.assetid: a07e2f38-281c-495b-965b-13fad03ba548
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e54c787b2b335c46e94dba310f1a5507b566f0b6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
ms.locfileid: "33038969"
---
# <a name="choose-the-right-sql-server-agent-service-account-for-multiserver-environments"></a>マルチサーバー環境に適した SQL Server エージェント サービス アカウントの選択
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database マネージ インスタンス](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database マネージ インスタンスと SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] エージェント サービスに対して選択する Windows アカウントによって、マルチサーバー環境の動作に次のような影響が生じることがあります。  
  
-   ローカルの Windows Administrators グループのメンバーではないアカウントで [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] エージェント サービスを実行する場合、マスター サーバーへの対象サーバーの参加は、失敗する可能性があります。 その場合は、次のエラー メッセージが返されます。  
  
    "参加操作に失敗しました"  
  
    この問題を解決するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] サービスおよび [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] エージェント サービスを再起動します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] エージェント サービスがローカル システム アカウントで実行されるとき、マスター サーバーと対象サーバー間の操作は、同じコンピューターにマスター サーバーと対象サーバーの両方が存在する場合にのみサポートされます。 この構成を使用している場合に、対象サーバーをマスター サーバーに参加させると、次のメッセージが返されます。  
  
    "*<target_server_computer_name>* のエージェント開始アカウントに対象サーバーとしてのログオン権限があることを確認します"  
  
    情報提供を目的としたこのメッセージは無視できます。 参加操作は、正常に完了します。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] エージェント サービスのアカウントの選択の詳細については、「 [SQL Server エージェント サービスのアカウントの選択](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md)」を参照してください。  
  
