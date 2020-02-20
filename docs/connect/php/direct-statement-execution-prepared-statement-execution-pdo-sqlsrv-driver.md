---
title: 직접 문 - 준비된 문 실행 PDO_SQLSRV 드라이버 | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 05544ca6-1e07-486c-bf03-e8c2c25b3024
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fa9e544fb7b79009d86a5742946a722d5adc18f2
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67993623"
---
# <a name="direct-statement-execution-and-prepared-statement-execution-in-the-pdo_sqlsrv-driver"></a>PDO_SQLSRV 드라이버에서 직접 문 실행 및 준비된 문 실행
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

이 항목에서는 PDO::SQLSRV_ATTR_DIRECT_QUERY 특성을 사용하여 기본값(준비된 명령문 실행) 대신 직접 명령문 실행을 지정하는 방법을 설명합니다. 문이 매개 변수 바인딩을 사용하여 두 번 이상 실행되는 경우 준비된 문을 사용하면 성능이 향상될 수 있습니다.  
  
## <a name="remarks"></a>설명  
드라이버를 사용하여 문을 준비하지 않고 서버에 직접 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 보내려면 [PDO::setAttribute](../../connect/php/pdo-setattribute.md)에서(또는 [PDO::__construct](../../connect/php/pdo-construct.md)로 전달되는 드라이버 옵션으로) 또는 [PDO::prepare](../../connect/php/pdo-prepare.md)를 호출할 때 PDO::SQLSRV_ATTR_DIRECT_QUERY 특성을 설정합니다. 기본적으로 PDO::SQLSRV_ATTR_DIRECT_QUERY의 값은 False(준비된 문 실행 사용)입니다.  
  
[PDO::query](../../connect/php/pdo-query.md)를 사용하는 경우 직접 실행해야 할 수 있습니다. [PDO::query](../../connect/php/pdo-query.md)를 호출하기 전에 [PDO::setAttribute](../../connect/php/pdo-setattribute.md)를 호출하고 PDO::SQLSRV_ATTR_DIRECT_QUERY를 True로 설정합니다.  [PDO::query](../../connect/php/pdo-query.md)를 호출할 때마다 PDO::SQLSRV_ATTR_DIRECT_QUERY를 다르게 설정하여 실행할 수 있습니다.  
  
[PDO::prepare](../../connect/php/pdo-prepare.md) 및 [PDOStatement::execute](../../connect/php/pdostatement-execute.md)를 사용하여 바인딩된 매개 변수로 쿼리를 여러 번 실행하는 경우 준비된 문 실행은 반복되는 쿼리의 실행을 최적화합니다.  이 경우 드라이버 옵션 배열 매개 변수에서 False로 설정된 PDO::SQLSRV_ATTR_DIRECT_QUERY를 사용하여 [PDO::prepare](../../connect/php/pdo-prepare.md)를 호출합니다. 필요한 경우 PDO::SQLSRV_ATTR_DIRECT_QUERY를 False로 설정하여 준비된 문을 실행할 수 있습니다.  
  
[PDO::prepare](../../connect/php/pdo-prepare.md)를 호출한 후 준비된 쿼리를 실행할 때 PDO::SQLSRV_ATTR_DIRECT_QUERY 값을 변경할 수 없습니다.  
  
쿼리에 이전 쿼리에서 설정한 컨텍스트가 필요한 경우 PDO::SQLSRV_ATTR_DIRECT_QUERY를 True로 설정하여 쿼리를 실행합니다. 예를 들어 쿼리에서 임시 테이블을 사용하는 경우 PDO::SQLSRV_ATTR_DIRECT_QUERY를 True로 설정해야 합니다.  
  
다음 샘플에서는 이전 문의 컨텍스트가 필요한 경우 PDO::SQLSRV_ATTR_DIRECT_QUERY를 True로 설정해야 함을 보여 줍니다. 이 샘플에서는 쿼리가 직접 실행될 때 프로그램에서 후속 문에만 사용할 수 있는 임시 테이블을 사용합니다.  
  
> [!NOTE]
> 쿼리가 저장 프로시저를 호출하고 이 저장 프로시저에서 임시 테이블을 사용하는 경우 [PDO::exec](../../connect/php/pdo-exec.md)를 대신 사용합니다.

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
[Microsoft Drivers for PHP for SQL Server 프로그래밍 가이드 | Microsoft Docs](../../connect/php/programming-guide-for-php-sql-driver.md)
  
