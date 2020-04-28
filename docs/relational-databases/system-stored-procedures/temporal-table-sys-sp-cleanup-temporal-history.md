---
title: sys. sp_cleanup_temporal_history | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 6eff30b4-b261-4f1f-b93c-1f69d754298d
author: CarlRabeler
ms.author: carlrab
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 302291ae42fa5fbb2f7dea94ccdb9f659379f5bc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74165830"
---
# <a name="syssp_cleanup_temporal_history-transact-sql"></a>sys. sp_cleanup_temporal_history (Transact-sql)

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

단일 트랜잭션 내에서 구성 된 HISTORY_RETENTION 기간과 일치 하는 temporal 기록 테이블의 모든 행을 제거 합니다.

## <a name="syntax"></a>구문

```
sp_cleanup_temporal_history [@schema_name = ] schema_name, [@table_name = ] table_name [, [@row_count=] @row_count_var [OUTPUT]]
```

## <a name="arguments"></a>인수

*\@table_name*

보존 정리가 호출 되는 temporal 테이블의 이름입니다.

*schema_name*

현재 temporal 테이블이 속한 스키마의 이름

*row_count_var* [출력]

삭제 된 행의 수를 반환 하는 출력 매개 변수입니다. 기록 테이블에 클러스터형 columnstore 인덱스가 있으면이 매개 변수는 항상 0을 반환 합니다.

## <a name="remarks"></a>설명

이 저장 프로시저는 유한 보존 기간을 지정한 temporal 테이블에만 사용할 수 있습니다.
기록 테이블에서 오래 된 행을 모두 즉시 정리 해야 하는 경우에만이 저장 프로시저를 사용 합니다. 데이터베이스 로그 및 i/o 하위 시스템에는 동일한 트랜잭션 내에 있는 모든 행을 삭제할 때 상당한 영향을 줄 수 있다는 것을 알고 있어야 합니다.

일반적으로 일반 작업 및 데이터베이스에 미치는 영향을 최소화 하 여 오래 된 행을 제거 하는 정리를 위해 내부 백그라운드 작업을 사용 하는 것이 좋습니다.

## <a name="permissions"></a>사용 권한

Db_owner 권한이 필요 합니다.

## <a name="example"></a>예제

```sql
declare @rowcnt int
EXEC sys.sp_cleanup_temporal_history 'dbo', 'Department', @rowcnt output
select @rowcnt
```

## <a name="next-steps"></a>다음 단계

[Temporal 테이블 보존 정책](https://docs.microsoft.com/azure/sql-database/sql-database-temporal-tables-retention-policy)
