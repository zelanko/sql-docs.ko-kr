---
title: sqlsrv_fetch_array | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_fetch_array
apitype: NA
helpviewer_keywords:
- sqlsrv_fetch_array
- retrieving data, as an array
- API Reference, sqlsrv_fetch_array
ms.assetid: 69270b9e-0791-42f4-856d-412da39dea63
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e983d3c9a0989a5aae79c074ba7b77b09528af6f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47662691"
---
# <a name="sqlsrvfetcharray"></a>sqlsrv_fetch_array
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

데이터의 다음 행을 숫자로 인덱싱된 배열, 결합형 배열 또는 둘 다로 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
sqlsrv_fetch_array( resource $stmt[, int $fetchType [, row[, ]offset]])  
```  
  
#### <a name="parameters"></a>매개 변수  
*$stmt*: 실행된 문에 해당하는 문 리소스입니다.  
  
*$fetchType* [선택 사항]: 미리 정의된 상수입니다. 이 매개 변수는 다음 표에 나열된 값 중 하나를 사용할 수 있습니다.  
  
|값|설명|  
|---------|---------------|  
|SQLSRV_FETCH_NUMERIC|데이터의 다음 행이 숫자형 배열로 반환됩니다.|  
|SQLSRV_FETCH_ASSOC|데이터의 다음 행이 결합형 배열로 반환됩니다. 배열 키는 결과 집합의 열 이름입니다.|  
|SQLSRV_FETCH_BOTH|데이터의 다음 행이 숫자형 배열과 결합형 배열 둘 다로 반환됩니다. 이것은 기본값입니다.|  
  
*row* [선택 사항]: 버전 1.1에서 추가되었습니다. 다음 값 중 하나로 스크롤 가능 커서를 사용하는 결과 집합에서 액세스할 행을 지정합니다. (*row*가 지정된 경우 기본값을 지정하는 경우에도 *fetchtype*이 명시적으로 지정되어야 합니다.)  
  
-   SQLSRV_SCROLL_NEXT  
-   SQLSRV_SCROLL_PRIOR  
-   SQLSRV_SCROLL_FIRST  
-   SQLSRV_SCROLL_LAST  
-   SQLSRV_SCROLL_ABSOLUTE  
-   SQLSRV_SCROLL_RELATIVE  
  
이러한 값에 대한 자세한 내용은 [커서 유형 지정 및 행 선택](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)을 참조하세요. 스크롤 가능 커서 지원이 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 버전 1.1에 추가되었습니다.  
  
*offset* [선택 사항]: 검색할 행을 지정하는 데 SQLSRV_SCROLL_ABSOLUTE 및 SQLSRV_SCROLL_RELATIVE와 함께 사용됩니다. 결과 집합의 첫 번째 레코드는 0입니다.  
  
## <a name="return-value"></a>반환 값  
데이터 행이 검색되는 경우 **배열** 이 반환됩니다. 검색할 행이 더 이상 없는 경우 **null** 이 반환됩니다. 오류가 발생하면 **false** 가 반환됩니다.  
  
*$fetchType* 매개 변수의 값을 기반으로, 반환된 **배열** 은 숫자로 인덱싱된 **배열**, 결합형 **배열**또는 둘 다일 수 있습니다. 기본적으로 숫자 키와 결합형 키가 둘 다 있는 **배열** 이 반환됩니다. 반환된 배열에 있는 값의 데이터 형식은 기본 PHP 데이터 형식입니다. 기본 PHP 데이터 형식에 대한 자세한 내용은 [Default PHP Data Types](../../connect/php/default-php-data-types.md)을 참조하세요.  
  
## <a name="remarks"></a>Remarks  
이름이 없는 열이 반환되면 배열 요소에 대한 결합형 키는 빈 문자열("")입니다. 예를 들어 값을 데이터베이스 테이블에 삽입하고 서버 생성 기본 키를 검색하는 다음 Transact-SQL 문을 고려해 보겠습니다.  
  
```
INSERT INTO Production.ProductPhoto (LargePhoto) VALUES (?);  
SELECT SCOPE_IDENTITY()
```
  
이 명령문의 `SELECT SCOPE_IDENTITY()` 부분에서 반환된 결과 집합이 결합형 배열로 검색되는 경우 반환된 열에 이름이 없기 때문에 반환된 값에 대한 키는 빈 문자열("")입니다. 이를 방지하려면 결과를 숫자형 배열로 검색하거나 Transact-SQL 문에서 반환된 열에 대한 이름을 지정할 수 있습니다. 다음은 Transact-SQL에 열 이름을 지정하는 한 가지 방법입니다.  
  
```
SELECT SCOPE_IDENTITY() AS PictureID
```
  
결과 집합에 이름이 없는 여러 열이 포함된 경우 마지막으로 이름이 지정되지 않은 열의 값이 빈 문자열("") 키에 할당됩니다.  
  
## <a name="example"></a>예제  
다음 예제는 결과 집합의 각 행을 결합형 **배열**로 검색합니다. 이 예제에서는 SQL Server 및 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 데이터베이스가 로컬 컴퓨터에 설치된 것으로 가정합니다. 모든 출력은 명령줄에서 예제가 실행될 때 콘솔에 기록됩니다.  
  
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
  
/* Set up and execute the query. */  
$tsql = "SELECT FirstName, LastName  
         FROM Person.Contact  
         WHERE LastName='Alan'";  
$stmt = sqlsrv_query( $conn, $tsql);  
if( $stmt === false)  
{  
     echo "Error in query preparation/execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve each row as an associative array and display the results.*/  
while( $row = sqlsrv_fetch_array( $stmt, SQLSRV_FETCH_ASSOC))  
{  
      echo $row['LastName'].", ".$row['FirstName']."\n";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a>예제  
다음 예제는 결과 집합의 각 행을 숫자로 인덱싱된 배열로 검색합니다.  
  
예제에서는 AdventureWorks 데이터베이스의 *Purchasing.PurchaseOrderDetail* 테이블에서 지정된 날짜 및 지정된 값보다 재고량(*StockQty*)이 작은 제품에 대해 제품 정보를 검색합니다.  
  
이 예제에서는 SQL Server 및 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 데이터베이스가 로컬 컴퓨터에 설치된 것으로 가정합니다. 모든 출력은 명령줄에서 예제가 실행될 때 콘솔에 기록됩니다.  
  
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
  
/* Define the query. */  
$tsql = "SELECT ProductID,  
                UnitPrice,  
                StockedQty   
         FROM Purchasing.PurchaseOrderDetail  
         WHERE StockedQty < 3   
         AND DueDate='2002-01-29'";  
  
/* Execute the query. */  
$stmt = sqlsrv_query( $conn, $tsql);  
if ( $stmt )  
{  
     echo "Statement executed.\n";  
}   
else   
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Iterate through the result set printing a row of data upon each  
iteration.*/  
while( $row = sqlsrv_fetch_array( $stmt, SQLSRV_FETCH_NUMERIC))  
{  
     echo "ProdID: ".$row[0]."\n";  
     echo "UnitPrice: ".$row[1]."\n";  
     echo "StockedQty: ".$row[2]."\n";  
     echo "-----------------\n";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
**sqlsrv_fetch_array** 함수는 항상 [기본 PHP 데이터 형식](../../connect/php/default-php-data-types.md)에 따라 데이터를 반환합니다. PHP 데이터 형식을 지정하는 방법에 대한 자세한 내용은 [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md)을 참조하세요.  
  
이름이 없는 필드가 검색되는 경우 배열 요소에 대한 결합형 키는 빈 문자열("")입니다. 자세한 내용은 [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)

[데이터 검색](../../connect/php/retrieving-data.md)

[설명서의 코드 예제 정보](../../connect/php/about-code-examples-in-the-documentation.md)

[SQL Server 용 PHP 용 Microsoft 드라이버에 대 한 가이드를 프로그래밍](../../connect/php/programming-guide-for-php-sql-driver.md)
  
