---
title: sqlsrv_errors | Microsoft Docs
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
- sqlsrv_errors
apitype: NA
helpviewer_keywords:
- API Reference, sqlsrv_errors
- sqlsrv_errors
- errors and warnings
ms.assetid: d1fcffec-f34f-46de-9a0e-343f3b5dbae2
caps.latest.revision: 39
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 589fc732d9d49b58763f6374277d4375cccbbaf8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsrverrors"></a>sqlsrv_errors
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

확장 오류 및/또는 경고 정보에 대 한 마지막 반환 **sqlsrv** 작업을 수행 합니다.  
  
**sqlsrv_errors** 함수 매개 변수 섹션 아래에 지정 된 매개 변수 값 중 하나를 호출 하 여 오류 및/또는 경고 정보를 반환할 수 있습니다.  
  
기본적으로 **sqlsrv** 함수를 호출할 때 생성되는 경고는 오류로 처리되며 **sqlsrv** 함수를 호출할 때 경고가 발생하면 함수가 false를 반환합니다. 그러나 SQLSTATE 값 01000, 01001, 01003 및 01S02에 해당하는 경고는 오류로 처리되지 않습니다.  
  
다음 코드 줄은 위에서 설명한 동작을 해제합니다. **sqlsrv** 함수를 호출할 때 경고가 생성되어도 함수가 false를 반환하지 않습니다.  
  
```  
sqlsrv_configure("WarningsReturnAsErrors", 0);  
```  
  
다음 코드 줄은 기본 동작을 복원합니다. 경고(위에서 언급한 예외 포함)가 오류로 처리됩니다.   
  
```  
sqlsrv_configure("WarningsReturnAsErrors", 1);  
```  
  
설정에 관계 없이 경고만 검색할 수 있습니다를 호출 하 여 **sqlsrv_errors** 하나로 **SQLSRV_ERR_ALL** 또는 **SQLSRV_ERR_WARNINGS** 매개 변수 값 (참조 매개 변수에 자세한 내용은 아래의 섹션)입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
sqlsrv_errors( [int $errorsAndOrWarnings] )  
```  
  
#### <a name="parameters"></a>매개 변수  
*$errorsAndOrWarnings*[선택 사항]: 미리 정의 된 상수입니다. 이 매개 변수는 다음 표에 나열된 값 중 하나를 사용할 수 있습니다.  
  
|Value|Description|  
|---------|---------------|  
|SQLSRV_ERR_ALL|마지막 **sqlsrv** 함수 호출 시 생성된 오류 및 경고가 반환됩니다.|  
|SQLSRV_ERR_ERRORS|마지막 **sqlsrv** 함수 호출 시 생성된 오류가 반환됩니다.|  
|SQLSRV_ERR_WARNINGS|마지막 **sqlsrv** 함수 호출 시 생성된 경고가 반환됩니다.|  
  
매개 변수 값을 지정하지 않은 경우 마지막 **sqlsrv** 함수 호출 시 생성된 오류 및 경고가 반환됩니다.  
  
## <a name="return-value"></a>반환 값  
배열의 **배열** 또는 **null**입니다. 각 **배열** 반환 된 **배열** 세 가지 키-값 쌍을 포함 합니다. 다음 표에는 각 키와 해당 설명이 나와 있습니다.  
  
|Key|Description|  
|-------|---------------|  
|SQLSTATE|ODBC 드라이버에서 발생하는 오류의 경우 ODBC 드라이버에서 반환한 SQLSTATE입니다. SQLSTATE 값에 대 한 ODBC에 대 한 정보를 참조 하십시오. [ODBC 오류 코드](../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md)합니다.<br /><br />[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]에서 발생하는 오류의 경우 IMSSP의 SQLSTATE입니다.<br /><br />[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]에서 발생하는 경고의 경우 01SSP의 SQLSTATE입니다.|  
|코드|SQL Server에서 발생하는 오류의 경우 네이티브 SQL Server 오류 코드입니다.<br /><br />ODBC 드라이버에서 발생하는 오류의 경우 ODBC 드라이버에서 반환된 오류 코드입니다.<br /><br />[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]에서 발생하는 오류의 경우 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 오류 코드입니다. 자세한 내용은 [Handling Errors and Warnings](../../connect/php/handling-errors-and-warnings.md)을 참조하세요.|  
|message|오류에 대한 설명입니다.|  
  
배열 값은 숫자 키 0, 1 및 2를 사용하여 액세스할 수도 있습니다. 오류나 경고가 발생하지 않는 경우 **null** 이 반환됩니다.  
  
## <a name="example"></a>예제  
다음 예제에서는 실패한 문을 실행하는 동안 발생하는 오류를 표시합니다. (때문에 문이 실패 **InvalidColumName** 지정된 된 테이블의 유효한 열 이름이 아닙니다.) 이 예에서는 가정 하는 SQL Server 및 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 데이터베이스가 로컬 컴퓨터에 설치 됩니다. 모든 출력은 명령줄에서 예제가 실행될 때 콘솔에 기록됩니다.  
  
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
  
/* Set up a query to select an invalid column name. */  
$tsql = "SELECT InvalidColumnName FROM Sales.SalesOrderDetail";  
  
/* Attempt execution. */  
/* Execution will fail because of the invalid column name. */  
$stmt = sqlsrv_query( $conn, $tsql);  
if( $stmt === false )  
{  
      if( ($errors = sqlsrv_errors() ) != null)  
      {  
         foreach( $errors as $error)  
         {  
            echo "SQLSTATE: ".$error[ 'SQLSTATE']."\n";  
            echo "code: ".$error[ 'code']."\n";  
            echo "message: ".$error[ 'message']."\n";  
         }  
      }  
}  
  
/* Free connection resources */  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>관련 항목:  
[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)

[설명서의 코드 예제 정보](../../connect/php/about-code-examples-in-the-documentation.md)  
  
