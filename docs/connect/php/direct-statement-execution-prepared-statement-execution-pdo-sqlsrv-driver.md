---
title: 직접 문 준비 된 문 실행 PDO_SQLSRV 드라이버 | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993623"
---
# <a name="direct-statement-execution-and-prepared-statement-execution-in-the-pdosqlsrv-driver"></a>PDO_SQLSRV 드라이버에서 직접 문 실행 및 준비된 문 실행
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

이 항목에서는 PDO::SQLSRV_ATTR_DIRECT_QUERY 특성을 사용하여 기본값(준비된 명령문 실행) 대신 직접 명령문 실행을 지정하는 방법을 설명합니다. 문이 매개 변수 바인딩을 사용 하 여 두 번 이상 실행 되는 경우 준비 된 문을 사용 하면 성능이 향상 될 수 있습니다.  
  
## <a name="remarks"></a>Remarks  
드라이버를 사용 하 여 문을 [!INCLUDE[tsql](../../includes/tsql-md.md)] 준비 하지 않고 서버에 직접 문을 보내려면 pdo:: [setAttribute](../../connect/php/pdo-setattribute.md) 를 사용 하 여 pdo:: SQLSRV_ATTR_DIRECT_QUERY 특성을 설정 하거나 [pdo:: __construct](../../connect/php/pdo-construct.md)에 전달 된 드라이버 옵션으로 설정할 수 있습니다.) 또는 [PDO::p repare](../../connect/php/pdo-prepare.md)를 호출 하는 경우. 기본적으로 PDO:: SQLSRV_ATTR_DIRECT_QUERY의 값은 False (준비 된 문 실행 사용)입니다.  
  
[PDO:: query](../../connect/php/pdo-query.md)를 사용 하는 경우 직접 실행 해야 할 수 있습니다. Pdo: [: query](../../connect/php/pdo-query.md)를 호출 하기 전에 [Pdo](../../connect/php/pdo-setattribute.md) :: setAttribute를 호출 하 고 pdo:: SQLSRV_ATTR_DIRECT_QUERY를 True로 설정 합니다.  Pdo: [: query](../../connect/php/pdo-query.md) 에 대 한 각 호출은 pdo:: SQLSRV_ATTR_DIRECT_QUERY에 대해 다른 설정을 사용 하 여 실행할 수 있습니다.  
  
[PDO::p repare](../../connect/php/pdo-prepare.md) 및 [PDOStatement:: execute](../../connect/php/pdostatement-execute.md) 를 사용 하 여 바인딩된 매개 변수를 사용 하 여 쿼리를 여러 번 실행 하는 경우 준비 된 문 실행은 반복 되는 쿼리의 실행을 최적화 합니다.  이 경우 pdo:: SQLSRV_ATTR_DIRECT_QUERY를 사용 하 여 pdo: [:p repare](../../connect/php/pdo-prepare.md) 를 호출 합니다. 필요한 경우 PDO:: SQLSRV_ATTR_DIRECT_QUERY을 False로 설정 하 여 준비 된 문을 실행할 수 있습니다.  
  
[Pdo::p repare](../../connect/php/pdo-prepare.md)를 호출 하면 준비 된 쿼리를 실행할 때 pdo:: SQLSRV_ATTR_DIRECT_QUERY의 값이 변경 되지 않습니다.  
  
쿼리에 이전 쿼리에 설정 된 컨텍스트가 필요한 경우 PDO:: SQLSRV_ATTR_DIRECT_QUERY를 True로 설정 하 여 쿼리를 실행 합니다. 예를 들어 쿼리에서 임시 테이블을 사용 하는 경우 PDO:: SQLSRV_ATTR_DIRECT_QUERY를 True로 설정 해야 합니다.  
  
다음 샘플에서는 이전 문의 컨텍스트가 필요한 경우 PDO:: SQLSRV_ATTR_DIRECT_QUERY를 True로 설정 해야 함을 보여 줍니다. 이 샘플에서는 쿼리가 직접 실행 될 때 프로그램의 이후 문에서만 사용할 수 있는 임시 테이블을 사용 합니다.  
  
> [!NOTE]
> 쿼리가 저장 프로시저를 호출 하 고이 저장 프로시저에서 임시 테이블을 사용 하는 경우 [PDO:: exec](../../connect/php/pdo-exec.md) 를 대신 사용 합니다.

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
[Microsoft Drivers for PHP for SQL Server 프로그래밍 가이드](../../connect/php/programming-guide-for-php-sql-driver.md)
  
