---
title: プロジェクトの設定 (型のマッピング) (AccessToSQL) |Microsoft ドキュメント
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Access data types
- data types, default mappings
- default data type mappings
- Project Settings dialog box, Type Mapping
- SQL Server data types
- Type Mapping settings
ms.assetid: b87b9683-abed-4677-8c50-18bdba704655
caps.latest.revision: 16
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: bd5bc6a0db71d2836c068a261681d813bc2011b3
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/05/2018
ms.locfileid: "34774468"
---
# <a name="project-settings-type-mapping-accesstosql"></a>プロジェクトの設定 (型のマッピング) (AccessToSQL)
プロジェクトの種類のマッピング設定では、SSMA プロジェクトの既定の型マッピングを設定できます。 個々 のデータベース オブジェクトの型マッピングを指定することもできます。 詳細については、次を参照してください。[マッピング ソースとターゲットのデータ型](http://msdn.microsoft.com/en-us/b362a075-16e7-423f-b63f-e1e9f02844a9)です。  
  
型のマッピングがで使用できる、**プロジェクト設定**と**プロジェクト設定の既定の** ダイアログ ボックス。  
  
-   使用して、**プロジェクト設定**ダイアログ ボックスを現在のプロジェクトの構成オプションを設定します。 型マッピングの設定にアクセスする、**ツール**メニューの **プロジェクト設定**、順にクリック**型マッピング**左側のウィンドウでします。  
  
-   使用して、**プロジェクト設定の既定の**ダイアログ ボックスをすべてのプロジェクトの構成オプションを設定します。 型マッピングの設定にアクセスする、**ツール**メニューの **プロジェクト設定の既定の**、対象の設定が表示する/から変更を必要な移行プロジェクトの種類を選択**移行のターゲット バージョン**ドロップダウンをクリックして**型マッピング**左側のウィンドウでします。  
  
## <a name="options"></a>および  
**変換元の型**  
アクセス データ型にマップします。  
  
**ターゲットの種類**  
ターゲット[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]または指定したアクセスのデータ型の SQL Azure のデータ型。  
  
次の表は、ソースとターゲットのデータ型の既定のマッピングを示します。  
  
|Access のデータ型|SQL Server データ型|  
|--------------------|------------------------|  
|**binary[\*..\*]**|**varbinary[\*]**|  
|**boolean**|**bit**|  
|**byte**|**tinyint**|  
|**currency**|**money**|  
|**date**|**datetime**|  
|**decimal**|**float**|  
|**double**|**float**|  
|**guid**|**uniqueidentifier**|  
|**整数 (integer)**|**smallint**|  
|**long**|**int**|  
|**longbinary**|**varbinary(max)**|  
|**memo**|**nvarchar(max)**|  
|**memo** - Access 97|**varchar(max)**|  
|**single**|**real**|  
|**text[\*..\*]**|**nvarchar[\*]**|  
|**テキスト [\*..\*]** - Access 97|**varchar[\*]**|  
  
**[追加]**  
マッピングのリストに、データ型を追加する をクリックします。  
  
**[編集]**  
マッピングのリスト内のデータ型を編集するのには、をクリックします。  
  
**削除**  
マッピングのリストから選択したデータ型のマッピングを削除する をクリックします。  
  
**既定値にリセット**  
すべてのデータ型マッピングを SSMA の既定値にリセットする をクリックします。  
  
## <a name="see-also"></a>参照  
[ソースとターゲットのデータ型のマッピング](http://msdn.microsoft.com/en-us/b362a075-16e7-423f-b63f-e1e9f02844a9)  
[ユーザー インターフェイス Reference(Access)](http://msdn.microsoft.com/en-us/af24c303-4a41-449b-9c86-d6558a97e839)  
  
