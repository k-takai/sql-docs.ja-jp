---
title: sys.sysdatabases (TRANSACT-SQL) |Microsoft ドキュメント
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.component: system-compatibility-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysdatabases_TSQL
- sys.sysdatabases_TSQL
- sys.sysdatabases
- sysdatabases
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysdatabases compatibility view
- sysdatabases system table
ms.assetid: 60a93880-62f1-4eda-a886-f046706ba90c
caps.latest.revision: 35
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 9a19ff47d576a7a2ffe5a72f609a27d5c1214f70
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
ms.locfileid: "33221973"
---
# <a name="syssysdatabases-transact-sql"></a>sys.sysdatabases (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  インスタンス内の各データベースの 1 つの行を含む[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]です。 ときに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]が最初にインストールされている**sysdatabases**のエントリが含まれています、**マスター**、**モデル**、 **msdb**、および**tempdb**データベース。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名|データ型|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|データベース名|  
|**dbid**|**smallint**|データベース ID|  
|**sid**|**varbinary(85)**|データベース作成者のシステム ID です。|  
|**モード**|**smallint**|データベースの作成中に内部で使用し、データベースをロックします。|  
|**ステータス**|**int**|ステータス ビット、その一部を使用して設定できます[ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md)前述。<br /><br /> 1 = **autoclose** (ALTER DATABASE)<br /><br /> 4 = **select/bulkcopy** (ALTER DATABASE は SET RECOVERY を使用して)<br /><br /> 8 =**間接的に trunc. log** (ALTER DATABASE は SET RECOVERY を使用して)<br /><br /> 16 =**破損ページ検出**(ALTER DATABASE)<br /><br /> 32 =**の読み込み**<br /><br /> 64 =**より前の回復**<br /><br /> 128 =**の回復**<br /><br /> 256 =**は回復されませんでした**<br /><br /> 512 =**オフライン**(ALTER DATABASE)<br /><br /> 1024 =**読み取り専用**(ALTER DATABASE)<br /><br /> 2048 = **dbo でのみ使用**(ALTER DATABASE は SET RESTRICTED_USER を使用して)<br /><br /> 4096 =**シングル ユーザー** (ALTER DATABASE)<br /><br /> 32768 =**緊急モード**<br /><br /> 65536 =**チェックサム**(ALTER DATABASE)<br /><br /> 4,194, 304 = **autoshrink** (ALTER DATABASE)<br /><br /> 1073741824 =**クリーンにシャット ダウン**<br /><br /> 複数のビットが同時にオンであってもかまいません。|  
|**status2**|**int**|16384 = **ANSI null default** (ALTER DATABASE)<br /><br /> 65536 = **concat null yields null** (ALTER DATABASE)<br /><br /> 131, 072 =**再帰トリガー** (ALTER DATABASE)<br /><br /> 1048576 =**ローカル カーソルの既定値は**(ALTER DATABASE)<br /><br /> 8,388, 608 =**識別子を引用符で囲まれた**(ALTER DATABASE)<br /><br /> 33554432 = **cursor close on commit** (ALTER DATABASE)<br /><br /> 67108864 = **ANSI nulls** (ALTER DATABASE)<br /><br /> 268435456 = **ANSI warnings** (ALTER DATABASE)<br /><br /> 536870912 =**完全なテキストが有効な**(を使用して設定**sp_fulltext_database**)|  
|**crdate**|**datetime**|作成日です。|  
|**reserved**|**datetime**|将来の使用のために予約されています。|  
|**category**|**int**|レプリケーションで使用する情報のビットマップです。<br /><br /> 1 = スナップショット レプリケーション用またはトランザクション レプリケーション用にパブリッシュされています。<br /><br /> 2 = スナップショット パブリケーションまたはトランザクション パブリケーションにサブスクライブしています。<br /><br /> 4 = マージ レプリケーション用にパブリッシュされています。<br /><br /> 8 = マージ パブリケーションにサブスクライブしています。<br /><br /> 16 = ディストリビューション データベースです。|  
|**cmptlevel**|**tinyint**|データベースの互換性レベル。 詳細については、「[ALTER DATABASE 互換性レベル &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)」を参照してください。|  
|**filename**|**nvarchar(260)**|データベースのプライマリ ファイルのオペレーティング システム パスと名前です。<br /><br /> **filename**を表示する**dbcreator**、 **sysadmin**、CREATE ANY DATABASE 権限、または、次の権限のいずれかのある権限付与対象ユーザーを持つデータベース所有者: ALTER ANY DATABASE、定義を表示する、任意のデータベースを作成します。 パスとファイル名を返すクエリ、 [sys.sysfiles](../../relational-databases/system-compatibility-views/sys-sysfiles-transact-sql.md)互換性ビューまたは[sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)ビュー。|  
|**version**|**smallint**|このデータベースが作成された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コードの内部バージョン番号です。 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
## <a name="see-also"></a>参照  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [システム ビューへのシステム テーブルのマッピング&#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [互換性ビュー &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
