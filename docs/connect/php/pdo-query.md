---
title: 'Pdo:: query | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f6f5e6d4-8ca9-4f06-89ed-de65ad3952a2
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c945bb5ab0a14b1c93b0c7f4fb16a72cd258bb14
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37979747"
---
# <a name="pdoquery"></a>PDO::query
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

SQL 쿼리를 실행하고 결과 집합을 PDOStatement 개체로 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
PDOStatement PDO::query ($statement[, $fetch_style);  
```  
  
#### <a name="parameters"></a>매개 변수  
*$statement*: 실행하려는 SQL 문입니다.  
  
*$fetch_style*: 쿼리를 수행하는 방법에 대한 선택적 지침입니다. 자세한 내용은 설명 섹션을 참조하세요.PDO::query의 $ $*fetch_style*은 PDO::fetch의 $*fetch_style*로 재정의할 수 있습니다.  
  
## <a name="return-value"></a>반환 값  
호출이 성공하면 PDO::query에서 PDOStatement 개체를 반환합니다. 호출이 실패하면 PDO::ATTR_ERRMODE의 설정에 따라 PDO::query에서 PDOException 개체를 발생시키거나 false를 반환합니다.  
  
## <a name="exceptions"></a>예외  
PDOException입니다.  
  
## <a name="remarks"></a>Remarks  
PDO::query를 사용하여 실행하는 쿼리는 PDO::SQLSRV_ATTR_DIRECT_QUERY의 설정에 따라 준비된 문을 실행하거나 직접 실행할 수 있습니다. 자세한 내용은 [Direct Statement Execution and Prepared Statement Execution in the PDO_SQLSRV Driver](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md)(PDO_SQLSRV 드라이버에서 직접 문 실행 및 준비된 문 실행)를 참조하세요.  
  
PDO::SQLSRV_ATTR_QUERY_TIMEOUT은 또한 PDO::exec의 동작에 영향을 줍니다. 자세한 내용은 [PDO::setAttribute](../../connect/php/pdo-setattribute.md)를 참조하세요.  
  
$*fetch_style*에 대해 다음 옵션을 지정할 수 있습니다.  
  
|style|설명|  
|---------|---------------|  
|PDO::FETCH_COLUMN, *num*|지정된 열의 데이터에 대한 쿼리입니다. 테이블의 첫 번째 열은 0입니다.|  
|PDO::FETCH_CLASS, '*classname*', array( *arglist* )|클래스의 인스턴스를 만들고 열 이름을 클래스의 속성에 할당합니다. 클래스 생성자가 하나 이상의 매개 변수를 사용하는 경우 *arglist*를 전달할 수도 있습니다.|  
|Fetch_class, '*classname*'|열 이름을 기존 클래스의 속성에 할당합니다.|  
  
PDO::query를 다시 호출하기 전에 PDOStatement::closeCursor를 호출하여 PDOStatement 개체와 연결된 데이터베이스 리소스를 해제합니다.  
  
null로 설정하면 PDOStatement 개체를 닫을 수 있습니다.  
  
결과 집합의 모든 데이터를 페치하지 않으면 다음 PDO::query 호출이 실패하지 않습니다.  
  
PDO 지원이 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 버전 2.0에 추가되었습니다.  
  
## <a name="example"></a>예제  
이 예제에서는 여러 개의 쿼리를 보여 줍니다.  
  
```  
<?php  
$database = "AdventureWorks";  
$conn = new PDO( "sqlsrv:server=(local) ; Database = $database", "", "");  
$conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );  
$conn->setAttribute( PDO::SQLSRV_ATTR_QUERY_TIMEOUT, 1 );  
  
$query = 'select * from Person.ContactType';  
  
// simple query  
$stmt = $conn->query( $query );  
while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){  
   print_r( $row['Name'] ."\n" );  
}  
  
echo "\n........ query for a column ............\n";  
  
// query for one column  
$stmt = $conn->query( $query, PDO::FETCH_COLUMN, 1 );  
while ( $row = $stmt->fetch() ){  
   echo "$row\n";  
}  
  
echo "\n........ query with a new class ............\n";  
$query = 'select * from HumanResources.Department order by GroupName';  
// query with a class  
class cc {  
   function __construct( $arg ) {  
      echo "$arg";  
   }  
  
   function __toString() {  
      return $this->DepartmentID . "; " . $this->Name . "; " . $this->GroupName;  
   }  
}  
  
$stmt = $conn->query( $query, PDO::FETCH_CLASS, 'cc', array( "arg1 " ));  
  
while ( $row = $stmt->fetch() ){  
   echo "$row\n";  
}  
  
echo "\n........ query into an existing class ............\n";  
$c_obj = new cc( '' );  
$stmt = $conn->query( $query, PDO::FETCH_INTO, $c_obj );  
while ( $stmt->fetch() ){  
   echo "$c_obj\n";  
}  
  
$stmt = null;  
?>  
```  
  
## <a name="see-also"></a>참고 항목  
[PDO 클래스](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
