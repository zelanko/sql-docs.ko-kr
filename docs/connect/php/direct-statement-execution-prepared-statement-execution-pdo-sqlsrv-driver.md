---
title: 직접 문 실행 PDO_SQLSRV 드라이버를 준비 된 문을 | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
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
ms.openlocfilehash: 9a054717a1d8249e842611b2e07f49631f376049
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38042222"
---
# <a name="direct-statement-execution-and-prepared-statement-execution-in-the-pdosqlsrv-driver"></a>PDO_SQLSRV 드라이버에서 직접 문 실행 및 준비된 문 실행
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

이 항목에서는 PDO::SQLSRV_ATTR_DIRECT_QUERY 특성을 사용하여 기본값(준비된 명령문 실행) 대신 직접 명령문 실행을 지정하는 방법을 설명합니다. 준비 된 문을 사용 하 여 문을 한 번만 매개 변수 바인딩을 사용 하 여 실행 되는 경우 성능이 향상 될 수 있습니다.  
  
## <a name="remarks"></a>Remarks  
전송 하려는 경우는 [!INCLUDE[tsql](../../includes/tsql_md.md)] 드라이버에서 문 준비 하지 않고 서버에 직접 문을 사용 하 여 pdo:: SQLSRV_ATTR_DIRECT_QUERY 특성을 설정할 수 있습니다 [pdo:: setattribute](../../connect/php/pdo-setattribute.md) (드라이버 옵션에 전달 되는 또는 [Pdo:: __construct](../../connect/php/pdo-construct.md)) 호출 하는 경우 나 [pdo:: prepare](../../connect/php/pdo-prepare.md)합니다. 기본적으로 pdo:: SQLSRV_ATTR_DIRECT_QUERY의 값이 False (사용 하 여 준비 된 문을 실행) 합니다.  
  
사용 하는 경우 [pdo:: query](../../connect/php/pdo-query.md), 직접 실행 되지 않는 것이 좋습니다. 호출 하기 전에 [pdo:: query](../../connect/php/pdo-query.md)를 호출 [pdo:: setattribute](../../connect/php/pdo-setattribute.md) pdo:: SQLSRV_ATTR_DIRECT_QUERY를 True로 설정 합니다.  호출할 때마다 [pdo:: query](../../connect/php/pdo-query.md) pdo:: SQLSRV_ATTR_DIRECT_QUERY에 대 한 다른 설정을 사용 하 여 실행할 수 있습니다.  
  
사용 하는 경우 [pdo:: prepare](../../connect/php/pdo-prepare.md) 하 고 [pdostatement:: Execute](../../connect/php/pdostatement-execute.md) 준비 된 문을 실행 하는 바인딩된 매개 변수를 사용 하 여 쿼리를 여러 번 실행 하는 반복된 쿼리를 실행 최적화 합니다.  이 이런 경우에 호출할 [pdo:: prepare](../../connect/php/pdo-prepare.md) 드라이버 옵션 배열 매개 변수에 False로 설정 하는 pdo:: SQLSRV_ATTR_DIRECT_QUERY를 사용 하 여 합니다. 필요한 경우에 False로 설정 된 pdo:: SQLSRV_ATTR_DIRECT_QUERY 사용 하 여 준비 된 문을 실행할 수 있습니다.  
  
호출한 후 [pdo:: prepare](../../connect/php/pdo-prepare.md), 준비 된 쿼리를 실행 하는 경우 pdo:: SQLSRV_ATTR_DIRECT_QUERY의 값을 변경할 수 없습니다.  
  
쿼리는 쿼리를 이전에 설정 된 컨텍스트가 필요를 True로 설정 된 pdo:: SQLSRV_ATTR_DIRECT_QUERY 사용 하 여 쿼리를 실행 합니다. 예를 들어 쿼리에서 임시 테이블을 사용 하는 경우 pdo:: SQLSRV_ATTR_DIRECT_QUERY True로 설정 되어야 합니다.  
  
다음 샘플에서는 이전 문에서 상황에 맞는 필요한 경우 할 경우 pdo:: SQLSRV_ATTR_DIRECT_QUERY을 True로 설정 합니다.  이 샘플에만 사용할 수 있는 프로그램의 후속 문의 쿼리를 직접 실행 하면 임시 테이블을 사용 합니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
[SQL Server 용 PHP 용 Microsoft 드라이버에 대 한 가이드를 프로그래밍](../../connect/php/programming-guide-for-php-sql-driver.md)
  
