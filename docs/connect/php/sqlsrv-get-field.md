---
title: sqlsrv_get_field | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_get_field
apitype: NA
helpviewer_keywords:
- sqlsrv_get_field
- API Reference, sqlsrv_get_field
- retrieving data, as a single field
ms.assetid: fa17cc56-fb38-433b-a40d-65642f04dc23
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 64ddca64f049ba95426dec542d68dc8a84e7d9dc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015016"
---
# <a name="sqlsrvgetfield"></a>sqlsrv_get_field
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

현재 행의 지정된 필드에서 데이터를 검색합니다. 필드 데이터는 순서대로 액세스해야 합니다. 예를 들어 두 번째 필드의 데이터에 액세스한 후 첫 번째 필드의 데이터에 액세스할 수 없습니다.  
  
## <a name="syntax"></a>구문  
  
```  
sqlsrv_get_field( resource $stmt, int $fieldIndex [, int $getAsType])  
```  
  
#### <a name="parameters"></a>매개 변수  
*$stmt*: 실행된 문에 해당하는 문 리소스입니다.  
  
*$fieldIndex*: 검색할 필드의 인덱스입니다. 인덱스는 0부터 시작합니다.  
  
*$getAsType* [선택 사항]: 반환된 데이터에 대해 PHP 데이터 형식을 결정하는 **SQLSRV** 상수(**SQLSRV_PHPTYPE_&#x2a;** )입니다. 지원되는 데이터 형식에 대한 자세한 내용은 [상수&#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)를 참조하세요. 반환 형식이 지정되지 않은 경우 기본 PHP 형식이 반환됩니다. 기본 PHP 형식에 대한 자세한 내용은 [Default PHP Data Types](../../connect/php/default-php-data-types.md)을 참조하세요. PHP 데이터 형식을 지정하는 방법에 대한 자세한 내용은 [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md)을 참조하세요.  
  
## <a name="return-value"></a>반환 값  
필드 데이터입니다. *$getAsType* 매개 변수를 사용하여 반환된 데이터의 PHP 데이터 형식을 지정할 수 있습니다. 반환 데이터 형식이 지정되지 않은 경우 기본 PHP 데이터 형식이 반환됩니다. 기본 PHP 형식에 대한 자세한 내용은 [Default PHP Data Types](../../connect/php/default-php-data-types.md)을 참조하세요. PHP 데이터 형식을 지정하는 방법에 대한 자세한 내용은 [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md)을 참조하세요.  
  
## <a name="remarks"></a>Remarks  
**sqlsrv_fetch** 및 **sqlsrv_get_field**의 조합은 데이터에 대한 정방향 전용 액세스를 제공합니다.  
  
**sqlsrv_fetch**/**sqlsrv_get_field** 조합은 결과 집합 행의 하나의 필드만 스크립트 메모리에 로드하고 PHP 반환 형식 사양을 허용합니다. (PHP 반환 형식을 지정하는 방법에 대한 자세한 내용은 [방법: PHP 데이터 형식 지정](../../connect/php/how-to-specify-php-data-types.md)을 참조하세요.) 이 함수 조합에서는 또한 데이터를 스트림으로 검색할 수 있습니다. (스트림으로 데이터를 검색하는 방법에 대한 자세한 내용은 [SQLSRV 드라이버를 사용하여 스트림으로 데이터 검색](../../connect/php/retrieving-data-as-a-stream-using-the-sqlsrv-driver.md)을 참조하세요.)  
  
## <a name="example"></a>예제  
다음 예제에서는 제품 검토 및 의견을 제출한 검토자의 이름이 포함된 데이터 행을 검색합니다. 결과 집합에서 데이터를 검색하려면 **sqlsrv_get_field** 가 사용됩니다. 이 예제에서는 SQL Server 및 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 데이터베이스가 로컬 컴퓨터에 설치된 것으로 가정합니다. 모든 출력은 명령줄에서 예제가 실행될 때 콘솔에 기록됩니다.  
  
```  
<?php  
/*Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Set up and execute the query. Note that both ReviewerName and  
Comments are of the SQL Server nvarchar type. */  
$tsql = "SELECT ReviewerName, Comments   
         FROM Production.ProductReview  
         WHERE ProductReviewID=1";  
$stmt = sqlsrv_query( $conn, $tsql);  
if( $stmt === false )  
{  
     echo "Error in statement preparation/execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Make the first row of the result set available for reading. */  
if( sqlsrv_fetch( $stmt ) === false )  
{  
     echo "Error in retrieving row.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Note: Fields must be accessed in order.  
Get the first field of the row. Note that no return type is  
specified. Data will be returned as a string, the default for  
a field of type nvarchar.*/  
$name = sqlsrv_get_field( $stmt, 0);  
echo "$name: ";  
  
/*Get the second field of the row as a stream.  
Because the default return type for a nvarchar field is a  
string, the return type must be specified as a stream. */  
$stream = sqlsrv_get_field( $stmt, 1,   
                            SQLSRV_PHPTYPE_STREAM( SQLSRV_ENC_CHAR));  
while( !feof( $stream))  
{   
    $str = fread( $stream, 10000);  
    echo $str;  
}  
  
/* Free the statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>참고 항목  
[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)  

[데이터 검색](../../connect/php/retrieving-data.md)  

[설명서의 코드 예제 정보](../../connect/php/about-code-examples-in-the-documentation.md)  
  
