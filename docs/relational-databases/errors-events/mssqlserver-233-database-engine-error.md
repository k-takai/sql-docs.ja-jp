---
title: MSSQLSERVER_233 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- "233"
helpviewer_keywords:
- 233 (Database Engine error)
ms.assetid: 201665dc-7ac8-4c19-90d3-33354c5caa72
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a029352dec1ac5a700b7ad5d048a9cb630347462
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver233"></a>MSSQLSERVER_233
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|233|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名||  
|メッセージ テキスト|サーバーとの接続は正常に確立されましたが、ログイン プロセスでエラーが発生しました。 (プロバイダー: 共有メモリ プロバイダー、エラー: 0 - パイプの他端にプロセスがありません。) (Microsoft SQL Server、エラー: 233)|  
  
## <a name="explanation"></a>説明  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クライアントがサーバーに接続できません。 このエラーは、サーバーがリモート接続を許可するように構成されていないことが原因で発生することがあります。  
  
## <a name="user-action"></a>ユーザーの操作  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャー ツールを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がリモート接続を許可できるようにします。  
  
## <a name="see-also"></a>参照  
[ネットワーク プロトコルとネットワーク ライブラリ](~/sql-server/install/network-protocols-and-network-libraries.md)  
[クライアント ネットワーク構成](~/database-engine/configure-windows/client-network-configuration.md)  
[クライアント プロトコルの構成](~/database-engine/configure-windows/configure-client-protocols.md)  
[サーバー ネットワーク プロトコルの有効化または無効化](~/database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  
