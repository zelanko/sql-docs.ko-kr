---
title: PDO::beginTransaction
description: Microsoft PDO_SQLSRV Driver for PHP for SQL Server의 PDO::beginTransaction 함수에 대한 API 참조입니다.
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4d5db438-9df7-4d22-9907-3ddc63bd2220
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ed3a4ed3e1dd4642f5456423e6266bb2a327c330
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88646213"
---
# <a name="pdobegintransaction"></a>PDO::beginTransaction
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

자동 커밋 모드를 끄고 트랜잭션을 시작합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
bool PDO::beginTransaction();  
```  
  
## <a name="return-value"></a>Return Value  
메서드 호출에 성공하면 true이고, 그렇지 않으면 false입니다.  
  
## <a name="remarks"></a>설명  
PDO::beginTransaction으로 시작한 트랜잭션은 [PDO::commit](../../connect/php/pdo-commit.md) 또는 [PDO::rollback](../../connect/php/pdo-rollback.md) 이 호출될 때 종료됩니다.  
  
PDO::beginTransaction은 PDO::ATTR_AUTOCOMMIT 값에 의해 영향을 받지도 않고 영향을 주지도 않습니다.  
  
이전 PDO::beginTransaction이 PDO::rollback 또는 PDO::commit으로 종료되기 전에는 PDO::beginTransaction을 호출할 수 없습니다.  
  
이 메서드가 실패하면 연결이 자동 커밋 모드로 돌아갑니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
[PDO 클래스](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
