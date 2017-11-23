---
title: sqlsrv_num_fields | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: sqlsrv_num_fields
apitype: NA
helpviewer_keywords:
- sqlsrv_num_fields
- API Reference, sqlsrv_num_fields
ms.assetid: 03ca1860-01ed-408c-862a-57a7355de4bf
caps.latest.revision: "17"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 978f04e3796cc104844ca86e3ac74b1c24cc10e1
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="sqlsrvnumfields"></a>sqlsrv_num_fields
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

활성 결과 집합의 필드 수를 검색합니다. **sqlsrv_num_fields** 실행 전 또는 후 준비 된 문에서 호출할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
sqlsrv_num_fields( resource $stmt)  
```  
  
#### <a name="parameters"></a>매개 변수  
*$stmt*: 대상 결과 집합이 활성화되는 문입니다.  
  
## <a name="return-value"></a>반환 값  
활성 결과 집합에서 필드의 수를 나타내는 정수 값입니다. 오류가 발생하면 부울 값 **false** 가 반환됩니다.  
  
## <a name="example"></a>예제  
다음 예제에서는 쿼리를 실행하여 Adventureworks 데이터베이스의 *HumanResources.Department* 테이블에 있는 상위 3개의 행에 대해 모든 필드를 검색합니다. **sqlsrv_num_fields** 함수 결과 집합의 필드 수를 결정 합니다. 이렇게 하면 반환된 각 행의 필드를 반복하면서 데이터를 표시할 수 있습니다.  
  
이 예제에서는 SQL Server 및 [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) 데이터베이스가 로컬 컴퓨터에 설치된 것으로 가정합니다. 모든 출력은 명령줄에서 예제가 실행될 때 콘솔에 기록됩니다.  
  
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
  
/* Define and execute the query. */  
$tsql = "SELECT TOP (3) * FROM HumanResources.Department";  
$stmt = sqlsrv_query($conn, $tsql);  
if( $stmt === false)  
{  
     echo "Error in executing query.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve the number of fields. */  
$numFields = sqlsrv_num_fields( $stmt );  
  
/* Iterate through each row of the result set. */  
while( sqlsrv_fetch( $stmt ))  
{  
     /* Iterate through the fields of each row. */  
     for($i = 0; $i < $numFields; $i++)  
     {  
          echo sqlsrv_get_field($stmt, $i,   
                   SQLSRV_PHPTYPE_STRING(SQLSRV_ENC_CHAR))." ";  
     }  
     echo "\n";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt );  
sqlsrv_close( $conn );  
?>  
```  
  
## <a name="see-also"></a>참고 항목  
[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)  
[sqlsrv_field_metadata](../../connect/php/sqlsrv-field-metadata.md)  
[설명서의 코드 예제 정보](../../connect/php/about-code-examples-in-the-documentation.md)  
  
