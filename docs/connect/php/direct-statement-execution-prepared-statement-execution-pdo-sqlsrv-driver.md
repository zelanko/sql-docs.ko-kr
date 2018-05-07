---
title: 직접 문 실행 PDO_SQLSRV 드라이버를 준비 된 문-| Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 05544ca6-1e07-486c-bf03-e8c2c25b3024
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f3a11f37c3e82506f5eea48a02bc1997c5de2c8b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="direct-statement-execution-and-prepared-statement-execution-in-the-pdosqlsrv-driver"></a>PDO_SQLSRV 드라이버에서 직접 문 실행 및 준비된 문 실행
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

이 항목에서는 기본값 (준비 된 문 실행) 대신 직접 문 실행을 지정 하는 pdo:: SQLSRV_ATTR_DIRECT_QUERY 특성의 사용을 설명 합니다. 준비 된 문을 사용 하 여 두 번 이상 매개 변수 바인딩을 사용 하 여 문이 실행 되는 경우 성능이 향상 될 수 있습니다.  
  
## <a name="remarks"></a>주의  
전송 하려는 경우는 [!INCLUDE[tsql](../../includes/tsql_md.md)] 드라이버에서 문 준비 하지 않고 서버에 직접 문, pdo:: SQLSRV_ATTR_DIRECT_QUERY 특성을 설정할 수 있습니다 [pdo:: setattribute](../../connect/php/pdo-setattribute.md) (또는에 전달 된 드라이버 옵션 [:: __Construct](../../connect/php/pdo-construct.md)) 호출 하는 경우 또는 [pdo:: prepare](../../connect/php/pdo-prepare.md)합니다. 기본적으로 pdo:: SQLSRV_ATTR_DIRECT_QUERY의 값이 False (사용 하 여 준비 된 문을 실행) 합니다.  
  
사용 하는 경우 [pdo:: query](../../connect/php/pdo-query.md), 직접 실행을 할 수 있습니다. 호출 하기 전에 [pdo:: query](../../connect/php/pdo-query.md), 호출 [pdo:: setattribute](../../connect/php/pdo-setattribute.md) pdo:: SQLSRV_ATTR_DIRECT_QUERY를 True로 설정 합니다.  호출할 때마다 [pdo:: query](../../connect/php/pdo-query.md) pdo:: SQLSRV_ATTR_DIRECT_QUERY에 대 한 다른 설정을 사용 하 여 실행할 수 있습니다.  
  
사용 하는 경우 [pdo:: prepare](../../connect/php/pdo-prepare.md) 및 [pdostatement:: Execute](../../connect/php/pdostatement-execute.md) 반복 된 쿼리의 실행을 최적화 준비 된 문을 실행 하는 바인딩된 매개 변수를 사용 하 여 쿼리를 여러 번 실행 하 합니다.  이 경우 호출 [pdo:: prepare](../../connect/php/pdo-prepare.md) 드라이버 옵션 배열 매개 변수에서 False로 설정 하는 pdo:: SQLSRV_ATTR_DIRECT_QUERY를 사용 합니다. 필요한 경우에 False로 pdo:: SQLSRV_ATTR_DIRECT_QUERY 설정 된 준비 된 문을 실행할 수 있습니다.  
  
호출한 후 [pdo:: prepare](../../connect/php/pdo-prepare.md), pdo:: SQLSRV_ATTR_DIRECT_QUERY의 값은 준비 된 쿼리를 실행할 때 변경할 수 없습니다.  
  
쿼리에 이전 쿼리에서에 설정 된 컨텍스트를이 필요한 경우에 True로 pdo:: SQLSRV_ATTR_DIRECT_QUERY 설정 된 쿼리를 실행 합니다. 예를 들어 쿼리에서 임시 테이블을 사용 하는 경우 pdo:: SQLSRV_ATTR_DIRECT_QUERY True로 설정 되어야 합니다.  
  
다음 샘플은 이전 문에서 컨텍스트 필요할 때 할 경우 pdo:: SQLSRV_ATTR_DIRECT_QUERY를 True로 설정 합니다.  이 샘플에서는 직접 쿼리를 실행 하는 경우만 프로그램의 이후 문이를 사용할 수 있는 임시 테이블을 사용 합니다.  
  
```  
<?php  
   $conn = new PDO('sqlsrv:Server=(local)', '', '');  
   $conn->setAttribute(constant('PDO::SQLSRV_ATTR_DIRECT_QUERY'), true);  
  
   $stmt1 = $conn->query("DROP TABLE #php_test_table");  
  
   $stmt2 = $conn->query("CREATE TABLE #php_test_table ([c1_int] int, [c2_int] int)");  
  
   $v1 = 1;  
   $v2 = 2;  
  
   $stmt3 = $conn->prepare("INSERT INTO #php_test_table (c1_int, c2_int) VALUES (:var1, :var2)");  
  
   if ($stmt3) {  
      $stmt3->bindValue(1, $v1);  
      $stmt3->bindValue(2, $v2);  
  
      if ($stmt3->execute())  
         echo "Execution succeeded\n";       
      else  
         echo "Execution failed\n";  
   }  
   else  
      var_dump($conn->errorInfo());  
  
   $stmt4 = $conn->query("DROP TABLE #php_test_table");  
?>  
```  
  
## <a name="see-also"></a>관련 항목:  
[SQL Server 용 PHP 용 Microsoft 드라이버에 대 한 가이드를 프로그래밍](../../connect/php/programming-guide-for-php-sql-driver.md)
  
