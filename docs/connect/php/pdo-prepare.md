---
title: 'Pdo:: prepare | Microsoft Docs'
ms.custom: 
ms.date: 07/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a8b16fdc-c748-49be-acf2-a6ac7432d16b
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7a83fabca6866e8e3b106d8696ef03514a93aa62
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="pdoprepare"></a>PDO::prepare
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

실행할 문을 준비합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
PDOStatement PDO::prepare ( $statement [, array(key_pair)] )  
```  
  
#### <a name="parameters"></a>매개 변수  
$*statement*: SQL 문이 포함된 문자열입니다.  
  
*key_pair*: 특성 이름 및 값을 포함 하는 배열입니다. 자세한 내용은 주의 섹션을 참조하십시오.  
  
## <a name="return-value"></a>반환 값  
성공하면 PDOStatement 개체를 반환합니다. 실패하면 PDOException 개체를 반환하거나 PDO::ATTR_ERRMODE 값에 따라 false를 반환합니다.  
  
## <a name="remarks"></a>주의  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 는 실행 때까지 준비된 문을 평가하지 않습니다.  
  
다음 표에서 가능한 *key_pair* 값입니다.  
  
|Key|Description|  
|-------|---------------|  
|PDO::ATTR_CURSOR|커서 동작을 지정합니다. 기본값은 PDO::CURSOR_FWDONLY입니다. PDO::CURSOR_SCROLL은 정적 커서입니다.<br /><br />`array( PDO::ATTR_CURSOR => PDO::CURSOR_FWDONLY )`)을 입력합니다.<br /><br />PDO::CURSOR_SCROLL을 사용하는 경우 PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE을 사용할 수 있으며 아래 설명되어 있습니다.<br /><br />참조 [커서 유형 &#40; PDO_SQLSRV 드라이버 &#41; ](../../connect/php/cursor-types-pdo-sqlsrv-driver.md) 결과 집합 및 커서 PDO_SQLSRV 드라이버에 대 한 자세한 내용은 합니다.|  
|PDO::ATTR_EMULATE_PREPARES|Pdo:: ATTR_EMULATE_PREPARES에 때 자리 표시자에 준비 된 문에 바인딩된 매개 변수도 바뀝니다. 자리 표시 자가 포함 전체 SQL 문 실행 시 데이터베이스에 다음 전송 됩니다. <br /><br />Pdo:: ATTR_EMULATE_PREPARES SQL Server의 몇 가지 제한 사항을 무시 데 사용할 수 있습니다. 예를 들어 SQL Server 일부 Transact SQL 절에서 명명 된 또는 위치 매개 변수를 지원 하지 않습니다. 또한 SQL Server의 한 제한은 바인딩 2100 개의 매개 변수입니다.<br /><br />Pdo:: ATTR_EMULATE_PREPARES 특성을 true로 설정할 수 있습니다. 예를 들어<br /><br />`PDO::ATTR_EMULATE_PREPARES => true`<br /><br />기본적으로 이 특성은 false로 설정됩니다.<br /><br />**참고:** `PDO::ATTR_EMULATE_PREPARES => true`를 사용하는 경우 매개 변수가 있는 쿼리의 보안이 적용되지 않습니다. 응용 프로그램은 매개 변수에 바인딩되는 데이터에 악성 Transact SQL 코드 없는지 확인 해야 합니다.<br /><br />**제한 사항:**: input_output 및 출력 매개 변수는 매개 변수는 데이터베이스 매개 변수가 있는 쿼리 기능을 사용 하 여 바인딩되지 않은 때문에 지원 되지 않습니다.|  
|PDO::SQLSRV_ATTR_ENCODING|PDO::SQLSRV_ENCODING_UTF8(기본값)<br /><br />PDO::SQLSRV_ENCODING_SYSTEM<br /><br />PDO::SQLSRV_ENCODING_BINARY|  
|PDO::SQLSRV_ATTR_DIRECT_QUERY|True이면 직접 쿼리 실행을 지정합니다. False는 준비된 문을 실행합니다. Pdo:: SQLSRV_ATTR_DIRECT_QUERY에 대 한 자세한 내용은 참조 [직접 문 실행 및 준비 된 문 실행 PDO_SQLSRV 드라이버에서](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md)합니다.|  
|PDO::SQLSRV_ATTR_QUERY_TIMEOUT|자세한 내용은 [PDO::setAttribute](../../connect/php/pdo-setattribute.md)을 참조하세요.|  
  
PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL을 사용하는 경우 PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE을 사용할 수 있습니다. 예:  
  
```  
array(PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL, PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE => PDO::SQLSRV_CURSOR_DYNAMIC));  
```  
  
다음 표는 PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE에 대한 가능한 값을 보여 줍니다.  
  
|값|Description|  
|---------|---------------|  
|PDO::SQLSRV_CURSOR_BUFFERED|클라이언트 쪽(버퍼됨) 정적 커서를 만듭니다. 클라이언트 쪽 커서에 대 한 자세한 내용은 참조 [커서 유형 &#40; PDO_SQLSRV 드라이버 &#41; ](../../connect/php/cursor-types-pdo-sqlsrv-driver.md).|  
|PDO::SQLSRV_CURSOR_DYNAMIC|서버 쪽(버퍼되지 않음) 동적 커서를 만들고 이를 통해 순서에 관계없이 행에 액세스할 수 있으며 데이터베이스에 변경 내용이 반영됩니다.|  
|PDO::SQLSRV_CURSOR_KEYSET_DRIVEN|서버 쪽 키 집합 커서를 만듭니다. 행이 테이블에서 삭제되는 경우 키 집합 커서가 행 개수를 업데이트하지 않습니다(삭제된 행은 값 없이 반환됨).|  
|PDO::SQLSRV_CURSOR_STATIC|서버 쪽 정적 커서를 만들고 이를 통해 순서에 관계없이 행에 액세스할 수 있지만 데이터베이스에 변경 내용은 반영되지 않습니다.<br /><br />PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL은 PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE => PDO::SQLSRV_CURSOR_STATIC을 암시합니다.|  
  
null로 설정하면 PDOStatement 개체를 닫을 수 있습니다.  
  
## <a name="example"></a>예제  
이 예제에서는 매개 변수 표식 및 정방향 전용 커서를 사용하는 PDO::prepare 메서드를 사용하는 방법을 보여 줍니다.  
  
```  
<?php  
$database = "Test";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$col1 = 'a';  
$col2 = 'b';  
  
$query = "insert into Table1(col1, col2) values(?, ?)";  
$stmt = $conn->prepare( $query, array( PDO::ATTR_CURSOR => PDO::CURSOR_FWDONLY, PDO::SQLSRV_ATTR_QUERY_TIMEOUT => 1  ) );  
$stmt->execute( array( $col1, $col2 ) );  
print $stmt->rowCount();  
echo "\n";  
  
$query = "insert into Table1(col1, col2) values(:col1, :col2)";  
$stmt = $conn->prepare( $query, array( PDO::ATTR_CURSOR => PDO::CURSOR_FWDONLY, PDO::SQLSRV_ATTR_QUERY_TIMEOUT => 1  ) );  
$stmt->execute( array( ':col1' => $col1, ':col2' => $col2 ) );  
print $stmt->rowCount();  
  
$stmt = null  
?>  
```  
  
## <a name="example"></a>예제  
이 예제에서는 클라이언트 쪽 커서를 사용하는 PDO::prepare 메서드를 사용하는 방법을 보여 줍니다. 서버 쪽 커서를 보여 주는 샘플을 보려면 [커서 유형 &#40; PDO_SQLSRV 드라이버 &#41; ](../../connect/php/cursor-types-pdo-sqlsrv-driver.md).  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$query = "select * from Person.ContactType";  
$stmt = $conn->prepare( $query, array(PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL));  
$stmt->execute();  
  
echo "\n";  
  
while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){  
   print "$row[Name]\n";  
}  
echo "\n..\n";  
  
$row = $stmt->fetch( PDO::FETCH_BOTH, PDO::FETCH_ORI_FIRST );  
print_r($row);  
  
$row = $stmt->fetch( PDO::FETCH_ASSOC, PDO::FETCH_ORI_REL, 1 );  
print "$row[Name]\n";  
  
$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_NEXT );  
print "$row[1]\n";  
  
$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_PRIOR );  
print "$row[1]..\n";  
  
$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_ABS, 0 );  
print_r($row);  
  
$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_LAST );  
print_r($row);  
?>  
```  
  
## <a name="see-also"></a>관련 항목:  
[PDO 클래스](../../connect/php/pdo-class.md)  
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  

