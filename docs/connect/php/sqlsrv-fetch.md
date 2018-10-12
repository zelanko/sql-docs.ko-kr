---
title: sqlsrv_fetch | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_fetch
apitype: NA
helpviewer_keywords:
- sqlsrv_fetch
- API Reference, sqlsrv_fetch
- retrieving data, as a single field
ms.assetid: a5a640a1-6e7d-452e-8b66-850a4dc2ce89
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b03669df3fdfadec0f06f5bd964a16827d1aff2e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47604235"
---
# <a name="sqlsrvfetch"></a>sqlsrv_fetch
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

결과 집합의 다음 행을 읽기에 사용할 수 있습니다. [sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md)를 사용하여 행의 필드를 읽습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
sqlsrv_fetch( resource $stmt[, row[, ]offset])  
```  
  
#### <a name="parameters"></a>매개 변수  
*$stmt*: 실행된 문에 해당하는 문 리소스입니다.  
  
> [!NOTE]  
> 결과를 검색하려면 문이 실행되어야 합니다. 문 실행에 대한 자세한 내용은 [sqlsrv_query](../../connect/php/sqlsrv-query.md) 및 [sqlsrv_execute](../../connect/php/sqlsrv-execute.md)를 참조하세요.  
  
*row* [선택 사항]: 다음 값 중 하나로, 스크롤 가능 커서를 사용하는 결과 집합에서 액세스할 행을 지정합니다.  
  
-   SQLSRV_SCROLL_NEXT  
  
-   SQLSRV_SCROLL_PRIOR  
  
-   SQLSRV_SCROLL_FIRST  
  
-   SQLSRV_SCROLL_LAST  
  
-   SQLSRV_SCROLL_ABSOLUTE  
  
-   SQLSRV_SCROLL_RELATIVE  
  
이러한 값에 대한 자세한 내용은 [커서 유형 지정 및 행 선택](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)을 참조하세요.  
  
*offset* [선택 사항]: 검색할 행을 지정하는 데 SQLSRV_SCROLL_ABSOLUTE 및 SQLSRV_SCROLL_RELATIVE와 함께 사용됩니다. 결과 집합의 첫 번째 레코드는 0입니다.  
  
## <a name="return-value"></a>반환 값  
결과 집합의 다음 행을 성공적으로 검색하면 **true** 가 반환됩니다. 결과 집합에 더 이상 결과가 없으면 **null** 이 반환됩니다. 오류가 발생한 경우 **false** 가 반환됩니다.  
  
## <a name="example"></a>예제  
다음 예제에서는 **sqlsrv_fetch** 를 사용하여 제품 검토 및 검토자 이름이 포함된 데이터 행을 검색합니다. 결과 집합에서 데이터를 검색하려면 [sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md)가 사용됩니다. 이 예제에서는 SQL Server 및 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 데이터베이스가 로컬 컴퓨터에 설치된 것으로 가정합니다. 모든 출력은 명령줄에서 예제가 실행될 때 콘솔에 기록됩니다.  
  
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
Comments are of SQL Server type nvarchar. */  
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
if( sqlsrv_fetch( $stmt ) === false)  
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
while( !feof( $stream ))  
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
[데이터 검색](../../connect/php/retrieving-data.md)  

[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)  

[설명서의 코드 예제 정보](../../connect/php/about-code-examples-in-the-documentation.md)  
  
