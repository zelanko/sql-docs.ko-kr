---
title: '방법: SQLSRV 드라이버를 사용 하 여 경고 및 오류 처리 | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- errors and warnings
ms.assetid: fa231d60-4c06-4137-89e8-097c28638c5d
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 16791a307fe317aa9495c5b4173cb1ebbb23d719
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35307422"
---
# <a name="how-to-handle-errors-and-warnings-using-the-sqlsrv-driver"></a>방법: SQLSRV 드라이버를 사용하여 오류 및 경고 처리
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

기본적으로 SQLSRV 드라이버는 경고를 처리 오류가 있습니다. 에 대 한 호출을 **sqlsrv** 오류 또는 경고를 생성 하는 함수 반환 **false**합니다. 이 항목에서는 이 기본 동작을 해제하는 방법과 경고를 오류와 별도로 처리하는 방법을 보여 줍니다.  
  
> [!NOTE]  
> 경고를 오류로 처리하는 기본 동작에는 몇 가지 예외가 있습니다. SQLSTATE 값 01000, 01001, 01003 및 01S02에 해당하는 경고는 오류로 처리되지 않습니다.  
  
## <a name="example"></a>예제  
다음 코드 예제에서는 두 개의 사용자 정의 함수를 사용 하 여 **DisplayErrors** 및 **DisplayWarnings**로, 오류 및 경고를 처리 합니다. 해당 예제에서 다음을 수행하여 경고와 오류를 별도로 처리하는 방법을 보여 줍니다.  
  
1.  경고를 오류로 처리하는 기본 동작을 해제합니다.  
  
2.  직원의 휴가 시간을 업데이트하는 저장 프로시저를 만들고 나머지 휴가 시간을 출력 매개 변수로 반환합니다. 직원의 사용 가능한 휴가 시간이 0보다 작은 경우 저장 프로시저에서 경고를 인쇄합니다.  
  
3.  각 직원에 대한 저장 프로시저를 호출하여 여러 직원의 휴가 시간을 업데이트하고 발생하는 모든 경고 및 오류에 해당하는 메시지를 표시합니다.  
  
4.  각 직원에 대한 나머지 휴가 시간을 표시합니다.  
  
첫 번째 호출에서는 **sqlsrv** 함수 ([sqlsrv_configure](../../connect/php/sqlsrv-configure.md)), 경고를 오류로 처리 됩니다. 경고가 오류 수집에 추가되기 때문에 오류와 별도로 경고를 확인할 필요가 없습니다. 그러나 이후에 **sqlsrv** 함수를 호출할 때는 경고가 오류로 처리되지 않으므로 경고와 오류에 대해 명시적으로 확인해야 합니다.  
  
또한 **sqlsrv** 함수에 대한 각 호출 이후 예제 코드가 오류를 확인합니다. 권장 방법입니다.  
  
이 예에서는 가정 하는 SQL Server 및 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 데이터베이스가 로컬 컴퓨터에 설치 됩니다. 모든 출력은 명령줄에서 예제가 실행될 때 콘솔에 기록됩니다. 예제가 AdventureWorks 데이터베이스의 새 설치에 대해 실행될 때 세 가지 경고 및 두 가지 오류를 생성합니다. 처음 두 가지 경고는 데이터베이스에 연결할 때 발생하는 표준 경고입니다. 세 번째 경고는 직원의 사용 가능한 휴가 시간이 0보다 작은 값으로 업데이트되므로 발생합니다. 직원의 사용 가능한 휴가 시간이 -40시간보다 작은 값으로 업데이트되기 때문에(테이블의 제약 조건 위반) 오류가 발생합니다.  
  
```  
<?php  
/* Turn off the default behavior of treating errors as warnings.  
Note: Turning off the default behavior is done here for demonstration  
purposes only. If setting the configuration fails, display errors and  
exit the script. */  
if( sqlsrv_configure("WarningsReturnAsErrors", 0) === false)  
{  
     DisplayErrors();  
     die;  
}  
  
/* Connect to the local server using Windows Authentication and   
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array("Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
/* If the connection fails, display errors and exit the script. */  
if( $conn === false )  
{  
     DisplayErrors();  
     die;  
}  
/* Display any warnings. */  
DisplayWarnings();  
  
/* Drop the stored procedure if it already exists. */  
$tsql1 = "IF OBJECT_ID('SubtractVacationHours', 'P') IS NOT NULL  
                DROP PROCEDURE SubtractVacationHours";  
$stmt1 = sqlsrv_query($conn, $tsql1);  
  
/* If the query fails, display errors and exit the script. */  
if( $stmt1 === false)  
{  
     DisplayErrors();  
     die;  
}  
/* Display any warnings. */  
DisplayWarnings();  
  
/* Free the statement resources. */  
sqlsrv_free_stmt( $stmt1 );  
  
/* Create the stored procedure. */  
$tsql2 = "CREATE PROCEDURE SubtractVacationHours  
                  @EmployeeID int,  
                  @VacationHours smallint OUTPUT  
              AS  
                  UPDATE HumanResources.Employee  
                  SET VacationHours = VacationHours - @VacationHours  
                  WHERE EmployeeID = @EmployeeID;  
                  SET @VacationHours = (SELECT VacationHours    
                                       FROM HumanResources.Employee  
                                       WHERE EmployeeID = @EmployeeID);  
              IF @VacationHours < 0   
              BEGIN  
                PRINT 'WARNING: Vacation hours are now less than zero.'  
              END;";  
$stmt2 = sqlsrv_query( $conn, $tsql2 );  
  
/* If the query fails, display errors and exit the script. */  
if( $stmt2 === false)  
{  
     DisplayErrors();  
     die;  
}  
/* Display any warnings. */  
DisplayWarnings();  
  
/* Free the statement resources. */  
sqlsrv_free_stmt( $stmt2 );  
  
/* Set up the array that maps employee ID to used vacation hours. */  
$emp_hrs = array (7=>4, 8=>5, 9=>8, 11=>50);  
  
/* Initialize variables that will be used as parameters. */  
$employeeId = 0;  
$vacationHrs = 0;  
  
/* Set up the parameter array. */  
$params = array(  
                 array(&$employeeId, SQLSRV_PARAM_IN),  
                 array(&$vacationHrs, SQLSRV_PARAM_INOUT)  
                );  
  
/* Define and prepare the query to substract used vacation hours. */  
$tsql3 = "{call SubtractVacationHours(?, ?)}";  
$stmt3 = sqlsrv_prepare($conn, $tsql3, $params);  
  
/* If the statement preparation fails, display errors and exit the script. */  
if( $stmt3 === false)  
{  
     DisplayErrors();  
     die;  
}  
/* Display any warnings. */  
DisplayWarnings();  
  
/* Loop through the employee=>vacation hours array. Update parameter  
 values before statement execution. */  
foreach(array_keys($emp_hrs) as $employeeId)  
{  
     $vacationHrs = $emp_hrs[$employeeId];  
     /* Execute the query.  If it fails, display the errors. */  
     if( sqlsrv_execute($stmt3) === false)  
     {  
          DisplayErrors();  
          die;  
     }  
     /* Display any warnings. */  
     DisplayWarnings();  
  
     /*Move to the next result returned by the stored procedure. */  
     if( sqlsrv_next_result($stmt3) === false)  
     {  
          DisplayErrors();  
          die;  
     }  
     /* Display any warnings. */  
     DisplayWarnings();  
  
     /* Display updated vacation hours. */  
     echo "EmployeeID $employeeId has $vacationHrs ";  
     echo "remaining vacation hours.\n";  
}  
  
/* Free the statement and connection resources. */  
sqlsrv_free_stmt( $stmt3 );  
sqlsrv_close( $conn );  
  
/* ------------- Error Handling Functions --------------*/  
function DisplayErrors()  
{  
     $errors = sqlsrv_errors(SQLSRV_ERR_ERRORS);  
     foreach( $errors as $error )  
     {  
          echo "Error: ".$error['message']."\n";  
     }  
}  
  
function DisplayWarnings()  
{  
     $warnings = sqlsrv_errors(SQLSRV_ERR_WARNINGS);  
     if(!is_null($warnings))  
     {  
          foreach( $warnings as $warning )  
          {  
               echo "Warning: ".$warning['message']."\n";  
          }  
     }  
}  
?>  
```  
  
## <a name="see-also"></a>관련 항목  
[방법: SQLSRV 드라이버를 사용하여 오류 및 경고 처리 구성](../../connect/php/how-to-configure-error-and-warning-handling-using-the-sqlsrv-driver.md)

[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)  
  
