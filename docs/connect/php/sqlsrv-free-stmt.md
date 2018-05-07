---
title: sqlsrv_free_stmt | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- sqlsrv_free_stmt
apitype: NA
helpviewer_keywords:
- sqlsrv_free_stmt
- API Reference, sqlsrv_free_stmt
ms.assetid: 3c71f432-36ad-41e1-8ac7-587c82539448
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8a57257fcaddfc1b5e520c99de0c217a7a57a6a1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsrvfreestmt"></a>sqlsrv_free_stmt
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

지정된 문과 연결된 모든 리소스를 해제합니다. 이 문은 이 함수를 호출한 후에는 다시 사용할 수 없습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
sqlsrv_free_stmt( resource $stmt)  
```  
  
#### <a name="parameters"></a>매개 변수  
*$stmt*: 닫을 문입니다.  
  
## <a name="return-value"></a>반환 값  
잘못된 매개 변수를 사용하여 함수를 호출하지 않는 한 부울 값 **true** 입니다. 잘못된 매개 변수를 사용하여 함수를 호출하는 경우에는 **false** 가 반환됩니다.  
  
> [!NOTE]  
> **Null** 은 이 함수에 대해 유효한 매개 변수입니다. 그러면 스크립트에서 함수가 여러 번 호출될 수 있습니다. 예를 들어 오류 조건에서 문을 해제 하 고 스크립트의 끝에서 다시 해제 하는 경우 두 번째 호출에서를 **sqlsrv_free_stmt** 돌아갑니다 **true** 에 첫 번째 호출 하므로 **sqlsrv_ free_stmt** (오류 조건) 문 리소스를 설정 **null**합니다.  
  
## <a name="example"></a>예제  
다음 예제에서는 문 리소스를 만들어 간단한 쿼리를 실행하고 **sqlsrv_free_stmt** 를 호출하여 문과 연결된 모든 리소스를 해제합니다. 이 예에서는 가정 하는 SQL Server 및 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 데이터베이스가 로컬 컴퓨터에 설치 됩니다. 모든 출력은 명령줄에서 예제가 실행될 때 콘솔에 기록됩니다.  
  
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
  
$stmt = sqlsrv_query( $conn, "SELECT * FROM Person.Contact");  
if( $stmt )  
{  
     echo "Statement executed.\n";  
}  
else  
{  
     echo "Query could not be executed.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/*-------------------------------  
     Process query results here.  
-------------------------------*/  
  
/* Free the statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>관련 항목:  
[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)  

[설명서의 코드 예제 정보](../../connect/php/about-code-examples-in-the-documentation.md)  

[sqlsrv_cancel](../../connect/php/sqlsrv-cancel.md)  
  
