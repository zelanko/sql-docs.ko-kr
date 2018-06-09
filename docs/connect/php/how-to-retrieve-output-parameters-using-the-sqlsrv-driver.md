---
title: '방법: SQLSRV 드라이버를 사용 하 여 출력 매개 변수 검색 | Microsoft Docs'
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
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34563891"
---
# <a name="how-to-retrieve-output-parameters-using-the-sqlsrv-driver"></a>방법: SQLSRV 드라이버를 사용하여 출력 매개 변수 검색
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

이 항목에서는 하나의 매개 변수가 출력 매개 변수로 정의된 저장 프로시저를 호출하는 방법을 설명합니다. 출력 또는 입력/출력 매개 변수를 검색할 때 저장된 프로시저에서 반환 된 모든 결과 반환 된 매개 변수 값에 액세스 하기 전에 사용 되어야 합니다.  
  
> [!NOTE]  
> 초기화되거나 **null**, **날짜/시간**또는 스트림 형식으로 업데이트되는 변수는 출력 매개 변수로 사용할 수 없습니다.  
  
SQLSRV_SQLTYPE_VARCHAR('max') 같은 스트림 형식을 출력 매개 변수로 사용하면 데이터가 잘릴 수 있습니다. 스트림 형식은 출력 매개 변수로 지원되지 않습니다. 스트림이 아닌 형식의 경우 출력 매개 변수의 길이를 지정하지 않거나 출력 매개 변수에 지정된 길이가 충분히 크지 않은 경우 데이터가 잘릴 수 있습니다.  
  
## <a name="example-1"></a>예 1
다음 예제에서는 지정된 직원이 연간 누계 판매를 반환하는 저장 프로시저를 호출합니다. PHP 변수 *$lastName* 이 입력 매개 변수이고 *$salesYTD* 가 출력 매개 변수입니다.  
  
> [!NOTE]  
> *$salesYTD* 를 0.0으로 초기화하면 반환된 PHPTYPE을 **부동**으로 설정합니다. 데이터 형식 무결성을 보장하려면 저장 프로시저를 호출하기 전에 출력 매개 변수를 초기화하거나 원하는 PHPTYPE을 지정해야 합니다. PHPTYPE 지정에 대한 자세한 내용은 [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md)을 참조하세요.  
  
저장 프로시저에서 하나의 결과만 반환하기 때문에 *$salesYTD* 에는 저장 프로시저가 실행된 직후 반환되는 출력 매개 변수 값이 들어 있습니다.  
  
> [!NOTE]  
> 권장되는 방법은 정식 구문을 사용하여 저장 프로시저를 호출하는 것입니다. 정식 구문에 대 한 자세한 내용은 참조 [저장 프로시저 호출](../../relational-databases/native-client-odbc-stored-procedures/calling-a-stored-procedure.md)합니다.  
  
이 예에서는 가정 하는 SQL Server 및 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 데이터베이스가 로컬 컴퓨터에 설치 됩니다. 모든 출력은 명령줄에서 예제가 실행될 때 콘솔에 기록됩니다.  
  
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
> 값의 범위 밖에 있는 될 수 있습니다 하는 경우 출력 매개 변수는 bigint 형식에 바인딩할 때는 [정수](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md), SQL 필드 유형을 해당 SQLSRV_SQLTYPE_BIGINT로 지정 해야 합니다. 그렇지 않으면 "값 범위를 벗어났습니다" 예외가 발생할 수 있습니다.

## <a name="example-2"></a>예제 2
이 코드 예제에는 출력 매개 변수로 큰 bigint 값을 바인딩하는 방법을 보여 줍니다.  

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

## <a name="see-also"></a>관련 항목  
[방법: SQLSRV 드라이버를 사용하여 매개 변수 방향 지정](../../connect/php/how-to-specify-parameter-direction-using-the-sqlsrv-driver.md)

[방법: SQLSRV 드라이버를 사용하여 입력 및 출력 매개 변수 검색](../../connect/php/how-to-retrieve-input-and-output-parameters-using-the-sqlsrv-driver.md)

[데이터 검색](../../connect/php/retrieving-data.md)  
  
