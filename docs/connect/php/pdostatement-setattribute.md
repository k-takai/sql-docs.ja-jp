---
title: Pdostatement::setattribute |Microsoft ドキュメント
ms.custom: ''
ms.date: 07/13/2017
ms.prod: sql
ms.prod_service: connectivity
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 329d9b5e-1c5d-40b0-9127-1051d0646fc7
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dbbb53da59f463c8dc601963f02b5b77ef6ec4b6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="pdostatementsetattribute"></a>PDOStatement::setAttribute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

定義済み PDO 属性またはカスタム ドライバー属性のいずれかの属性値を設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
bool PDOStatement::setAttribute ($attribute, $value );  
```  
  
#### <a name="parameters"></a>パラメーター  
$*属性*::attr _ * または pdo::sqlsrv_attr _ のいずれかの整数\*定数。 使用可能な属性の一覧については、「解説」セクションを参照してください。  
  
$*値*: 指定された $ 用に設定する (複合) 値*属性*です。  
  
## <a name="return-value"></a>戻り値  
成功した場合は TRUE、それ以外の場合は FALSE です。  
  
## <a name="remarks"></a>解説  
次の表に、使用可能な属性の一覧を示します。  
  
|attribute|値|Description|  
|-------------|----------|---------------|  
|PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE|PHP メモリの制限に 1。|クライアント側カーソルの結果セットを保持するバッファーのサイズを設定します。<br /><br />既定では 10,240 KB (10 MB) です。<br /><br />クライアント側のカーソルの詳細については、次を参照してください。[カーソルの種類&#40;PDO_SQLSRV ドライバー&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)です。|  
|PDO::SQLSRV_ATTR_ENCODING|Integer<br /><br />PDO::SQLSRV_ENCODING_UTF8 (既定)<br /><br />PDO::SQLSRV_ENCODING_SYSTEM<br /><br />PDO::SQLSRV_ENCODING_BINARY|ドライバーがサーバーとの通信に使用する文字セット エンコーディングを設定します。|  
|PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE|true または false|数値の SQL 型 (ビット、integer、smallint、tinyint、float または real) と列からの数値のフェッチを処理します。<br /><br />接続オプション フラグ ATTR_STRINGIFY_FETCHES が on の場合は、SQLSRV_ATTR_FETCHES_NUMERIC_TYPE がある場合でも文字列は、戻り値です。<br /><br />バインド列で返される PDO 型 PDO_PARAM_INT がある場合は、SQLSRV_ATTR_FETCHES_NUMERIC_TYPE がオフの場合でも、int は整数型の列からの戻り値です。|  
|PDO::SQLSRV_ATTR_QUERY_TIMEOUT|Integer|クエリのタイムアウト (秒単位) を設定します。<br /><br />既定で、ドライバーは、結果を無制限に待機します。 負の数値は許可できません。<br /><br />0 は、タイムアウトがないことを示します。|  
  
## <a name="example"></a>例  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "", array('MultipleActiveResultSets'=>false )  );  
  
$stmt = $conn->prepare('SELECT * FROM Person.ContactType');  
  
echo $stmt->getAttribute( constant( "PDO::ATTR_CURSOR" ) );  
  
echo "\n";  
  
$stmt->setAttribute(PDO::SQLSRV_ATTR_QUERY_TIMEOUT, 2);  
echo $stmt->getAttribute( constant( "PDO::SQLSRV_ATTR_QUERY_TIMEOUT" ) );  
?>  
```  
  
## <a name="see-also"></a>参照  
[PDOStatement クラス](../../connect/php/pdostatement-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
