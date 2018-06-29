---
title: 메모리 내 OLTP에서 지원되지 않는 Transact-SQL 구문 | Microsoft 문서
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e3f8009c-319d-4d7b-8993-828e55ccde11
caps.latest.revision: 34
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: b0d852a4a0d104c815a76076661a3e3c56355d90
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36181350"
---
# <a name="transact-sql-constructs-not-supported-by-in-memory-oltp"></a>메모리 내 OLTP에서 지원되지 않는 Transact-SQL 구문
  메모리 액세스에 최적화된 테이블과 고유하게 컴파일된 저장 프로시저는 디스크 기반 테이블과 해석된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저에서 지원되는 전체 [!INCLUDE[tsql](../../includes/tsql-md.md)] 노출 영역을 지원하지 않습니다. 지원되지 않는 기능 중 하나를 사용하려고 하면 서버에서 오류가 반환됩니다.  
  
 오류 메시지 텍스트에는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 유형(예: 기능, 작업, 옵션)과 기능 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 키워드의 이름이 언급됩니다. 대부분의 지원되지 않는 기능은 지원되지 않는 기능을 나타내는 오류 메시지 텍스트와 함께 오류 10794를 반환합니다. 다음 표에서는 오류 메시지 텍스트에 나타날 수 있는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 기능 및 키워드와 오류를 해결하기 위한 수정 동작을 나열합니다.  
  
 메모리 최적화 테이블과 고유하게 컴파일된 저장 프로시저에서 지원되는 기능에 대한 자세한 내용은 다음을 참조하세요.  
  
-   [고유하게 컴파일된 저장 프로시저의 마이그레이션 문제](migration-issues-for-natively-compiled-stored-procedures.md)  
  
-   [메모리 내 OLTP에 대한 Transact-SQL 지원](transact-sql-support-for-in-memory-oltp.md)  
  
-   [지원되는 SQL Server 기능](unsupported-sql-server-features-for-in-memory-oltp.md)  
  
-   [고유하게 컴파일된 저장 프로시저](../in-memory-oltp/natively-compiled-stored-procedures.md)  
  
## <a name="databases-that-use-in-memory-oltp"></a>메모리 내 OLTP를 사용하는 데이터베이스  
 다음 표에는 메모리 내 OLTP 데이터베이스와 관련된 오류 메시지 텍스트에 나타날 수 있는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 기능 및 키워드가 나열되어 있습니다.  
  
|형식|속성|해결 방법|  
|----------|----------|----------------|  
|옵션|AUTO_CLOSE|데이터베이스 옵션 AUTO_CLOSE=ON은 MEMORY_OPTIMIZED_DATA 파일 그룹이 있는 데이터베이스에서 지원되지 않습니다.|  
|옵션|ATTACH_REBUILD_LOG|CREATE 데이터베이스 옵션 ATTACH_REBUILD_LOG는 MEMORY_OPTIMIZED_DATA 파일 그룹이 있는 데이터베이스에서 지원되지 않습니다.|  
|기능|DATABASE SNAPSHOT|데이터베이스 스냅숏 만들기는 MEMORY_OPTIMIZED_DATA 파일 그룹이 있는 데이터베이스에서 지원되지 않습니다.|  
|기능|sync_method 'database snapshot' 또는 'database snapshot character'를 사용한 복제|sync_method 'database snapshot' 또는 'database snapshot character'를 사용한 복제는 MEMORY_OPTIMIZED_DATA 파일 그룹이 있는 데이터베이스에서 지원되지 않습니다.|  
|기능|DBCC CHECKDB<br /><br /> DBCC CHECKTABLE|DBCC CHECKDB는 데이터베이스에서 메모리 최적화 테이블을 건너뜁니다.<br /><br /> 메모리 최적화 테이블에 대한 DBCC CHECKTABLE은 실패합니다.|  
  
## <a name="memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블  
 다음 표에서는 메모리 최적화 테이블과 관련된 오류의 메시지 텍스트에 나타날 수 있는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 기능 및 키워드와 오류를 해결하기 위한 수정 동작을 나열합니다.  
  
|형식|속성|해결 방법|  
|----------|----------|----------------|  
|기능|ON|파일 그룹이나 파티션 구성표에는 메모리 액세스에 최적화된 테이블을 배치할 수 없습니다. `CREATE TABLE` 문에서 ON 절을 제거합니다.|  
|데이터 형식|*데이터 형식 이름*|표시된 데이터 형식이 지원되지 않습니다. 지원되는 데이터 형식 중 하나로 형식을 바꿉니다. 자세한 내용은 참조 [지원 되는 데이터 유형](supported-data-types-for-in-memory-oltp.md)합니다.|  
|기능|계산 열|계산된 열은 메모리 최적화 테이블에서 지원되지 않습니다. 계산된 열을 제거는 `CREATE TABLE` 문.|  
|기능|복제|복제는 메모리 최적화 테이블에서 지원되지 않습니다.|  
|기능|FILESTREAM|FILESTREAM 저장소는 메모리 최적화 테이블의 열에 지원되지 않습니다. 제거는 `FILESTREAM` 열 정의에서 키워드입니다.|  
|기능|SPARSE|메모리 최적화 테이블의 열을 SPARSE로 정의할 수 없습니다. 제거는 `SPARSE` 열 정의에서 키워드입니다.|  
|기능|ROWGUIDCOL|ROWGUIDCOL 옵션은 메모리 최적화 테이블의 열에서 지원되지 않습니다. 제거는 `ROWGUIDCOL` 열 정의에서 키워드입니다.|  
|기능|FOREIGN KEY|FOREIGN KEY 제약 조건은 메모리 최적화 테이블에서 지원되지 않습니다. 테이블 정의에서 제약 조건을 제거합니다.<br /><br /> 제약 조건에 대 한 지원 부족을 완화 하는 방법에 대 한 정보를 참조 하십시오. [마이그레이션 확인 및 Foreign Key Constraints](../../database-engine/migrating-check-and-foreign-key-constraints.md)합니다.|  
|기능|CHECK|CHECK 제약 조건은 메모리 최적화 테이블에서 지원되지 않습니다. 테이블 정의에서 제약 조건을 제거합니다.<br /><br /> 제약 조건에 대 한 지원 부족을 완화 하는 방법에 대 한 정보를 참조 하십시오. [마이그레이션 확인 및 Foreign Key Constraints](../../database-engine/migrating-check-and-foreign-key-constraints.md)합니다.|  
|기능|UNIQUE|UNIQUE 제약 조건은 메모리 최적화 테이블에서 지원되지 않습니다. 테이블 정의에서 제약 조건을 제거합니다.<br /><br /> 제약 조건에 대 한 지원 부족을 완화 하는 방법에 대 한 정보를 참조 하십시오. [마이그레이션 확인 및 Foreign Key Constraints](../../database-engine/migrating-check-and-foreign-key-constraints.md)합니다.|  
|기능|COLUMNSTORE|COLUMNSTORE 인덱스는 메모리 최적화 테이블에서 지원되지 않습니다. 대신 NONCLUSTERED 또는 NONCLUSTERED HASH 인덱스를 지정합니다.|  
|기능|클러스터형 인덱스|비클러스터형 인덱스를 지정합니다. 기본 키 인덱스의 경우 `PRIMARY KEY NONCLUSTERED [HASH]`를 지정해야 합니다.|  
|기능|비 1252 코드 페이지|데이터 형식이 `char` 및 `varchar`인 메모리 최적화 테이블의 열은 코드 페이지 1252를 사용해야 합니다. (var)char 대신 n(var)char을 사용하거나 코드 페이지 1252의 데이터 정렬을 사용합니다(예: Latin1_General_BIN2). 자세한 내용은 [Collations and Code Pages](../../database-engine/collations-and-code-pages.md)를 참조하세요.|  
|기능|트랜잭션 내부 DDL|사용자 트랜잭션의 컨텍스트에서는 메모리 액세스에 최적화된 테이블과 고유하게 컴파일된 저장 프로시저를 만들거나 삭제할 수 없습니다. 트랜잭션을 시작하지 말고 CREATE 또는 DROP 문을 실행하기 전에 세션 설정 IMPLICIT_다TRANSACTIONS가 OFF인지 확인합니다.|  
|기능|DDL 트리거|해당 DLL 작업에 대한 서버 또는 데이터베이스 트리거가 있는 경우 메모리 액세스에 최적화된 테이블과 고유하게 컴파일된 저장 프로시저를 만들거나 삭제할 수 없습니다. CREATE/DROP TABLE 및 CREATE/DROP PROCEDURE에 대한 서버 및 데이터베이스 트리거를 제거합니다.|  
|기능|EVENT NOTIFICATION|해당 DLL 작업에 대한 서버 또는 데이터베이스 이벤트 알림이 있는 경우 메모리 액세스에 최적화된 테이블 및 고유하게 컴파일된 저장 프로시저를 만들거나 삭제할 수 없습니다. CREATE TABLE 또는 DROP TABLE과 CREATE PROCEDURE 또는 DROP PROCEDURE에 대한 서버 및 데이터베이스 이벤트 알림을 제거합니다.|  
|기능|FileTable|메모리 액세스에 최적화된 테이블을 파일 테이블로 만들 수 없습니다. `AS FileTable` 문에서 `CREATE TABLE` 인수를 제거합니다.|  
|연산|기본 키 열의 업데이트|메모리 최적화 테이블의 기본 키 열과 테이블 형식을 업데이트할 수 없습니다. 기본 키를 업데이트해야 하는 경우 기존 열을 삭제하고 업데이트된 기본 키가 있는 새 열을 삽입합니다.|  
|연산|CREATE  INDEX|`CREATE TABLE` 문을 사용하여 메모리 최적화 테이블의 인덱스를 인라인으로 지정해야 합니다. 메모리 최적화 테이블에 인덱스를 추가하려면 새 인덱스 사양을 포함하여 테이블을 삭제하고 다시 만듭니다.|  
|연산|ALTER TABLE|메모리 최적화 테이블 변경은 지원되지 않습니다. 업데이트된 테이블 정의를 사용하여 테이블을 삭제하고 다시 만듭니다.|  
|연산|CREATE FULLTEXT INDEX|전체 텍스트 인덱스는 메모리 최적화 테이블에서 지원되지 않습니다.|  
|연산|스키마 변경|메모리 액세스에 최적화된 테이블과 고유하게 컴파일된 저장 프로시저는 `sp_rename`과 같은 스키마 변경을 지원하지 않습니다.<br /><br /> 테이블 이름 바꾸기와 같이 스키마를 변경하려고 하면 오류 12320이 발생합니다. 스키마 버전을 변경해야 하는 작업(예: 이름 바꾸기)은 메모리 최적화 테이블에서 지원되지 않습니다.<br /><br /> 스키마를 변경하려면 테이블이나 프로시저를 삭제하고 업데이트된 정의를 사용하여 다시 만듭니다.|  
|연산|CREATE TRIGGER|메모리 최적화 테이블의 트리거는 지원되지 않습니다.|  
|연산|TRUNCATE TABLE|TRUNCATE 작업은 메모리 최적화 테이블에서 지원되지 않습니다. 테이블에서 모든 행을 제거 하려면 사용 하 여 모든 행이 삭제 `DELETE FROM` *테이블* 하거나 삭제 하 고 테이블을 다시 만듭니다.|  
|연산|ALTER AUTHORIZATION|메모리 최적화 테이블이나 고유하게 컴파일된 저장 프로시저의 소유자 변경은 지원되지 않습니다. 테이블이나 프로시저를 삭제하고 다시 만들어 소유권을 변경합니다.|  
|연산|ALTER SCHEMA|기존의 메모리 최적화 테이블이나 고유하게 컴파일된 저장 프로시저의 스키마 변경은 지원되지 않습니다. 스키마를 변경하려면 테이블이나 프로시저를 삭제하고 다시 만듭니다.|  
|연산|DBCC CHECKTABLE|DBCC CHECKTABLE은 메모리 최적화 테이블에서 지원되지 않습니다.|  
|기능|ANSI_PADDING OFF|세션 옵션 `ANSI_PADDING` 테이블이 나 고유 하 게 컴파일된 저장된 프로시저를 메모리 액세스에 최적화 된 만들 때 ON 이어야 합니다. CREATE 문을 실행하기 전에 `SET ANSI_PADDING ON`을 실행합니다.|  
|옵션|DATA_COMPRESSION|압축은 메모리 최적화 테이블에서 지원되지 않습니다. 테이블 정의에서 옵션을 제거합니다.|  
|기능|DTC|분산 트랜잭션에서는 메모리 액세스에 최적화된 테이블과 고유하게 컴파일된 저장 프로시저에 액세스할 수 없습니다. SQL 트랜잭션을 대산 사용합니다.|  
|기능|MARS(Multiple Active Result Sets)|MARS(Multiple Active Result Set)는 메모리 최적화 테이블에 지원되지 않습니다. 이 오류는 연결된 서버 사용을 나타낼 수도 있습니다. 연결된 서버는 MARS를 사용할 수 있습니다. 연결된 서버는 메모리 최적화 테이블에 지원되지 않습니다. 그 대신 메모리 최적화 테이블을 호스팅하는 서버와 데이터베이스에 직접 연결합니다.|  
|연산|메모리 액세스에 최적화된 테이블을 대상으로 사용하는 MERGE|메모리 액세스에 최적화된 테이블은 `MERGE` 작업의 대상일 수 없습니다. 사용 하 여 `INSERT`, `UPDATE`, 또는 `DELETE` 문 대신 합니다.|  
  
## <a name="indexes-on-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블의 인덱스  
 다음 표에서는 메모리 최적화 테이블의 인덱스와 관련된 오류의 메시지 텍스트에 나타날 수 있는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 기능 및 키워드와 오류를 해결하기 위한 수정 동작을 나열합니다.  
  
|형식|속성|해결 방법|  
|----------|----------|----------------|  
|기능|필터링된 인덱스|필터링된 인덱스는 메모리 최적화 테이블에서 지원되지 않습니다. 생략 된 `WHERE` 인덱스 사양에서 절.|  
|기능|UNIQUE|고유 인덱스는 메모리 최적화 테이블에서 지원되지 않습니다. 인덱스 사양에서 `UNIQUE` 인수를 제거합니다.|  
|기능|Null 허용 열|메모리 최적화 테이블의 인덱스 키에 있는 모든 열을 `NOT NULL`로 지정해야 합니다. 모든 열과 함께 `NOT NULL` 제약 조건을 인덱스 키에 포함시킵니다.|  
|기능|비-bin2 데이터 정렬|BIN2 데이터 정렬을 사용하여 메모리 최적화 인덱스의 키에 있는 모든 문자 열을 선언해야 합니다. `COLLATE` 절을 사용하여 열 정의에서 데이터 정렬을 설정합니다. 자세한 내용은 [Collations and Code Pages](../../database-engine/collations-and-code-pages.md)를 참조하세요.|  
|기능|포괄 열|메모리 최적화 테이블의 포괄 열을 지정할 필요가 없습니다. 메모리 최적화 테이블의 모든 열은 모든 메모리 최적화 인덱스에 암시적으로 포함됩니다.|  
|연산|ALTER INDEX|메모리 최적화 테이블의 인덱스 변경은 지원되지 않습니다. 그 대신 업데이트된 인덱스 사양을 사용하여 테이블을 삭제하고 다시 만듭니다.|  
|연산|DROP  INDEX|메모리 최적화 테이블의 인덱스 삭제는 지원되지 않습니다. 그 대신 테이블을 삭제하고 원하는 인덱스를 사용하여 테이블을 다시 만듭니다.|  
|인덱스 옵션|*인덱스 옵션*|표시된 인덱스 옵션은 메모리 최적화 테이블의 인덱스에 지원되지 않습니다. 인덱스 사양에서 옵션을 제거합니다.|  
  
## <a name="nonclustered-hash-indexes"></a>비클러스터형 해시 인덱스  
 다음 표에서는 비클러스터형 해시 인덱스와 관련된 오류의 메시지 텍스트에 나타날 수 있는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 기능 및 키워드와 오류를 해결하기 위한 수정 동작을 나열합니다.  
  
|형식|속성|해결 방법|  
|----------|----------|----------------|  
|옵션|ASC/DESC|비클러스터형 해시 인덱스가 정렬되지 않습니다. 인덱스 키 사양에서 `ASC` 및 `DESC` 키워드를 제거합니다.|  
  
## <a name="natively-compiled-stored-procedures"></a>Natively Compiled Stored Procedures  
 다음 표에서는 고유하게 컴파일된 저장 프로시저와 관련된 오류의 메시지 텍스트에 나타날 수 있는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 기능 및 키워드와 오류를 해결하기 위한 수정 동작을 나열합니다.  
  
|형식|기능|해결 방법|  
|----------|-------------|----------------|  
|기능|인라인 테이블 변수|변수 선언을 사용하여 테이블 형식을 인라인으로 선언할 수 없습니다. 테이블 형식을 사용 하 여 명시적으로 선언 해야 합니다는 `CREATE TYPE` 문.|  
|기능|커서|커서는 고유하게 컴파일된 저장 프로시저 위나 안에서 지원되지 않습니다.<br /><br /> -클라이언트에서 프로시저를 실행할 때 커서 API 대신 RPC를 사용 합니다. ODBC가 있는 경우 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 `EXECUTE`를 사용하지 말고 그 대신 프로시저 이름을 직접 지정합니다.<br /><br /> -에서 프로시저를 실행할 때는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리 또는 다른 저장된 프로시저를 고유 하 게 컴파일된 저장된 프로시저와 함께 커서를 사용 하지 마십시오.<br /><br /> -집합 기반 논리를 사용 하 여 커서를 사용 하는 대신 고유 하 게 컴파일된 저장된 프로시저를 만들 때는 또는 `WHILE` 루프입니다.|  
|기능|비 상수 매개 변수 기본값|고유하게 컴파일된 저장 프로시저에서 매개 변수와 함께 기본값을 사용할 때는 값이 상수여야 합니다. 매개 변수 선언에서 와일드카드를 제거 합니다.|  
|기능|EXTERNAL|CLR 저장 프로시저는 고유하게 컴파일될 수 없습니다. CREATE PROCEDURE 문에서 AS EXTERNAL 절이나 NATIVE_COMPILATION 옵션을 제거합니다.|  
|기능|번호가 매겨진 저장 프로시저|고유하게 컴파일된 저장 프로시저에 번호를 매길 수 없습니다. 제거는 `;` *번호* 에서 `CREATE PROCEDURE` 문.|  
|기능|다중 행 INSERT... VALUES 문|고유하게 컴파일된 저장 프로시저에서 동일한 `INSERT` 문을 사용하여 여러 행을 삽입할 수 없습니다. 만들 `INSERT` 각 행에 대 한 문입니다.|  
|기능|CTE(공통 테이블 식)|CTE(공통 테이블 식)은 고유하게 컴파일된 저장 프로시저에서 지원되지 않습니다. 쿼리를 다시 작성합니다.|  
|기능|하위 쿼리|하위 쿼리(다른 쿼리 내에 중첩된 쿼리)는 지원되지 않습니다. 쿼리를 다시 작성합니다.|  
|기능|COMPUTE|`COMPUTE` 절은 지원되지 않습니다. 쿼리에서 이 절을 제거합니다.|  
|기능|SELECT INTO|`INTO` 절은 `SELECT` 문에 지원되지 않습니다. 으로 쿼리를 다시 작성 `INSERT INTO` *테이블*`SELECT`합니다.|  
|기능|OUTPUT|`OUTPUT` 절은 지원되지 않습니다. 쿼리에서 이 절을 제거합니다.|  
|기능|불완전한 삽입 열 목록|`INSERT` 문에서는 테이블에 잇는 모든 열에 대해 값을 지정해야 합니다.|  
|기능|*함수*|기본 제공 함수는 고유하게 컴파일된 저장 프로시저에서 지원되지 않습니다. 저장 프로시저에서 함수를 제거합니다. 지원 되는 기본 제공 함수에 대 한 자세한 내용은 참조 [Natively Compiled Stored Procedures](../in-memory-oltp/natively-compiled-stored-procedures.md)합니다.|  
|기능|CASE|`CASE` 문은 고유하게 컴파일된 저장 프로시저 내부의 쿼리에서 지원되지 않습니다. 각 사례에 대해 쿼리를 만듭니다. 자세한 내용은 참조 [CASE 문 구현](implementing-a-case-expression-in-a-natively-compiled-stored-procedure.md)합니다.|  
|기능|사용자 정의 함수|사용자 정의 함수는 고유하게 컴파일된 저장 프로시저에서 사용할 수 없습니다. 프로시저 정의에서 함수에 대한 참조를 제거합니다.|  
|기능|사용자 정의 집계|사용자 정의 집계 함수는 고유하게 컴파일된 저장 프로시저에서 사용할 수 없습니다. 프로시저에서 함수에 대한 참조를 제거합니다.|  
|기능|찾아보기 모드 메타데이터|고유하게 컴파일된 저장 프로시저는 브라우저 모드 메타데이터를 지원하지 않습니다. 세션 옵션 `NO_BROWSETABLE`이 OFF로 설정되어 있는지 확인합니다.|  
|기능|FROM 절의 DELETE|`FROM` 절은 고유하게 컴파일된 저장 프로시저에서 테이블 원본을 사용하는 `DELETE` 문에 대해 지원되지 않습니다.<br /><br /> `DELETE` 와 `FROM` 절에서 삭제할 테이블을 나타내는 데 사용 하는 경우 지원 됩니다.|  
|기능|FROM 절의 UPDATE|`FROM` 절은 고유하게 컴파일된 저장 프로시저의 `UPDATE` 문에서 지원되지 않습니다.|  
|기능|임시 프로시저|임시 저장 프로시저를 고유하게 컴파일할 수 없습니다. 영구 고유하게 컴파일된 저장 프로시저 또는 임시 해석된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저를 만듭니다.|  
|격리 수준|READ UNCOMMITTED|격리 수준 READ UNCOMMITTED는 고유하게 컴파일된 저장 프로시저에서 지원되지 않습니다. SNAPSHOT과 같이 지원되는 격리 수준을 사용합니다.|  
|격리 수준|READ COMMITTED|격리 수준 READ UNCOMMITTED는 고유하게 컴파일된 저장 프로시저에서 지원되지 않습니다. SNAPSHOT과 같이 지원되는 격리 수준을 사용합니다.|  
|기능|임시 테이블|tempdb의 테이블은 고유하게 컴파일된 저장 프로시저에서 사용할 수 없습니다. 그 대신 테이블 변수 또는 DURABILITY=SCHEMA_ONLY인 메모리 최적화 테이블을 사용합니다.|  
|기능|MARS|MARS(Multiple Active Result Set)는 고유하게 컴파일된 저장 프로시저에 지원되지 않습니다. 이 오류는 연결된 서버 사용을 나타낼 수도 있습니다. 연결된 서버는 MARS를 사용할 수 있습니다. 연결된 서버는 고유하게 컴파일된 저장 프로시저에 지원되지 않습니다. 그 대신 고유하게 컴파일된 저장 프로시저를 호스팅하는 서버와 데이터베이스에 직접 연결합니다.|  
|기능|DTC|분산 트랜잭션에서는 메모리 액세스에 최적화된 테이블과 고유하게 컴파일된 저장 프로시저에 액세스할 수 없습니다. SQL 트랜잭션을 대산 사용합니다.|  
|기능|비-bin2 데이터 정렬|고유하게 컴파일된 저장 프로시저의 문자열에 비교, 정렬, 및 기타 작업을 수행하려면 BIN2 데이터 정렬을 사용해야 합니다. COLLATE 절을 사용하거나 적절한 데이터 정렬과 함께 열과 변수를 사용합니다. 자세한 내용은 [Collations and Code Pages](../../database-engine/collations-and-code-pages.md)를 참조하세요.|  
|기능|SC 데이터 정렬이 있는 문자열 잘림|`_SC` 데이터 정렬이 있는 문자열은 UTF-16 인코딩을 사용합니다. n(var)char 값을 단축된 길이의 n(var)char 값으로 변환하면 잘림이 발생합니다. 이 작업은 고유하게 컴파일된 저장 프로시저의 UTF-16 값에 대해 지원되지 않습니다. U t F-16 문자열의 잘림을 방지합니다.|  
|기능|EXECUTE WITH RECOMPILE|옵션 `WITH RECOMPILE` 고유 하 게 컴파일된 저장된 프로시저에 지원 되지 않습니다.|  
|기능|SC 데이터 정렬에 인수가 있는 LEN 및 SUBSTRING|_SC 데이터 정렬이 있는 문자열은 UTF-16 인코딩을 사용합니다. 기본 제공 함수 LEN 및 SUBSTRING은 고유하게 컴파일된 저장 프로시저 내에서 사용될 때 UTF-16 인코딩을 지원하지 않습니다. 다른 데이터 정렬을 사용하거나 이러한 함수를 사용하지 마십시오.|  
|기능|관리자 전용 연결에서 실행.|DAC(관리자 전용 연결)에서 고유하게 컴파일된 저장 프로시저를 실행할 수 없습니다. 일반 연결을 대신 사용합니다.|  
|연산|ALTER PROCEDURE|고유하게 컴파일된 저장 프로시저를 변경할 수 없습니다. 프로시저 정의를 변경하려면 저장 프로시저를 삭제하고 다시 만듭니다.|  
|연산|저장점(savepoint)|활성 저장점이 있는 트랜잭션에서 고유하게 컴파일된 저장 프로시저를 호출할 수 없습니다. 트랜잭션에서 저장점을 제거합니다.|  
|연산|ALTER AUTHORIZATION|메모리 최적화 테이블이나 고유하게 컴파일된 저장 프로시저의 소유자 변경은 지원되지 않습니다. 테이블이나 프로시저를 삭제하고 다시 만들어 소유권을 변경합니다.|  
|연산자|OPENROWSET|이 연산자는 지원되지 않습니다. 제거 `OPENROWSET` 에서 고유 하 게 컴파일된 저장 프로시저입니다.|  
|연산자|OPENQUERY|이 연산자는 지원되지 않습니다. 제거 `OPENQUERY` 에서 고유 하 게 컴파일된 저장 프로시저입니다.|  
|연산자|OPENDATASOURCE|이 연산자는 지원되지 않습니다. 제거 `OPENDATASOURCE` 에서 고유 하 게 컴파일된 저장 프로시저입니다.|  
|연산자|OPENXML|이 연산자는 지원되지 않습니다. 제거 `OPENXML` 에서 고유 하 게 컴파일된 저장 프로시저입니다.|  
|연산자|CONTAINSTABLE|이 연산자는 지원되지 않습니다. 제거 `CONTAINSTABLE` 에서 고유 하 게 컴파일된 저장 프로시저입니다.|  
|연산자|FREETEXTTABLE|이 연산자는 지원되지 않습니다. 제거 `FREETEXTTABLE` 에서 고유 하 게 컴파일된 저장 프로시저입니다.|  
|기능|테이블 반환 함수|테이블 반환 함수는 고유하게 컴파일된 저장 프로시저에서 참조할 수 없습니다. 이러한 제한에 대한 가능한 해결 방법 중 하나는 테이블 반환 함수의 논리를 프로시저 본문에 추가하는 것입니다.|  
|연산자|CHANGETABLE|이 연산자는 지원되지 않습니다. 제거 `CHANGETABLE` 에서 고유 하 게 컴파일된 저장 프로시저입니다.|  
|연산자|GOTO|이 연산자는 지원되지 않습니다. WHILE과 같은 다른 프로시저 구문을 사용합니다.|  
|연산자|EXECUTE, INSERT EXEC|고유하게 컴파일된 저장 프로시저 중첩은 지원되지 않습니다. 필요한 작업을 저장 프로시저의 일부로 인라인으로 지정할 수 있습니다.|  
|연산자|OFFSET|이 연산자는 지원되지 않습니다. 제거 `OFFSET` 에서 고유 하 게 컴파일된 저장 프로시저입니다.|  
|연산자|UNION|이 연산자는 지원되지 않습니다. 제거 `UNION` 에서 고유 하 게 컴파일된 저장 프로시저입니다. 테이블 변수를 사용하여 여러 결과 집합을 단일 결과 집합으로 결합할 수 있습니다.|  
|연산자|INTERSECT|이 연산자는 지원되지 않습니다. 제거 `INTERSECT` 에서 고유 하 게 컴파일된 저장 프로시저입니다. 일부 경우에는 INNER JOIN을 사용하여 동일한 결과를 얻을 수 있습니다.|  
|연산자|EXCEPT|이 연산자는 지원되지 않습니다. 제거 `EXCEPT` 에서 고유 하 게 컴파일된 저장 프로시저입니다.|  
|연산자|OUTER JOIN|이 연산자는 지원되지 않습니다. 제거 `OUTER JOIN` 에서 고유 하 게 컴파일된 저장 프로시저입니다. 자세한 내용은 참조 [외부 조인 구현](implementing-an-outer-join.md)합니다.|  
|연산자|APPLY|이 연산자는 지원되지 않습니다. 제거 `APPLY` 에서 고유 하 게 컴파일된 저장 프로시저입니다.|  
|연산자|PIVOT|이 연산자는 지원되지 않습니다. 제거 `PIVOT` 에서 고유 하 게 컴파일된 저장 프로시저입니다.|  
|연산자|UNPIVOT|이 연산자는 지원되지 않습니다. 제거 `UNPIVOT` 에서 고유 하 게 컴파일된 저장 프로시저입니다.|  
|연산자|OR, IN|분리(OR, IN)는 고유하게 컴파일된 저장 프로시저에 있는 쿼리의 WHERE 절에서 지원되지 않습니다. 각 사례에 대해 쿼리를 만듭니다.|  
|연산자|CONTAINS|이 연산자는 지원되지 않습니다. 제거 `CONTAINS` 에서 고유 하 게 컴파일된 저장 프로시저입니다.|  
|연산자|FREETEXT|이 연산자는 지원되지 않습니다. 제거 `FREETEXT` 에서 고유 하 게 컴파일된 저장 프로시저입니다.|  
|연산자|NOT|이 연산자는 지원되지 않습니다. 제거 `NOT` 에서 고유 하 게 컴파일된 저장 프로시저입니다. 일부 경우에는 `NOT`을 같지 않음으로 대체할 수 있습니다. 예를 들어, `NOT a=b`를 `a!=b`로 대체할 수 있습니다.|  
|연산자|TSEQUAL|이 연산자는 지원되지 않습니다. 제거 `TSEQUAL` 에서 고유 하 게 컴파일된 저장 프로시저입니다.|  
|연산자|LIKE|이 연산자는 지원되지 않습니다. 제거 `LIKE` 에서 고유 하 게 컴파일된 저장 프로시저입니다.|  
|연산자|NEXT VALUE FOR|고유하게 컴파일된 저장 프로시저 내부에서 시퀀스를 참조할 수 없습니다. 해석된 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 값을 얻은 다음 고유하게 컴파일된 저장 프로시저로 값을 전달합니다. 자세한 내용은 [메모리 액세스에 최적화된 테이블에서 IDENTITY 구현](implementing-identity-in-a-memory-optimized-table.md)을 참조하세요.|  
|SET 옵션|*옵션*|고유하게 컴파일된 저장 프로시저 내부에서 SET 옵션을 변경할 수 없습니다. BEGIN ATOMIC 문을 사용하여 특정 옵션을 설정할 수 있습니다. 자세한 내용은 [Natively Compiled Stored Procedures](../in-memory-oltp/natively-compiled-stored-procedures.md)에서 ATOMIC 블록에 대한 섹션을 참조하십시오.|  
|피연산자|TABLESAMPLE|이 연산자는 지원되지 않습니다. 제거 `TABLESAMPLE` 에서 고유 하 게 컴파일된 저장 프로시저입니다.|  
|옵션|RECOMPILE|고유하게 컴파일된 저장 프로시저는 만들 때 컴파일됩니다. 고유하게 컴파일된 저장 프로시저를 다시 컴파일하려면 프로시저를 삭제하고 다시 만드십시오. 제거 `RECOMPILE` 프로시저 정의에서 합니다.|  
|옵션|ENCRYPTION|이 옵션은 지원되지 않습니다. 제거 `ENCRYPTION` 프로시저 정의에서 합니다.|  
|옵션|FOR REPLICATION|복제를 위해 고유하게 컴파일된 저장 프로시저를 만들 수 없습니다. 프로시저 정의에서 `FOR REPLICATION`을 제거합니다.|  
|옵션|FOR XML|이 옵션은 지원되지 않습니다. 제거 `FOR XML` 에서 고유 하 게 컴파일된 저장 프로시저입니다.|  
|옵션|FOR BROWSE|이 옵션은 지원되지 않습니다. 제거 `FOR BROWSE` 에서 고유 하 게 컴파일된 저장 프로시저입니다.|  
|조인 힌트|HASH, MERGE|고유하게 컴파일된 저장 프로시저는 중첩 루프 조인만 지원합니다. 해시 및 병합 조인은 지원되지 않습니다. 조인 힌트를 제거합니다.|  
|쿼리 힌트|*쿼리 힌트*|이 쿼리 힌트는 고유하게 컴파일된 저장 프로시저 내부에 없습니다. 지원되는 쿼리 힌트는 [쿼리 힌트&#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-query)를 참조하세요.|  
|옵션|DISTINCT|이 옵션은 지원되지 않습니다. 고유하게 컴파일된 저장 프로시저의 쿼리에서 `DISTINCT`를 제거합니다.|  
|옵션|PERCENT|이 옵션이 지원 되지 않습니다 `TOP` 절. 고유하게 컴파일된 저장 프로시저의 쿼리에서 `PERCENT`를 제거합니다.|  
|옵션|WITH  TIES|이 옵션이 지원 되지 않습니다 `TOP` 절. 고유하게 컴파일된 저장 프로시저의 쿼리에서 `WITH TIES`를 제거합니다.|  
|집계 함수|*Aggregate 함수*|이 절은 지원되지 않습니다. 고유하게 컴파일된 저장 프로시저의 집계 함수에 대한 자세한 내용은 [Natively Compiled Stored Procedures](../in-memory-oltp/natively-compiled-stored-procedures.md)를 참조하십시오.|  
|순위 함수|*순위 함수*|순위 함수는 고유하게 컴파일된 저장 프로시저에서 지원되지 않습니다. 프로시저 정의에서 해당 함수를 제거합니다.|  
|기능|*함수*|이 함수는 지원되지 않습니다. 고유하게 컴파일된 저장 프로시저에서 해당 함수를 제거합니다.|  
|인수를 제거합니다.|*문*|이 문은 지원되지 않습니다. 고유하게 컴파일된 저장 프로시저에서 해당 함수를 제거합니다.|  
|기능|문자 및 이진 문자열과 함께 사용되는 MIN 및 MAX|집계 함수 `MIN` 및 `MAX`는 고유하게 컴파일된 저장 프로시저 내부의 문자와 이진 문자열에 사용할 수 없습니다.|  
|기능|집계 함수 없는 GROUP BY|고유하게 컴파일된 저장 프로시저에서 쿼리에 `GROUP BY` 절이 있으면 쿼리에서 SELECT 또는 HAVING 절에 집계 함수도 사용해야 합니다. 집계 함수를 쿼리에 추가합니다.|  
|기능|GROUP BY ALL|ALL은 고유하게 컴파일된 저장 프로시저에서 GROUP BY 절에 사용할 수 없습니다. GROUP BY 절에서 ALL을 제거합니다.|  
|기능|GROUP BY ()|빈 목록으로 그룹화는 지원되지 않습니다. GROUP BY 절을 제거하거나 그룹화 목록에 열을 포함합니다.|  
|기능|ROLLUP|`ROLLUP`은 고유하게 컴파일된 저장 프로시저에서 `GROUP BY` 절에 사용할 수 없습니다. 제거 `ROLLUP` 프로시저 정의에서 합니다.|  
|기능|CUBE|`CUBE`은 고유하게 컴파일된 저장 프로시저에서 `GROUP BY` 절에 사용할 수 없습니다. 제거 `CUBE` 프로시저 정의에서 합니다.|  
|기능|GROUPING SETS|`GROUPING SETS`은 고유하게 컴파일된 저장 프로시저에서 `GROUP BY` 절에 사용할 수 없습니다. 제거 `GROUPING SETS` 프로시저 정의에서 합니다.|  
|기능|BEGIN TRANSACTION, COMMIT TRANSACTION 및 ROLLBACK TRANSACTION|ATOMIC 블록을 사용하여 트랜잭션과 오류 처리를 제어합니다. 자세한 내용은 [Atomic Blocks](atomic-blocks-in-native-procedures.md)을(를) 참조하십시오.|  
|기능|인라인 테이블 변수 선언|테이블 변수는 명시적으로 정의된 메모리 최적화 테이블 형식을 참조해야 합니다. 메모리 최적화 테이블 형식을 만들고 이 형식을 인라인으로 지정하는 대신 변수 선언에 이 형식을 사용합니다.|  
|기능|sp_recompile|고유하게 컴파일된 저장 프로시저의 다시 컴파일은 지원되지 않습니다. 프로시저를 삭제하고 다시 만듭니다.|  
|기능|EXECUTE AS CALLER|`EXECUTE AS` 절은 필수입니다. 그러나 `EXECUTE AS CALLER`는 지원되지 않습니다. 사용 하 여 `EXECUTE AS OWNER`, `EXECUTE AS` *사용자*, 또는 `EXECUTE AS SELF`합니다.|  
|기능|디스크 기반 테이블|디스크 기반 테이블은 고유하게 컴파일된 저장 프로시저에서 액세스할 수 없습니다. 고유하게 컴파일된 저장 프로시저에서 디스크 기반 테이블에 대한 참조를 제거합니다. 또는 디스크 기반 테이블을 메모리 액세스에 최적화된 테이블로 마이그레이션합니다.|  
|기능|뷰|뷰는 고유하게 컴파일된 저장 프로시저에서 액세스할 수 없습니다. 뷰 대신 기본 테이블을 참조합니다.|  
|기능|테이블 반환 함수|테이블 반환 함수는 고유하게 컴파일된 저장 프로시저에서 액세스할 수 없습니다. 고유하게 컴파일된 저장 프로시저에서 테이블 반환 함수에 대한 참조를 제거합니다.|  
  
## <a name="transactions-that-access-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블에 액세스하는 트랜잭션  
 다음 표에서는 메모리 최적화 테이블에 액세스하는 트랜잭션과 관련된 오류의 메시지 텍스트에 나타날 수 있는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 기능 및 키워드와 오류를 해결하기 위한 수정 동작을 나열합니다.  
  
|형식|속성|해결 방법|  
|----------|----------|----------------|  
|기능|저장점(savepoint)|메모리 최적화 테이블에 액세스하는 트랜잭션에서 명시적인 저장점을 만드는 작업은 지원되지 않습니다.|  
|기능|바운드 트랜잭션|바운드 세션은 메모리 최적화 테이블에 액세스하는 트랜잭션에 참여할 수 없습니다. 프로시저를 실행하기 전에 세션을 바인딩하지 마십시오.|  
|기능|DTC|메모리 최적화 테이블에 액세스하는 트랜잭션은 분산 트랜잭션일 수 없습니다.|  
  
## <a name="see-also"></a>관련 항목  
 [메모리 내 OLTP로 마이그레이션](migrating-to-in-memory-oltp.md)  
  
  
