---
title: "外部ファイル形式を削除 (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 8cf9009b-59f9-4aac-bef1-dcf2cf0708b2
caps.latest.revision: 12
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 25719f7617cbb75b1b9467a00c392f703a9710ac
ms.contentlocale: ja-jp
ms.lasthandoff: 09/01/2017

---
# <a name="drop-external-file-format-transact-sql"></a>外部のファイル形式の削除 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  PolyBase 外部ファイルの形式を削除します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
-- Syntax for SQL Server, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
-- Drop an external file format  
DROP EXTERNAL FILE FORMAT external_file_format_name  
[;]  
```  
  
## <a name="arguments"></a>引数  
 *external_file_format_name*  
 削除するには、外部のファイル形式の名前です。  
  
## <a name="metadata"></a>メタデータ  
 外部ファイル形式の使用の一覧を表示する、 [sys.external_file_formats & #40 です。TRANSACT-SQL と #41 です。](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md)システム ビューです。  
  
```  
SELECT * FROM sys.external_file_formats;  
```  
  
## <a name="permissions"></a>Permissions  
 必要と任意の外部のファイル形式を変更します。  
  
## <a name="general-remarks"></a>全般的な解説  
 外部のファイル形式を削除しても、外部のデータは削除されません。  
  
## <a name="locking"></a>ロック  
 共有ロックは、外部ファイルのオブジェクトの書式設定されます。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-basic-syntax"></a>A. 基本的な構文を使用します。  
  
```  
DROP EXTERNAL FILE FORMAT myfileformat;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例:[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]と[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-using-basic-syntax"></a>B. 基本的な構文を使用します。  
  
```  
DROP EXTERNAL FILE FORMAT myfileformat;  
```  
  
## <a name="see-also"></a>参照  
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)  
  
  

