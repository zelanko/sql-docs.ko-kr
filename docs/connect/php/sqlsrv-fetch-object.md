---
title: sqlsrv_fetch_object | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- sqlsrv_fetch_object
apitype: NA
helpviewer_keywords:
- sqlsrv_fetch_object
- API Reference, sqlsrv_fetch_object
- retrieving data, as an object
ms.assetid: 4ce2df2c-083a-4a4d-a1e2-e866e63707d5
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d77c725535cec8846d864fd4e85113d99892cda7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsrvfetchobject"></a>sqlsrv_fetch_object
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

PHP 개체로 데이터의 다음 행을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
sqlsrv_fetch_object( resource $stmt [, string $className [, array $ctorParams[, row[, ]offset]]])  
```  
  
#### <a name="parameters"></a>매개 변수  
*$stmt*: 실행된 문에 해당하는 문 리소스입니다.  
  
*$className* [선택 사항]: 인스턴스화할 클래스의 이름을 지정 하는 문자열입니다. *$className* 매개 변수의 값이 지정되지 않은 경우 PHP **stdClass** 의 인스턴스가 인스턴스화됩니다.  
  
*$ctorParams* [선택 사항]: 지정 된 클래스의 생성자에 전달 된 값을 포함 하는 배열에서 *$className* 매개 변수입니다. 지정된 클래스의 생성자가 매개 변수 값을 허용하는 경우 *$ctorParams* object **sqlsrv_fetch_object**매개 변수를 사용해야 합니다.  
  
*행* [선택 사항]: 스크롤 가능 커서를 사용 하는 결과 집합에서 액세스할 행을 지정 하는 다음 값 중 하나입니다. (경우 *행* 지정 된 *$className* 및 *$ctorParams* 명시적으로 지정 해야에 대 한 null을 지정 해야 하는 경우에 *$className*및 *$ctorParams*.)  
  
-   SQLSRV_SCROLL_NEXT  
  
-   SQLSRV_SCROLL_PRIOR  
  
-   SQLSRV_SCROLL_FIRST  
  
-   SQLSRV_SCROLL_LAST  
  
-   SQLSRV_SCROLL_ABSOLUTE  
  
-   SQLSRV_SCROLL_RELATIVE  
  
이러한 값에 대한 자세한 내용은 [커서 유형 지정 및 행 선택](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)을 참조하세요.  
  
*오프셋* [선택 사항]: 검색할 행을 지정 하려면 데 SQLSRV_SCROLL_ABSOLUTE 및 SQLSRV_SCROLL_RELATIVE 함께 사용 합니다. 결과 집합의 첫 번째 레코드는 0입니다.  
  
## <a name="return-value"></a>반환 값  
결과 집합 필드 이름에 해당하는 속성을 가진 PHP 개체입니다. 속성 값은 해당 결과 집합 필드 값으로 채워집니다. 선택적 *$className* 매개 변수로 지정된 클래스가 존재하지 않거나 지정된 문과 연결된 활성 결과 집합이 없는 경우 **false** 가 반환됩니다. 검색할 행이 더 이상 없는 경우 **null** 이 반환됩니다.  
  
반환된 개체의 값 데이터 형식이 기본 PHP 데이터 형식이 됩니다. 기본 PHP 데이터 형식에 대한 자세한 내용은 [Default PHP Data Types](../../connect/php/default-php-data-types.md)을 참조하세요.  
  
## <a name="remarks"></a>주의  
클래스 이름이 선택적 *$className* 매개 변수로 지정된 경우 이 클래스 형식의 개체가 인스턴스화됩니다. 클래스에 이름이 결과 집합의 필드 이름과 일치하는 속성이 있는 경우 해당 결과 집합 값이 속성에 적용됩니다. 결과 집합 필드 이름이 클래스 속성과 일치하지 않는 경우 결과 집합 필드 이름을 사용하는 속성이 개체에 추가되고 결과 집합 값이 속성에 적용됩니다.  
  
다음 규칙은 *$className* 매개 변수로 클래스를 지정할 때 적용됩니다.  
  
-   일치는 대/소문자를 구분합니다. 예를 들어 속성 이름 CustomerId가 필드 이름 CustomerID와 일치하지 않습니다. 이 경우 CustomerID 속성이 개체에 추가되고 CustomerID 필드의 값이 CustomerID 속성에 지정됩니다.  
  
-   액세스 한정자에 관계없이 일치가 발생합니다. 예를 들어 지정된 클래스에 그 이름이 결과 집합 필드 이름과 일치하는 개인 속성이 있는 경우 결과 집합 필드의 값이 속성에 적용됩니다.  
  
-   클래스 속성 데이터 형식은 무시됩니다. 결과 집합의 "CustomerID" 필드가 문자열이지만 클래스의 "CustomerID" 속성이 정수인 경우 결과 집합의 문자열 값이 "CustomerID" 속성에 기록됩니다.  
  
-   지정된 클래스가 존재하지 않는 경우 함수가 **false** 를 반환하고 오류 수집에 오류를 추가합니다. 오류 정보 검색에 대한 자세한 내용은 [sqlsrv_errors](../../connect/php/sqlsrv-errors.md)를 참조하세요.  
  
이름이 없는 필드가 반환되면 **sqlsrv_fetch_object** 가 필드 값을 삭제하고 경고를 발생시킵니다. 예를 들어 값을 데이터베이스 테이블에 삽입하고 서버 생성 기본 키를 검색하는 다음 Transact-SQL 문을 고려해 보겠습니다.  
  
<pre>INSERT INTO Production.ProductPhoto (LargePhoto) VALUES (?);  
SELECT SCOPE_IDENTITY()</pre>  
  
이 쿼리에서 반환된 결과가 **sqlsrv_fetch_object**로 검색되는 경우 `SELECT SCOPE_IDENTITY()` 에서 반환된 값이 삭제되고 경고가 발생합니다. 이를 방지하려면 Transact-SQL 문에서 반환된 필드에 대해 이름을 지정하면 됩니다. 다음은 Transact-SQL에 열 이름을 지정하는 한 가지 방법입니다.  
  
`SELECT SCOPE_IDENTITY() AS PictureID`  
  
## <a name="example"></a>예제  
다음 예제는 결과 집합의 각 행을 PHP 개체로 검색합니다. 이 예에서는 가정 하는 SQL Server 및 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 데이터베이스가 로컬 컴퓨터에 설치 된 합니다. 모든 출력은 명령줄에서 예제가 실행될 때 콘솔에 기록됩니다.  
  
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
if( $stmt === false )  
{  
     echo "Error in query preparation/execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve each row as a PHP object and display the results.*/  
while( $obj = sqlsrv_fetch_object( $stmt))  
{  
      echo $obj->LastName.", ".$obj->FirstName."\n";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a>예제  
다음 예제는 결과 집합의 각 행을 스크립트에서 정의된 *Product* 클래스의 인스턴스로 검색합니다. 제품 정보를 검색 하는 예제는 *Purchasing.PurchaseOrderDetail* 및 *Production.Product* 지정 된 제품에 대 한 AdventureWorks 데이터베이스의 테이블 (기한 *DueDate*), 및 재고량 (*StockQty*) 지정된 된 값 보다 작아야 합니다. 예제에서는 **sqlsrv_fetch_object**에 대한 호출에서 클래스를 지정할 때 적용하는 일부 규칙을 강조합니다.  
  
-   *$product* 변수는 *Product* 클래스의 인스턴스입니다. 그 이유는 "제품"이 *$className* 매개 변수로 지정되었고 *Product* 클래스가 존재하기 때문입니다.  
  
-   기존 *name* 속성이 일치하지 않기 때문에 *Name* 속성이 *$product* 인스턴스에 추가됩니다.  
  
-   일치하는 속성이 없기 때문에 *Color* 속성이 *$product* 인스턴스에 추가됩니다.  
  
-   개인 속성 *UnitPrice* 는 *UnitPrice* 필드 값으로 채워집니다.  
  
이 예에서는 가정 하는 SQL Server 및 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 데이터베이스가 로컬 컴퓨터에 설치 됩니다. 모든 출력은 명령줄에서 예제가 실행될 때 콘솔에 기록됩니다.  
  
```  
<?php  
/* Define the Product class. */  
class Product  
{  
     /* Constructor */  
     public function Product($ID)  
     {  
          $this->objID = $ID;  
     }  
     public $objID;  
     public $name;  
     public $StockedQty;  
     public $SafetyStockLevel;  
     private $UnitPrice;  
     function getPrice()  
     {  
          return $this->UnitPrice;  
     }  
}  
  
/* Connect to the local server using Windows Authentication, and  
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
$tsql = "SELECT Name,  
                SafetyStockLevel,  
                StockedQty,  
                UnitPrice,  
                Color  
         FROM Purchasing.PurchaseOrderDetail AS pdo  
         JOIN Production.Product AS p  
         ON pdo.ProductID = p.ProductID  
         WHERE pdo.StockedQty < ?  
         AND pdo.DueDate= ?";  
  
/* Set the parameter values. */  
$params = array(3, '2002-01-29');  
  
/* Execute the query. */  
$stmt = sqlsrv_query( $conn, $tsql, $params);  
if ( $stmt )  
{  
     echo "Statement executed.\n";  
}   
else   
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Iterate through the result set, printing a row of data upon each  
 iteration. Note the following:  
     1) $product is an instance of the Product class.  
     2) The $ctorParams parameter is required in the call to  
        sqlsrv_fetch_object, because the Product class constructor is  
        explicity defined and requires parameter values.  
     3) The "Name" property is added to the $product instance because  
        the existing "name" property does not match.  
     4) The "Color" property is added to the $product instance  
        because there is no matching property.  
     5) The private property "UnitPrice" is populated with the value  
        of the "UnitPrice" field.*/  
$i=0; //Used as the $objID in the Product class constructor.  
while( $product = sqlsrv_fetch_object( $stmt, "Product", array($i)))  
{  
     echo "Object ID: ".$product->objID."\n";  
     echo "Product Name: ".$product->Name."\n";  
     echo "Stocked Qty: ".$product->StockedQty."\n";  
     echo "Safety Stock Level: ".$product->SafetyStockLevel."\n";  
     echo "Product Color: ".$product->Color."\n";  
     echo "Unit Price: ".$product->getPrice()."\n";  
     echo "-----------------\n";  
     $i++;  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
기존 **sqlsrv_fetch_object** 함수는 항상 [Default PHP Data Types](../../connect/php/default-php-data-types.md)매개 변수를 사용해야 합니다. PHP 데이터 형식을 지정하는 방법에 대한 자세한 내용은 [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md)을 참조하세요.  
  
이름이 없는 필드가 반환되면 **sqlsrv_fetch_object** 가 필드 값을 삭제하고 경고를 발생시킵니다. 예를 들어 값을 데이터베이스 테이블에 삽입하고 서버 생성 기본 키를 검색하는 다음 Transact-SQL 문을 고려해 보겠습니다.  
  
<pre>INSERT INTO Production.ProductPhoto (LargePhoto) VALUES (?);  
SELECT SCOPE_IDENTITY()</pre>  
  
이 쿼리에서 반환된 결과가 **sqlsrv_fetch_object**로 검색되는 경우 `SELECT SCOPE_IDENTITY()` 에서 반환된 값이 삭제되고 경고가 발생합니다. 이를 방지하려면 Transact-SQL 문에서 반환된 필드에 대해 이름을 지정하면 됩니다. 다음은 Transact-SQL에 열 이름을 지정하는 한 가지 방법입니다.  
  
`SELECT SCOPE_IDENTITY() AS PictureID`  
  
## <a name="see-also"></a>관련 항목:  
[데이터 검색](../../connect/php/retrieving-data.md)  

[설명서의 코드 예제 정보](../../connect/php/about-code-examples-in-the-documentation.md)  

[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)  
  
