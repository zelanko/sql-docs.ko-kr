---
title: 해석된 T-SQL을 사용하는 메모리 최적화 테이블
description: 해석된 Transact-SQL(Transact-SQL 일괄 처리 또는 SQL Server의 저장 프로시저)을 사용하여 메모리 최적화 테이블에 액세스하는 방법에 대해 알아봅니다.
ms.custom: seo-dt-2019
ms.date: 05/31/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 92a44d4d-0e53-4fb0-b890-de264c65c95a
author: MightyPen
ms.author: genemi
monikerRange: =azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 63e19c205bf635257d8b5b4957fe64b6ec310c64
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97465464"
---
# <a name="accessing-memory-optimized-tables-using-interpreted-transact-sql"></a>해석된 Transact-SQL을 사용하여 메모리 액세스에 최적화된 테이블에 액세스
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

 단지 몇 가지 예외를 제외하고 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리 또는 DML 작업(SELECT, INSERT, UPDATE 또는 DELETE), 임시 일괄 처리, 테이블 반환 함수, 트리거, 뷰 및 저장 프로시저와 같은 SQL 모듈을 사용하여 메모리 최적화 테이블에 액세스할 수 있습니다.  
  
해석된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리 또는 고유하게 컴파일된 저장 프로시저가 아닌 저장 프로시저를 의미합니다. 메모리 최적화 테이블에 대한 해석된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 액세스를 interop 액세스라고 합니다.  

[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 해석된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리는 메모리 최적화 테이블을 직렬 모드 대신 병렬로 스캔할 수 있습니다.

메모리 액세스에 최적화된 테이블은 고유하게 컴파일된 저장 프로시저를 사용하여 액세스할 수도 있습니다. 고유하게 컴파일된 저장 프로시저는 성능이 중요한 OLTP 작업에 권장됩니다.  
  
해석된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 액세스는 다음과 같은 시나리오에 권장됩니다.  
  
- 임시 쿼리 및 관리 태스크  
  
- 고유하게 컴파일된 저장 프로시저(예: 종종 *OVER* 함수라고 하는 [window](../../t-sql/queries/select-over-clause-transact-sql.md) 함수)에서 사용할 수 없는 구문을 일반적으로 사용하는 보고 쿼리  
  
- 애플리케이션 코드를 최소한으로 변경하거나 변경하지 않고 애플리케이션에서 성능이 중요한 부분을 메모리 최적화 테이블로 마이그레이션하려는 경우. 테이블을 마이그레이션하면 성능이 향상될 수 있습니다. 그런 다음 저장 프로시저를 고유하게 컴파일된 저장 프로시저로 마이그레이션하면 성능이 추가로 향상될 수 있습니다.  
  
- [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 고유하게 컴파일된 저장 프로시저에 사용할 수 없는 경우  
  
그러나 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 구문은 메모리 최적화 테이블의 데이터에 액세스하는 해석된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저에서 지원되지 않습니다.  
  
|영역|지원되지 않음|  
|----------|-----------------|  
|테이블에 대한 액세스|TRUNCATE TABLE<br /><br /> MERGE(메모리 최적화 테이블을 대상으로 사용)<br /><br /> 동적 및 키 집합 커서(자동으로 정적 커서로 강등됨)<br /><br /> 컨텍스트 연결을 사용하여 CLR 모듈에서 액세스<br /><br /> 인덱싱된 뷰에서 메모리 최적화 테이블 참조|  
|데이터베이스 간|데이터베이스 간 쿼리<br /><br /> 데이터베이스 간 트랜잭션<br /><br /> 연결된 서버|  
  
## <a name="table-hints"></a>테이블 힌트

테이블 힌트에 대한 자세한 내용은 [테이블 힌트&#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)를 참조하세요. [!INCLUDE[hek_2](../../includes/hek-2-md.md)]를 지원하기 위해 SNAPSHOT이 추가되었습니다.  
  
다음 테이블 힌트는 해석된 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 메모리 최적화 테이블에 액세스하는 경우 지원되지 않습니다.  

:::row:::
    :::column:::
        HOLDLOCK

        PAGLOCK

        READUNCOMMITTED

        TABLOCKXX
    :::column-end:::
    :::column:::
        IGNORE_CONSTRAINTS

        READCOMMITTED

        ROWLOCK

        UPDLOCK
    :::column-end:::
    :::column:::
        IGNORE_TRIGGERS

        READCOMMITTEDLOCK

        SPATIAL_WINDOW_MAX_CELLS = *integer*

        XLOCK
    :::column-end:::
    :::column:::
        NOWAIT

        READPAST

        TABLOCK
    :::column-end:::
:::row-end:::

해석된 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 명시적 또는 암시적 트랜잭션에서 메모리 최적화 테이블에 액세스하는 경우 적어도 다음 중 하나를 수행해야 합니다.  
  
- SNAPSHOT, REPEATABLEREAD, SERIALIZABLE 등 [격리 수준 테이블 힌트](../../relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md) 를 지정합니다.  
  
- [MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT](../../t-sql/statements/alter-database-transact-sql-set-options.md) 데이터베이스 옵션을 ON으로 설정합니다.  
  
[자동 커밋 모드](../../odbc/reference/develop-app/auto-commit-mode.md)에서 실행되는 쿼리에서 액세스하는 메모리 최적화 테이블에는 격리 수준 테이블 힌트가 필요하지 않습니다.  
  
## <a name="see-also"></a>참고 항목

[메모리 내 OLTP에 대한 Transact-SQL 지원](../../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)   

[메모리 내 OLTP로 마이그레이션](./plan-your-adoption-of-in-memory-oltp-features-in-sql-server.md)