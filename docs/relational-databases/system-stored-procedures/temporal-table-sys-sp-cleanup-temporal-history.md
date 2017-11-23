---
title: sys.sp_cleanup_temporal_history | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: 
ms.prod_service: sql-database
ms.service: sql-database
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6eff30b4-b261-4f1f-b93c-1f69d754298d
caps.latest.revision: "4"
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ed631f41e1ce49bfa431645b5f439925190198c7
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="temporal-table---sysspcleanuptemporalhistory"></a>임시 테이블-sys.sp_cleanup_temporal_history
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

단일 트랜잭션 내에서 구성 된 HISTORY_RETENTION 기간 일치 하는 임시 기록 테이블에서 모든 행을 제거 합니다.
  
## <a name="syntax"></a>구문  
```  
sp_cleanup_temporal_history [@schema_name = ] schema_name, [@table_name = ] table_name [, [@row_count=] @row_count_var [OUTPUT]]
```  
  
## <a name="arguments"></a>인수  

*@table_name*

정리 호출 되는 보존에 대 한 임시 테이블의 이름입니다.

*schema_name*

현재 임시 테이블에 속한 스키마의 이름

*row_count_var* [출력]

삭제 된 행 수를 반환 하는 출력 매개 변수입니다. 이 매개 변수를 반환 합니다 경우 기록 테이블에는 클러스터형 columnstore 인덱스, 항상 0입니다.
  
## <a name="remarks"></a>주의
이 저장된 프로시저가 임시 테이블 에서만 사용할 수 있는지가 무한 보존 기간이 지정 합니다.
즉시 기록 테이블에서 오래 된 모든 행을 정리 해야 하는 경우에이 저장된 프로시저를 사용 합니다. 것은 데이터베이스 로그와 I/O 하위 시스템에 상당한 영향을 동일한 트랜잭션 내에서 적합 한 모든 행을 삭제 하는 것이 알아야 합니다. 

항상 제거 정기 작업 및 일반적으로 데이터베이스에 대 한 최소한의 영향을 가진 행이 오래 된 있는지 정리에 대 한 내부 백그라운드 태스크에 의존 하는 것이 좋습니다.

## <a name="permissions"></a>Permissions  
 Db_owner 권한이 필요합니다.  

## <a name="example"></a>예제

```
declare @rowcnt int
EXEC sys.sp_cleanup_temporal_history 'dbo', 'Department', @rowcnt output
select @rowcnt
```

## <a name="see-also"></a>참고 항목

[임시 테이블 보존 정책](https://docs.microsoft.com/azure/sql-database/sql-database-temporal-tables-retention-policy)
