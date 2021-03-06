---
title: マスター サーバーの作成 | Microsoft Docs
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
f1_keywords:
- sql13.ag.msxwiz.operator.f1
- sql13.ag.msxwiz.login.f1
- sql13.ag.msxwiz.target.f1
- sql13.ag.msxwiz.complete.f1
- sql13.ag.msxwiz.cover.f1
helpviewer_keywords:
- master servers [SQL Server], creating
- wizards [SQL Server Management Studio], Master Server Wizard
- SQL Server Agent jobs, master servers
- Master Server Wizard
ms.assetid: 05739a73-1fdf-4d9d-92a6-70f328380322
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 12fe6ba1182f5ad4cfa60176eba40a3de28971a3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
ms.locfileid: "33045879"
---
# <a name="make-a-master-server"></a>Make a Master Server
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database マネージ インスタンス](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database マネージ インスタンスと SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] を使用してマスター サーバー [!INCLUDE[tsql](../../includes/tsql_md.md)]を作成する方法について説明します。  
  
**このトピックの内容**  
  
-   **作業を開始する準備:**  
  
    [Security](#Security)  
  
-   **マスター サーバーを作成するために使用するもの:**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>はじめに  
  
### <a name="Security"></a>Security  
プロキシに関連付けられているステップを持つ分散ジョブは、対象サーバーのプロキシ アカウントのコンテキストで実行されます。 次の条件を満たしていることを確認してください。満たしていないと、プロキシに関連付けられているジョブ ステップがマスター サーバーから対象サーバーにダウンロードされません。  
  
-   マスター サーバー レジストリのサブキー **\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<&#42;instance_name&#42;>\SQL Server Agent\AllowDownloadedJobsToMatchProxyName** (REG_DWORD) が 1 (true) に設定されていること。 既定では、この値は 0 (false) に設定されます。  
  
-   ジョブ ステップを実行するマスター サーバー プロキシ アカウントと同じ名前を持つ対象サーバーにプロキシ アカウントが存在すること。  
  
マスター サーバーから対象サーバーにプロキシ アカウントをダウンロード中に、これらのアカウントを使用するジョブ ステップが失敗した場合は、 **msdb** データベースの **sysdownloadlist** テーブルの **error_message** 列を参照して、以下のエラー メッセージの有無を確認します。  
  
-   "ジョブ ステップではプロキシ アカウントが必要ですが、対象サーバーで一致するプロキシが無効です。"  
  
    このエラーを解決するには、 **AllowDownloadedJobsToMatchProxyName** レジストリ サブキーを 1 に設定します。  
  
-   "プロキシ アカウントが見つかりませんでした。"  
  
    このエラーを解決するには、対象サーバー上にプロキシ アカウントが存在し、ジョブ ステップを実行するマスター サーバー プロキシ アカウントと同じ名前が付けられているかどうかを確認します。  
  
#### <a name="Permissions"></a>Permissions  
このプロシージャの実行権限は、既定では **sysadmin** 固定サーバー ロールのメンバーに与えられています。  
  
## <a name="SSMSProcedure"></a>SQL Server Management Studio の使用  
  
#### <a name="to-make-a-master-server"></a>マスター サーバーを作成するには  
  
1.  **オブジェクト エクスプローラー** で、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[SQL Server エージェント]** を右クリックし、 **[マルチサーバーの管理]** をポイントして、 **[マスター サーバーに設定]** をクリックします。 **マスター サーバー ウィザード** を使用してマスター サーバーを作成し、対象サーバーを追加します。  
  
3.  **[マスター サーバー オペレーター]** ページで、マスター サーバーのオペレーターを設定します。電子メールまたはポケットベルを使用してオペレーターに通知を送信するには、電子メールが送信されるように [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] エージェントを設定しておく必要があります。 **net send**を使用してオペレーターに通知を送信するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] エージェントが置かれているサーバーで Messenger サービスが実行されている必要があります。  
  
    **[電子メール アドレス]**  
    オペレーターの電子メール アドレスを設定します。  
  
    **[ポケットベル アドレス]**  
    オペレーターのポケットベル メール アドレスを設定します。  
  
    **[Net Send アドレス]**  
    オペレーターの **net send** アドレスを設定します。  
  
4.  **[対象サーバー]** ページで、マスター サーバーの対象サーバーを選択します。  
  
    **[登録済みサーバー]**  
    Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] に登録されているサーバーで、まだ対象サーバーになっていないものを一覧表示します。  
  
    **[対象サーバー]**  
    対象サーバーであるサーバーを一覧表示します。  
  
    **>**  
    選択したサーバーを対象サーバーの一覧に移動します。  
  
    **>>**  
    すべてのサーバーを対象サーバーの一覧に移動します。  
  
    **<**  
    選択したサーバーを対象サーバーの一覧から削除します。  
  
    **<<**  
    すべてのサーバーを対象サーバーの一覧から削除します。  
  
    **[接続の追加]**  
    サーバーを登録せずに対象サーバーの一覧に追加します。  
  
    **[接続]**  
    選択したサーバーの接続プロパティを変更します。  
  
5.  **[マスター サーバー ログインの資格情報]** ページで、必要に応じて対象サーバーの新しいログインを作成してマスター サーバーへの権利を割り当てるかどうかを指定します。  
  
    **[必要に応じて新しいログインを作成し、MSX へのアクセス権を割り当てる]**  
    指定されたログインが存在していない場合に、新しいログインを対象サーバーに作成します。  
  
## <a name="TsqlProcedure"></a>Transact-SQL の使用  
  
#### <a name="to-make-a-master-server"></a>マスター サーバーを作成するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde_md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、現在のサーバーを AdventureWorks1 マスター サーバーに追加します。 現在のサーバーの場所は、Building 21 の Room 309 の Rack 5 です。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_msx_enlist N'AdventureWorks1',   
    N'Building 21, Room 309, Rack 5' ;   
GO;  
```  
  
詳細については、「 [sp_msx_enlist (Transact-SQL)](http://msdn.microsoft.com/en-us/ceb3b2bc-0cc4-48d8-9bdc-6a809556e35f)」を参照してください。  
  
## <a name="see-also"></a>参照  
[マルチサーバー環境の作成](../../ssms/agent/create-a-multiserver-environment.md)  
[エンタープライズ全体の管理の自動化](../../ssms/agent/automated-administration-across-an-enterprise.md)  
  
