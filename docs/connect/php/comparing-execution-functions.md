---
title: 함수 실행 비교
description: 이 항목에는 Microsoft Drivers for PHP for SQL Server를 사용하는 경우의 다양한 쿼리 실행 함수가 나열되어 있습니다.
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- executing queries
ms.assetid: 130fc0fd-87dd-46b2-918f-de9dc572c769
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 33d7ebe420dd59d4f659dbe2ce6c784b49b89d04
ms.sourcegitcommit: d1051f05a7db81ec62d9785bb6af572408f3d4e0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88680748"
---
# <a name="comparing-execution-functions"></a>함수 실행 비교
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 는 함수를 실행하기 위한 몇 가지 옵션을 제공합니다.  

## <a name="sqlsrv-execution-functions"></a>SQLSRV 실행 함수  
SQLSRV 드라이버를 사용하는 경우 단일 쿼리를 실행하려면 [sqlsrv_query](../../connect/php/sqlsrv-query.md) 를 사용하고 각 실행에 대해 다른 매개 변수 값으로 준비된 문을 여러 번 실행하려면 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) 와 [sqlsrv_execute](../../connect/php/sqlsrv-execute.md) 를 사용합니다.  

## <a name="pdo_sqlsrv-execution-functions"></a>PDO_SQLSRV 실행 함수 
PDO_SQLSRV 드라이버를 사용하는 경우에 다음 중 하나를 사용하여 쿼리를 실행할 수 있습니다.  
  
-   [PDO::exec](../../connect/php/pdo-exec.md)  
  
-   [PDO::query](../../connect/php/pdo-query.md)  
  
-   [PDO::prepare](../../connect/php/pdo-prepare.md) 및 [PDOStatement::execute](../../connect/php/pdostatement-execute.md).  
  
## <a name="see-also"></a>참고 항목  
[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)

[PDO_SQLSRV 드라이버 참조](../../connect/php/pdo-sqlsrv-driver-reference.md)

[Microsoft Drivers for PHP for SQL Server 프로그래밍 가이드 | Microsoft Docs](../../connect/php/programming-guide-for-php-sql-driver.md)
  
