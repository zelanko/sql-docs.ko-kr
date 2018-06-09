---
title: '방법: SQLSRV 드라이버를 사용 하 여 I/O 매개 변수를 검색 | Microsoft Docs'
ms.custom: ''
ms.date: 04/12/2018
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- stored procedure support
ms.assetid: 9a7c5f60-67f9-4968-a3a8-c256ee481da2
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 57143ae8694bba2bdeae3ff552b2ebb089ce6536
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34563931"
---
# <a name="how-to-retrieve-input-and-output-parameters-using-the-sqlsrv-driver"></a>How to: Retrieve Input and Output Parameters Using the SQLSRV Driver
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

이 항목에서는 SQLSRV 드라이버를 사용하여 하나의 매개 변수가 입출력 매개 변수로 정의된 저장 프로시저를 호출하는 방법 및 결과를 검색하는 방법을 보여 줍니다. 출력 또는 입력/출력 매개 변수를 검색할 때 저장된 프로시저에서 반환 된 모든 결과 반환 된 매개 변수 값에 액세스 하기 전에 사용 되어야 합니다.  
  
> [!NOTE]  
> 초기화되거나 **null**, **날짜/시간**또는 스트림 형식으로 업데이트되는 변수는 출력 매개 변수로 사용할 수 없습니다.  
  
## <a name="example-1"></a>예 1
다음 예제에서는 지정된 직원이 사용할 수 있는 휴가 시간에서 사용한 휴가 시간을 빼는 저장 프로시저를 호출합니다. 사용한 휴가 시간을 나타내는 변수 *$vacationHrs*가 저장 프로시저에 입력 매개 변수로 전달됩니다. 사용할 수 있는 휴가 시간을 업데이트한 다음 저장 프로시저는 동일한 매개 변수를 사용하여 나머지 휴가 시간 수를 반환합니다.  
  
> [!NOTE]  
> *$vacationHrs* 를 4로 초기화하면 반환된 PHPTYPE을 정수로 설정합니다. 데이터 형식 무결성을 보장하려면 저장 프로시저를 호출하기 전에 입출력 매개 변수를 초기화하거나 원하는 PHPTYPE을 지정해야 합니다. PHPTYPE 지정에 대한 자세한 내용은 [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md)을 참조하세요.  
  
저장된 프로시저가 두 결과 반환 하기 때문에 [sqlsrv_next_result](../../connect/php/sqlsrv-next-result.md) 저장된 프로시저가 출력 매개 변수의 값을 사용할 수 있도록 실행 된 후 호출 해야 합니다. 호출한 후 **sqlsrv_next_result**, *$vacationHrs* 저장된 프로시저에서 반환 된 출력 매개 변수의 값을 포함 합니다.  
  
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
$tsql_dropSP = "IF OBJECT_ID('SubtractVacationHours', 'P') IS NOT NULL  
                DROP PROCEDURE SubtractVacationHours";  
$stmt1 = sqlsrv_query( $conn, $tsql_dropSP);  
if( $stmt1 === false )  
{  
     echo "Error in executing statement 1.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Create the stored procedure. */  
$tsql_createSP = "CREATE PROCEDURE SubtractVacationHours  
                        @EmployeeID int,  
                        @VacationHrs smallint OUTPUT  
                  AS  
                  UPDATE HumanResources.Employee  
                  SET VacationHours = VacationHours - @VacationHrs  
                  WHERE EmployeeID = @EmployeeID;  
                  SET @VacationHrs = (SELECT VacationHours  
                                      FROM HumanResources.Employee  
                                      WHERE EmployeeID = @EmployeeID)";  
  
$stmt2 = sqlsrv_query( $conn, $tsql_createSP);  
if( $stmt2 === false )  
{  
     echo "Error in executing statement 2.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/*--------- The next few steps call the stored procedure. ---------*/  
  
/* Define the Transact-SQL query. Use question marks (?) in place of  
the parameters to be passed to the stored procedure */  
$tsql_callSP = "{call SubtractVacationHours( ?, ?)}";  
  
/* Define the parameter array. By default, the first parameter is an  
INPUT parameter. The second parameter is specified as an INOUT  
parameter. Initializing $vacationHrs to 8 sets the returned PHPTYPE to  
integer. To ensure data type integrity, output parameters should be  
initialized before calling the stored procedure, or the desired  
PHPTYPE should be specified in the $params array.*/  
  
$employeeId = 4;  
$vacationHrs = 8;  
$params = array(   
                 array($employeeId, SQLSRV_PARAM_IN),  
                 array(&$vacationHrs, SQLSRV_PARAM_INOUT)  
               );  
  
/* Execute the query. */  
$stmt3 = sqlsrv_query( $conn, $tsql_callSP, $params);  
if( $stmt3 === false )  
{  
     echo "Error in executing statement 3.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Display the value of the output parameter $vacationHrs. */  
sqlsrv_next_result($stmt3);  
echo "Remaining vacation hours: ".$vacationHrs;  
  
/*Free the statement and connection resources. */  
sqlsrv_free_stmt( $stmt1);  
sqlsrv_free_stmt( $stmt2);  
sqlsrv_free_stmt( $stmt3);  
sqlsrv_close( $conn);  
?>  
```  

> [!NOTE]
> 값의 범위 밖에 있는 될 수 있습니다 하는 경우는 입/출력 매개 변수는 bigint 형식에 바인딩할 때는 [정수](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md), SQL 필드 유형을 해당 SQLSRV_SQLTYPE_BIGINT로 지정 해야 합니다. 그렇지 않으면 "값 범위를 벗어났습니다" 예외가 발생할 수 있습니다.

## <a name="example-2"></a>예제 2
이 코드 예제를 입/출력 매개 변수로 큰 bigint 값을 바인딩하는 방법을 보여 줍니다.  

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
$stmt = sqlsrv_prepare($conn, $outSql, array(array(&$bigintOut, SQLSRV_PARAM_INOUT, null, SQLSRV_SQLTYPE_BIGINT)));
sqlsrv_execute($stmt);
echo "$bigintOut\n";   // Expect 9223372036854

sqlsrv_free_stmt($stmt);  
sqlsrv_close($conn);  

?>
```

## <a name="see-also"></a>관련 항목  
[방법: SQLSRV 드라이버를 사용하여 매개 변수 방향 지정](../../connect/php/how-to-specify-parameter-direction-using-the-sqlsrv-driver.md)

[방법: SQLSRV 드라이버를 사용하여 출력 매개 변수 검색](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)

[데이터 검색](../../connect/php/retrieving-data.md)  
  
