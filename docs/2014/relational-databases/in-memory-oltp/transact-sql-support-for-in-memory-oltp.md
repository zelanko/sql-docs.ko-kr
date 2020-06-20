---
title: 메모리 내 OLTP에 대한 Transact-SQL 지원 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: b1cc7c30-1747-4c21-88ac-e95a5e58baac
author: rothja
ms.author: jroth
ms.openlocfilehash: bf3708a258e3bb97231e45b10bea2c59351a06a2
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85025493"
---
# <a name="transact-sql-support-for-in-memory-oltp"></a>메모리 내 OLTP에 대한 Transact-SQL 지원
  Transact-SQL 쿼리 또는 DML 문(SELECT, INSERT, UPDATE 또는 DELETE), 임시 문과, 저장 프로시저, 테이블 반환 함수, 스칼라 함수, 트리거, 뷰와 같은 SQL 모듈을 사용하여 메모리 최적화 테이블에 액세스할 수 있습니다. 자세한 내용은 해석 된 [transact-sql을 사용 하 여 메모리 액세스에 최적화 된 테이블에 액세스](accessing-memory-optimized-tables-using-interpreted-transact-sql.md)를 참조 하세요.  
  
 메모리 최적화 테이블만 참조하는 저장 프로시저는 기계어 코드에 고유하게 컴파일될 수 있으며, 일반적으로 해석되는 (디스크 기반) 저장 프로시저에서 상당한 성능 향상을 제공합니다. 메모리 최적화 테이블에 최적으로 액세스하려면 고유하게 컴파일된 저장 프로시저를 사용합니다. 자세한 내용은 [고유하게 컴파일된 저장 프로시저](natively-compiled-stored-procedures.md)를 참조하세요.  
  
 데이터베이스 개체(DDL 문)를 만들고 수정할 때 다음 문이 수정되었습니다.  
  
-   [ALTER Database 파일 및 파일 그룹 옵션 transact-sql&#41;&#40;](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options) (참조 `MEMORY_OPTIMIZED_DATA` )  
  
-   [Transact-sql&#41;SQL SERVER 데이터베이스 &#40;만들기](/sql/t-sql/statements/create-database-sql-server-transact-sql) (참조 `MEMORY_OPTIMIZED_DATA` )  
  
-   [Transact-sql&#41;&#40;프로시저 만들기](/sql/t-sql/statements/create-procedure-transact-sql) (,, `NATIVE_COMPILATION` 및 참조 `SCHEMABINDING` `EXECUTE AS` `BEGIN ATOMIC` )  
  
-   [Transact-sql&#41;&#40;CREATE TABLE](/sql/t-sql/statements/create-table-transact-sql) (,,, `MEMORY_OPTIMIZED` `DURABILITY` 및 참조 `BUCKET_COUNT` `INDEX` `HASH` )  
  
-   [Transact-sql&#41;형식 &#40;만듭니다](/sql/t-sql/statements/create-type-transact-sql) (,, `MEMORY_OPTIMIZED` 및 참조 `BUCKET_COUNT` `INDEX` `HASH` ).  
  
-   [ @local_variable Transact-sql&#41;&#40;선언](/sql/t-sql/language-elements/declare-local-variable-transact-sql) (참조 `NULL`  |  `NOT NULL` )  
  
 메모리 액세스에 최적화된 테이블은 `PRIMARY KEY` 및 `NOT NULL` 제약 조건을 지원합니다. 지원 되지 않는 제약 조건 구현에 대 한 자세한 내용은 [Check 및 Foreign Key 제약 조건 마이그레이션](../../database-engine/migrating-check-and-foreign-key-constraints.md)을 참조 하세요.  
  
 지원되지 않는 기능에 대한 자세한 내용은 [메모리 내 OLTP에서 지원되지 않는 Transact-SQL 구문](transact-sql-constructs-not-supported-by-in-memory-oltp.md)을 참조하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [지원되는 데이터 형식](supported-data-types-for-in-memory-oltp.md)  
  
-   [해석된 Transact-SQL을 사용하여 메모리 액세스에 최적화된 테이블에 액세스](accessing-memory-optimized-tables-using-interpreted-transact-sql.md)  
  
-   [메모리 내 OLTP에 대한 시스템 보기, 저장 프로시저, DMV 및 대기 형식](../../database-engine/system-views-stored-procedures-dmvs-and-wait-types-for-in-memory-oltp.md)  
  
## <a name="see-also"></a>참고 항목  
 [메모리 내 OLTP는 메모리 내 최적화를 &#40;&#41;](in-memory-oltp-in-memory-optimization.md)   
 [고유 하 게 컴파일된 저장 프로시저의 마이그레이션 문제](migration-issues-for-natively-compiled-stored-procedures.md)   
 [지원 되는 SQL Server 기능](unsupported-sql-server-features-for-in-memory-oltp.md)   
 [Natively Compiled Stored Procedures](natively-compiled-stored-procedures.md)  
  
  
