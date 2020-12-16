---
title: 트리거 마이그레이션 | Microsoft 문서
description: SQL Server 인스턴스에서 CREATE, ALTER, DROP, GRANT, DENY, REVOKE 또는 UPDATE STATISTICS에 대해 발생하는 DDL 트리거와 메모리 최적화 테이블에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: ad5385c5-5a50-40ca-a319-97d5606b8511
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4147c69de6eb360820ed7bd47c7ee7c8c867d52b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97465364"
---
# <a name="migrating-triggers"></a>트리거 마이그레이션
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  이 항목에서는 DDL 트리거와 메모리 최적화 테이블에 대해 설명합니다.  
  
 DML 트리거는 메모리 최적화 테이블에서 지원되지만 FOR | AFTER 트리거 이벤트로만 지원됩니다. 예제는 [FROM 또는 하위 쿼리를 사용하여 UPDATE 구현](../../relational-databases/in-memory-oltp/implementing-update-with-from-or-subqueries.md)을 참조하세요. 
  
 LOGON 트리거는 LOGON 이벤트에 대해 발생하도록 정의된 트리거입니다. LOGON 트리거는 메모리 최적화 테이블에 영향을 주지 않습니다.  
  
## <a name="ddl-triggers"></a>DDL 트리거  
 DDL 트리거는 이 트리거가 정의된 데이터베이스 또는 서버에서 CREATE, ALTER, DROP, GRANT, DENY, REVOKE, or UPDATE STATISTICS 문을 실행할 때 발생하도록 정의된 트리거입니다.  
  
 데이터베이스 또는 서버에 CREATE_TABLE 또는 이를 포함하는 이벤트 그룹에 정의된 DDL 트리거가 하나 이상 있으면 메모리 최적화 테이블을 만들 수 없습니다. 데이터베이스 또는 서버에 DROP_TABLE 또는 이를 포함하는 이벤트 그룹에 정의된 DDL 트리거가 하나 이상 있으면 메모리 최적화 테이블을 삭제할 수 없습니다.  
  
 CREATE_PROCEDURE, DROP_PROCEDURE 또는 이러한 이벤트를 포함하는 이벤트 그룹에 DDL 트리거나 하나 이상 있는 경우에는 고유하게 컴파일된 저장 프로시저를 만들 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [메모리 내 OLTP로 마이그레이션](./plan-your-adoption-of-in-memory-oltp-features-in-sql-server.md)  
  
