---
title: "syscollector_config_store (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- syscollector_config_store_TSQL
- syscollector_config_store
dev_langs: TSQL
helpviewer_keywords:
- data collector view
- syscollector_config_store view
ms.assetid: f15f6b05-6808-4b76-b6a8-48dec844cf63
caps.latest.revision: "17"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: aabe9744ea3766dfeb8acc5707164f05c6419b1b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/17/2017
---
# <a name="syscollectorconfigstore-transact-sql"></a>syscollector_config_store (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  コレクション セットのインスタンスではなく、データ コレクター全体に適用されたプロパティを返します。 このビューの各行は、管理データ ウェアハウスの名前や、管理データ ウェアハウスが置かれているインスタンスの名前など、データ コレクターの特定のプロパティを表します。  
  
||  
|-|  
|**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] から [現在のバージョン](http://go.microsoft.com/fwlink/p/?LinkId=299658)まで)。|  
  
|列名|データ型|Description|  
|-----------------|---------------|-----------------|  
|parameter_name|**nvarchar (128)**|プロパティの名前。 NULL 値は許可されません。|  
|parameter_value|**sql_variant**|プロパティの実際の値。 NULL 値が許可されます。|  
  
## <a name="permissions"></a>Permissions  
 ビューの SELECT 権限、または dc_operator、dc_proxy、dc_admin のいずれかの固定データベース ロールのメンバーシップが必要です。  
  
## <a name="remarks"></a>解説  
 このビューで確認できるプロパティはあらかじめ決まっており、実際の値は適切なストアド プロシージャを使ってのみ変更できます。 次の表で、このビューを介して公開されるプロパティについて説明します。  
  
|プロパティ名|Description|  
|-------------------|-----------------|  
|CacheDirectory|コレクター型のパッケージが一時的な情報を格納するファイル システム内のディレクトリの名前です。<br /><br /> NULL = 既定の一時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ディレクトリを使用します。|  
|CacheWindow|データのアップロード時にエラーが発生した場合に使用される、キャッシュ ディレクトリのデータの保有ポリシーを示します。<br /><br /> -1 = アップロード エラーが発生した場合は常にデータを保持します。<br /><br /> 0 = アップロード エラーが発生した場合にデータを保持しません。<br /><br /> *n*= からデータを保持する *n* 以前のアップロード エラー場所 *n*  > = 1 です。<br /><br /> この値を変更するには、sp_syscollector_set_cache_window ストアド プロシージャを使用します。|  
|CollectorEnabled|データ コレクターの状態を示します。<br /><br /> 0 = 無効になっています<br /><br /> 1 = 有効になっています。<br /><br /> この値を変更するには、sp_syscollector_enable_collector ストアド プロシージャまたは sp_syscollector_disable_collector ストアド プロシージャを使用します。|  
|MDWDatabase|管理データ ウェアハウスの名前です。 この値を変更するには、sp_syscollector_set_warehouse_database_name ストアド プロシージャを使用します。|  
|MDWInstance|管理データ ウェアハウスが存在する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの名前です。 この値を変更するには、sp_syscollector_set_warehouse_instance_name ストアド プロシージャを使用します。|  
  
## <a name="examples"></a>使用例  
 次の例では、syscollector_config_store ビューのクエリを実行します。  
  
```tsql  
SELECT parameter_name, parameter_value  
FROM msdb.dbo.syscollector_config_store;  
```  
  
## <a name="see-also"></a>参照  
 [データ コレクター ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [データ コレクターのビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [[データ コレクション]](../../relational-databases/data-collection/data-collection.md)   
 [sp_syscollector_enable_collector &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql.md)   
 [sp_syscollector_disable_collector &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-disable-collector-transact-sql.md)   
 [sp_syscollector_set_warehouse_database_name &#40;です。TRANSACT-SQL と #41 です。](../../relational-databases/system-stored-procedures/sp-syscollector-set-warehouse-database-name-transact-sql.md)   
 [sp_syscollector_set_warehouse_instance_name &#40;です。TRANSACT-SQL と #41 です。](../../relational-databases/system-stored-procedures/sp-syscollector-set-warehouse-instance-name-transact-sql.md)   
 [sp_syscollector_set_cache_window &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-cache-window-transact-sql.md)  
  
  