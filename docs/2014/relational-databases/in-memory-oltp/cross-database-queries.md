---
title: 데이터베이스 간 쿼리 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: a0305f5b-91bd-4d18-a2fc-ec235b062fd3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0ccf8ea4fc15be567d0e95a66b2e5320fae7dbbc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48205163"
---
# <a name="cross-database-queries"></a>데이터베이스 간 쿼리
  [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]에서 메모리 최적화 테이블은 데이터베이스 간 트랜잭션을 지원하지 않습니다. 메모리 최적화 테이블에도 액세스하는 동일한 쿼리 또는 동일한 트랜잭션에서 다른 데이터베이스에 액세스할 수 없습니다. 데이터베이스의 테이블에서 다른 데이터베이스에 있는 메모리 최적화 테이블로 데이터를 쉽게 복사할 수 없습니다.  
  
 테이블 변수는 트랜잭션 변수가 아닙니다. 메모리 최적화 테이블 변수는 데이터베이스 간 쿼리에 사용할 수 있으므로, 데이터베이스의 데이터를 다른 데이터베이스에 있는 메모리 최적화 테이블로 쉽게 이동할 수 있습니다. 두 트랜잭션을 사용할 수 있습니다. 첫 번째 트랜잭션에서 원격 테이블의 데이터를 변수에 삽입합니다. 두 번째 트랜잭션에서 변수의 데이터를 메모리 최적화 로컬 테이블에 삽입합니다.  
  
 예를 들어 행을 복사 하려면 데이터베이스 db1의 t1 테이블에서에서 db2의 t2 테이블로에 변수를 사용 하 여 @v1 dbo.tt1 형식의 @ 같이 사용할 수 있습니다.  
  
```tsql  
USE db2   
GO   
DECLARE @v1 dbo.tt1   
INSERT @v1 SELECT * FROM db1.dbo.t1   
INSERT dbo.t2 SELECT * FROM @v1   
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [메모리 내 OLTP로 마이그레이션](migrating-to-in-memory-oltp.md)  
  
  
