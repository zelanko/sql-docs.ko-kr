---
title: PDOStatement::rowCount | Microsoft Docs
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
ms.assetid: 0569f26a-2376-4c20-8813-bd3c87d0ae9f
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2d81d8b06eefa893e6b286159465719f408fce7f
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="pdostatementrowcount"></a>PDOStatement::rowCount
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

최근 실행된 문에서 추가, 삭제 또는 변경된 행 수를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
int PDOStatement::rowCount ();  
```  
  
## <a name="return-value"></a>반환 값  
추가, 삭제 또는 변경된 행 수입니다.  
  
## <a name="remarks"></a>주의  
관련된 PDOStatement에서 실행된 마지막 SQL 문이 SELECT 문인 경우 PDO::CURSOR_FWDONLY 커서가 -1을 반환합니다. PDO::CURSOR_SCROLLABLE 커서는 결과 집합의 행 수를 반환합니다.  
  
PDO 지원이 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 버전 2.0에 추가되었습니다.  
  
## <a name="example"></a>예제  
이 예제에서는 rowCount의 두 가지 용도를 보여 줍니다. 첫 번째 용도는 테이블에 추가된 행 수를 반환합니다. 두 번째 용도는 스크롤 가능한 커서를 지정할 때 rowCount가 결과 집합에서 행 수를 반환할 수 있다는 것을 보여 줍니다.  
  
```  
<?php  
$database = "Test";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$col1 = 'a';  
$col2 = 'b';  
  
$query = "insert into Table2(col1, col2) values(?, ?)";  
$stmt = $conn->prepare( $query );  
$stmt->execute( array( $col1, $col2 ) );  
print $stmt->rowCount();  
  
echo "\n\n";  
  
$con = null;  
$database = "AdventureWorks";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$query = "select * from Person.ContactType";  
$stmt = $conn->prepare( $query, array(PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL));  
$stmt->execute();  
print $stmt->rowCount();  
?>  
```  
  
## <a name="see-also"></a>참고 항목  
[PDOStatement 클래스](../../connect/php/pdostatement-class.md)  
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  
