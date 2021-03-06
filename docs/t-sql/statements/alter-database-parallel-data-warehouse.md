---
title: ALTER DATABASE (並列データ ウェアハウス) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: pdw
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5751656b-7aae-4152-a314-4c631bea4fc4
caps.latest.revision: 10
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b17fcc15be4c8faf496c469bb1e46fe2c6d42012
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2018
ms.locfileid: "34550493"
---
# <a name="alter-database-parallel-data-warehouse"></a>ALTER DATABASE (並列データ ウェアハウス)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] の複製テーブル、分散テーブル、トランザクション ログの最大データベース サイズ オプションを変更します。 このステートメントを使用すると、サイズの増加または減少に合わせてデータベースのディスク領域割り当てを管理できます。 また、この記事では Parallel Data Warehouse のデータベース オプションの設定に関連する構文についても説明します。 
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
-- Parallel Data Warehouse  
ALTER DATABASE database_name    
    SET ( <set_database_options>   | <db_encryption_option> )  
[;]  
  
<set_database_options> ::=   
{  
    AUTOGROW = { ON | OFF }  
    | REPLICATED_SIZE = size [GB]  
    | DISTRIBUTED_SIZE = size [GB]  
    | LOG_SIZE = size [GB]
    | SET AUTO_CREATE_STATISTICS { ON | OFF }
    | SET AUTO_UPDATE_STATISTICS { ON | OFF } 
    | SET AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF }
}  
  
<db_encryption_option> ::=  
    ENCRYPTION { ON | OFF }  
```  
  
## <a name="arguments"></a>引数  
 *database_name*  
 変更するデータベースの名前。 アプライアンスでデータベースの一覧を表示するには、[sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) を使用します。  
  
 AUTOGROW = { ON | OFF }  
 AUTOGROW オプションを更新します。 AUTOGROW が ON のとき、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] は、複製テーブル、分散テーブル、トランザクション ログの割り当て領域を必要に応じて自動的に増やし、記憶域要件の増加に対応します。 AUTOGROW が OFF のとき、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] は、複製テーブル、分散テーブル、トランザクション ログが最大サイズ設定を超過したときにエラーを返します。  
  
 REPLICATED_SIZE = *size* [GB]  
 変更されているデータベースのすべての複製テーブルを格納するための新しい最大 GB を計算ノードごとに指定します。 アプライアンスの記憶域を計画している場合、アプライアンスの計算ノード数に REPLICATED_SIZE を掛ける必要があります。  
  
 DISTRIBUTED_SIZE = *size* [GB]  
 変更されているデータベースのすべての分散テーブルを格納するための新しい最大 GB をデータベースごとに指定します。 このサイズは、アプライアンスの計算ノード全体で分散されます。  
  
 LOG_SIZE = *size* [GB]  
 変更されているデータベースのすべてのトランザクション ログを格納するための新しい最大 GB をデータベースごとに指定します。 このサイズは、アプライアンスの計算ノード全体で分散されます。  
  
 ENCRYPTION { ON | OFF }  
 データベースを暗号化する (ON) か、暗号化しない (OFF) かを設定します。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] の暗号化は、[sp_pdw_database_encryption](http://msdn.microsoft.com/5011bb7b-1793-4b2b-bd9c-d4a8c8626b6e) が **1** に設定されているときにのみ構成できます。 Transparent Data Encryption を構成するには、先にデータベース暗号化キーを作成する必要があります。 データベース暗号化の詳細については、「[Transparent Data Encryption &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)」を参照してください。  

 SET AUTO_CREATE_STATISTICS { ON | OFF } 統計の自動作成オプション AUTO_CREATE_STATISTICS がオンの場合、クエリ プランのカーディナリティの推定を向上させるために、クエリ オプティマイザーによってクエリ述語内の個々の列に関する統計が必要に応じて作成されます。 これらの 1 列ずつの統計は、既存の統計オブジェクトにまだヒストグラムがない列について作成されます。

 AU7 へのアップグレード後に作成された新しいデータベースの場合、既定値は ON です。 アップグレードの前に作成されたデータベースの場合、既定値は OFF です。 

 統計の詳細については、「[統計](/sql/relational-databases/statistics/statistics)」を参照してください。

 SET AUTO_UPDATE_STATISTICS { ON | OFF } 統計の自動更新オプション AUTO_UPDATE_STATISTICS がオンの場合、古くなっている可能性がある統計がクエリ オプティマイザーによって判断され、それらがクエリで使用されると更新されます。 挿入、更新、削除、またはマージの各操作によってテーブルまたはインデックス付きビューのデータの分布が変わると、統計は古くなったと判断されます。 クエリ オプティマイザーでは、統計が前回更新されてから発生したデータ変更の数をカウントし、その変更の数をしきい値と比較することで、統計が古くなっている可能性がないかを判断します。 このしきい値は、テーブルまたはインデックス付きビューの行数に基づいて決められます。

 AU7 へのアップグレード後に作成された新しいデータベースの場合、既定値は ON です。 アップグレードの前に作成されたデータベースの場合、既定値は OFF です。 

 統計の詳細については、「[統計](/sql/relational-databases/statistics/statistics)」を参照してください。


 SET AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF } 統計の非同期更新オプション AUTO_UPDATE_STATISTICS_ASYNC によって、クエリ オプティマイザーで統計の同期更新と非同期更新のどちらを使用するかが決まります。 AUTO_UPDATE_STATISTICS_ASYNC オプションは、インデックスに対して作成された統計オブジェクト、クエリ述語内の列に対して 1 列ずつ作成された統計オブジェクト、および CREATE STATISTICS ステートメントを使用して作成された統計に適用されます。

 AU7 へのアップグレード後に作成された新しいデータベースの場合、既定値は ON です。 アップグレードの前に作成されたデータベースの場合、既定値は OFF です。 

 統計の詳細については、「[統計](/sql/relational-databases/statistics/statistics)」を参照してください。

  
## <a name="permissions"></a>アクセス許可  
 データベースに対する ALTER 権限が必要です。  
  
## <a name="error-messages"></a>エラー メッセージ
自動統計が無効になっている場合に、統計の設定を変更しようとすると、"このオプションは PDW でサポートされていません" というエラーが PDW から返されます。 システム管理者は、機能スイッチ [AutoStatsEnabled](../../analytics-platform-system/appliance-feature-switch.md) を有効にすることにより、自動統計を有効にすることができます。

## <a name="general-remarks"></a>全般的な解説  
 REPLICATED_SIZE、DISTRIBUTED_SIZE、LOG_SIZE は、データベースの現在の値と同じ値か、それより大きい値か、それより小さい値に設定できます。  
  
## <a name="limitations-and-restrictions"></a>制限事項と制約事項  
 増加と縮小はおおよそで行われます。 結果的に与えられる実際のサイズはサイズ パラメーターとは異なる場合があります。  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] は ALTER DATABASE ステートメントを不可分操作として実行しません。 実行中、ステートメントが中止された場合、既に発生している変更はそのまま残ります。  

統計の設定は、管理者によって自動統計が有効にされた場合にのみ機能します。管理者である場合は、機能スイッチ [AutoStatsEnabled](../../analytics-platform-system/appliance-feature-switch.md) を使用して自動統計を有効または無効にします。 
  
## <a name="locking-behavior"></a>ロック動作  
 DATABASE オブジェクトを共有ロックします。 別のユーザーが読み取りまたは書き込みをしているデータベースを変更することはできません。 データベースで [USE](http://msdn.microsoft.com/158ec56b-b822-410f-a7c4-1a196d4f0e15) ステートメントを発行しているセッションもこれに該当します。  
  
## <a name="performance"></a>[パフォーマンス]  
 データベース内の実際のデータ サイズとディスクの断片化の量によっては、データベースの縮小に多大な時間とシステム リソースが必要となります。 たとえば、データベースを縮小に数時間かかることがあります。  
  
## <a name="determining-encryption-progress"></a>暗号化の進捗状況を見る  
 次のクエリを使用すると、データベースの Transparent Data Encryption の進捗状況を割合で見ることができます。  
  
```  
WITH  
database_dek AS (  
    SELECT ISNULL(db_map.database_id, dek.database_id) AS database_id,  
        dek.encryption_state, dek.percent_complete,  
        dek.key_algorithm, dek.key_length, dek.encryptor_thumbprint,  
        type  
    FROM sys.dm_pdw_nodes_database_encryption_keys AS dek  
    INNER JOIN sys.pdw_nodes_pdw_physical_databases AS node_db_map  
        ON dek.database_id = node_db_map.database_id   
        AND dek.pdw_node_id = node_db_map.pdw_node_id  
    LEFT JOIN sys.pdw_database_mappings AS db_map  
        ON node_db_map .physical_name = db_map.physical_name  
    INNER JOIN sys.dm_pdw_nodes nodes  
        ON nodes.pdw_node_id = dek.pdw_node_id  
    WHERE dek.encryptor_thumbprint <> 0x  
),  
dek_percent_complete AS (  
    SELECT database_dek.database_id, AVG(database_dek.percent_complete) AS percent_complete  
    FROM database_dek  
    WHERE type = 'COMPUTE'  
    GROUP BY database_dek.database_id  
)  
SELECT DB_NAME( database_dek.database_id ) AS name,  
    database_dek.database_id,  
    ISNULL(  
       (SELECT TOP 1 dek_encryption_state.encryption_state  
        FROM database_dek AS dek_encryption_state  
        WHERE dek_encryption_state.database_id = database_dek.database_id  
        ORDER BY (CASE encryption_state  
            WHEN 3 THEN -1  
            ELSE encryption_state  
            END) DESC), 0)  
        AS encryption_state,  
dek_percent_complete.percent_complete,  
database_dek.key_algorithm, database_dek.key_length, database_dek.encryptor_thumbprint  
FROM database_dek  
INNER JOIN dek_percent_complete   
    ON dek_percent_complete.database_id = database_dek.database_id  
WHERE type = 'CONTROL';  
```  
  
 TDE 実装の全手順を包括的な例で見るには、「[Transparent Data Encryption &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)」を参照してください。  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-altering-the-autogrow-setting"></a>A. AUTOGROW 設定を変更する  
 データベース `CustomerSales` の AUTOGROW を ON に設定します。  
  
```  
ALTER DATABASE CustomerSales  
    SET ( AUTOGROW = ON );  
```  
  
### <a name="b-altering-the-maximum-storage-for-replicated-tables"></a>B. 複製テーブルの最大記憶域を変更する  
 次の例では、データベース `CustomerSales` の複製テーブルの記憶域上限を 1 GB に設定します。 これは計算ノードごとの記憶域上限になります。  
  
```  
ALTER DATABASE CustomerSales  
    SET ( REPLICATED_SIZE = 1 GB );  
```  
  
### <a name="c-altering-the-maximum-storage-for-distributed-tables"></a>C. 分散テーブルの最大記憶域を変更する  
 次の例では、データベース `CustomerSales` の分散テーブルの記憶域上限を 1000 GB (1 テラバイト) に設定します。 これは、計算ノードごとの記憶域上限ではなく、アプライアンス全体の全計算ノードの記憶域上限を 1 つにしたものになります。  
  
```  
ALTER DATABASE CustomerSales  
    SET ( DISTRIBUTED_SIZE = 1000 GB );  
```  
  
### <a name="d-altering-the-maximum-storage-for-the-transaction-log"></a>D. トランザクション ログの最大記憶域を変更する  
 次の例では、データベース `CustomerSales` を更新し、アプライアンスの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] トランザクション ログの最大サイズを 10 GB にします。  
  
```  
ALTER DATABASE CustomerSales  
    SET ( LOG_SIZE = 10 GB );  
```  

### <a name="e-check-for-current-statistics-values"></a>E. 現在の統計値を確認する

次のクエリを実行すると、すべてのデータベースについて現在の統計値が返されます。 値が 1 の場合は機能がオンであることを意味し、値が 0 の場合は機能がオフであることを意味します。

```sql
SELECT NAME,
    is_auto_create_stats_on,
    is_auto_update_stats_on,
    is_auto_update_stats_async_on
FROM sys.databases;
```
### <a name="f-enable-auto-create-and-auto-update-stats-for-a-database"></a>F. データベースに対して統計の自動作成および自動更新を有効にする
次のステートメントを使用して、データベース CustomerSales について自動的かつ非同期的に統計を作成および更新する機能を有効にします。  これにより、高品質のクエリ プランを作成するために必要に応じて統計が作成および更新されます。

```sql
ALTER DATABASE CustomerSales
    SET AUTO_CREATE_STATISTICS ON;
ALTER DATABASE CustomerSales
    SET AUTO_UPDATE_STATISTICS ON; 
ALTER DATABASE CustomerSales
    SET AUTO_UPDATE_STATISTICS_ASYNC ON;
```
  
## <a name="see-also"></a>参照  
 [CREATE DATABASE &#40;並列データ ウェアハウス&#41;](../../t-sql/statements/create-database-parallel-data-warehouse.md)   
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)  
  
  
