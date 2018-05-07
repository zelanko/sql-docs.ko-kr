---
title: 'Pdo:: begintransaction | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4d5db438-9df7-4d22-9907-3ddc63bd2220
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3e4ad9df1db56719e683a3047f19a9f1842df9f3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="pdobegintransaction"></a>PDO::beginTransaction
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

자동 커밋 모드를 끄고 트랜잭션을 시작합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
bool PDO::beginTransaction();  
```  
  
## <a name="return-value"></a>반환 값  
메서드 호출에 성공하면 true이고, 그렇지 않으면 false입니다.  
  
## <a name="remarks"></a>주의  
Pdo:: begintransaction으로 시작한 트랜잭션은 하면 끝납니다 [pdo:: commit](../../connect/php/pdo-commit.md) 또는 [pdo:: rollback](../../connect/php/pdo-rollback.md) 호출 됩니다.  
  
PDO::beginTransaction은 PDO::ATTR_AUTOCOMMIT 값에 의해 영향을 받지도 않고 영향을 주지도 않습니다.  
  
이전 PDO::beginTransaction이 PDO::rollback 또는 PDO::commit으로 종료되기 전에는 PDO::beginTransaction을 호출할 수 없습니다.  
  
이 방법이 실패 하면 연결을 자동 커밋 모드로 반환 합니다.  
  
PDO 지원이 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 버전 2.0에 추가되었습니다.  
  
## <a name="example"></a>예제  
다음 예제는 Test라는 데이터베이스와 Table1이라는 테이블을 사용합니다. 트랜잭션을 시작하고 두 행을 추가한 다음 한 행을 삭제하는 명령을 실행합니다. 명령이 데이터베이스에 전송되고 트랜잭션이 `PDO::commit`으로 명시적으로 종료됩니다.  
  
```  
<?php  
   $conn = new PDO( "sqlsrv:server=(local); Database = Test", "", "");  
   $conn->beginTransaction();  
   $ret = $conn->exec("insert into Table1(col1, col2) values('a', 'b') ");  
   $ret = $conn->exec("insert into Table1(col1, col2) values('a', 'c') ");  
   $ret = $conn->exec("delete from Table1 where col1 = 'a' and col2 = 'b'");  
   $conn->commit();  
   // $conn->rollback();  
   echo $ret;  
?>  
```  
  
## <a name="see-also"></a>관련 항목:  
[PDO 클래스](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
