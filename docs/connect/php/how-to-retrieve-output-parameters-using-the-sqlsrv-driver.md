---
title: '方法: SQLSRV ドライバーを使用して出力パラメーターの取得 |Microsoft ドキュメント'
ms.custom: ''
ms.date: 04/11/2018
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- stored procedure support
ms.assetid: 1157bab7-6ad1-4bdb-a81c-662eea3e7fcd
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 81a94f68d7198285125236337a0025e41f1bf8ef
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2018
ms.locfileid: "34563890"
---
# <a name="how-to-retrieve-output-parameters-using-the-sqlsrv-driver"></a>方法: SQLSRV ドライバーを使用して出力パラメーターを取得する
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

このトピックでは、1 つのパラメーターが出力パラメーターとして定義されているストアド プロシージャを呼び出す方法について説明します。 出力パラメーターまたは入出力パラメーターを取得するには場合、は、返されるパラメーター値にアクセスする前に、ストアド プロシージャによって返されるすべての結果が使用する必要があります。  
  
> [!NOTE]  
> **null**、 **DateTime**、またはストリーム型に初期化または更新される変数は出力パラメーターとして使用できません。  
  
SQLSRV_SQLTYPE_VARCHAR('max') などのストリーム型が出力パラメーターとして使用されている場合、データの切り捨てが発生することがあります。 ストリーム型は出力パラメーターとしてサポートされません。 非ストリーム型の場合、出力パラメーターの長さが指定されていないか、または指定された長さが出力パラメーターに十分な大きさでない場合に、データの切り捨てが発生することがあります。  
  
## <a name="example-1"></a>例 1
次の例では、指定された従業員による年度累計売上を返すストアド プロシージャを呼び出しています。 PHP 変数 *$lastName* は入力パラメーターで、 *$salesYTD* は出力パラメーターです。  
  
> [!NOTE]  
> *$salesYTD* を 0.0 に初期化すると、返される PHPTYPE が **float**に設定されます。 データ型の整合性を確保するため、ストアド プロシージャを呼び出す前に出力パラメーターを初期化するか、目的の PHPTYPE を指定する必要があります。 PHPTYPE の指定については、「 [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md)」を参照してください。  
  
ストアド プロシージャによって返される結果は 1 つだけであるため、 *$salesYTD* には、ストアド プロシージャが実行された直後の出力パラメーターの戻り値が格納されます。  
  
> [!NOTE]  
> 正規の構文を使用してストアド プロシージャを呼び出すことをお勧めします。 正規の構文の詳細については、次を参照してください。[ストアド プロシージャの呼び出し](../../relational-databases/native-client-odbc-stored-procedures/calling-a-stored-procedure.md)です。  
  
例では、SQL Server および[AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works)データベースがローカル コンピューターにインストールされています。 コマンド ラインからこの例を実行すると、すべての出力はコンソールに書き込まれます。  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and   
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Drop the stored procedure if it already exists. */  
$tsql_dropSP = "IF OBJECT_ID('GetEmployeeSalesYTD', 'P') IS NOT NULL  
                DROP PROCEDURE GetEmployeeSalesYTD";  
$stmt1 = sqlsrv_query( $conn, $tsql_dropSP);  
if( $stmt1 === false )  
{  
     echo "Error in executing statement 1.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Create the stored procedure. */  
$tsql_createSP = " CREATE PROCEDURE GetEmployeeSalesYTD  
                   @SalesPerson nvarchar(50),  
                   @SalesYTD money OUTPUT  
                   AS  
                   SELECT @SalesYTD = SalesYTD  
                   FROM Sales.SalesPerson AS sp  
                   JOIN HumanResources.vEmployee AS e   
                   ON e.EmployeeID = sp.SalesPersonID  
                   WHERE LastName = @SalesPerson";  
$stmt2 = sqlsrv_query( $conn, $tsql_createSP);  
if( $stmt2 === false )  
{  
     echo "Error in executing statement 2.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/*--------- The next few steps call the stored procedure. ---------*/  
  
/* Define the Transact-SQL query. Use question marks (?) in place of  
 the parameters to be passed to the stored procedure */  
$tsql_callSP = "{call GetEmployeeSalesYTD( ?, ? )}";  
  
/* Define the parameter array. By default, the first parameter is an  
INPUT parameter. The second parameter is specified as an OUTPUT  
parameter. Initializing $salesYTD to 0.0 sets the returned PHPTYPE to  
float. To ensure data type integrity, output parameters should be  
initialized before calling the stored procedure, or the desired  
PHPTYPE should be specified in the $params array.*/  
$lastName = "Blythe";  
$salesYTD = 0.0;  
$params = array(   
                 array($lastName, SQLSRV_PARAM_IN),  
                 array(&$salesYTD, SQLSRV_PARAM_OUT)  
               );  
  
/* Execute the query. */  
$stmt3 = sqlsrv_query( $conn, $tsql_callSP, $params);  
if( $stmt3 === false )  
{  
     echo "Error in executing statement 3.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Display the value of the output parameter $salesYTD. */  
echo "YTD sales for ".$lastName." are ". $salesYTD. ".";  
  
/*Free the statement and connection resources. */  
sqlsrv_free_stmt( $stmt1);  
sqlsrv_free_stmt( $stmt2);  
sqlsrv_free_stmt( $stmt3);  
sqlsrv_close( $conn);  
?>  
```  

> [!NOTE]
> 場合は、値がの範囲外に至る可能性があります、bigint 型出力パラメーターをバインドするときに、[整数](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)、SQLSRV_SQLTYPE_BIGINT として、SQL フィールドの種類を指定する必要があります。 それ以外の場合、「範囲外の値」例外可能性があります。

## <a name="example-2"></a>例 2
このコード サンプルでは、出力パラメーターとして大きな bigint 値をバインドする方法を示します。  

```
<?php
$serverName = "(local)";
$connectionInfo = array("Database"=>"testDB");  
$conn = sqlsrv_connect($serverName, $connectionInfo);  
if ($conn === false) {  
    echo "Could not connect.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  

// Assume the stored procedure spTestProcedure exists, which retrieves a bigint value of some large number
// e.g. 9223372036854
$bigintOut = 0;
$outSql = "{CALL spTestProcedure (?)}";
$stmt = sqlsrv_prepare($conn, $outSql, array(array(&$bigintOut, SQLSRV_PARAM_OUT, null, SQLSRV_SQLTYPE_BIGINT)));
sqlsrv_execute($stmt);
echo "$bigintOut\n";   // Expect 9223372036854

sqlsrv_free_stmt($stmt);  
sqlsrv_close($conn);  

?>
```

## <a name="see-also"></a>参照  
[方法: SQLSRV ドライバーを使用してパラメーターの方向を指定する](../../connect/php/how-to-specify-parameter-direction-using-the-sqlsrv-driver.md)

[方法: SQLSRV ドライバーを使用して入力/出力パラメーターを取得する](../../connect/php/how-to-retrieve-input-and-output-parameters-using-the-sqlsrv-driver.md)

[データの取得](../../connect/php/retrieving-data.md)  
  
