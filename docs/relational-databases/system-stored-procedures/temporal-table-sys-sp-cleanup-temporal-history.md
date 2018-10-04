---
title: sys.sp_cleanup_temporal_history | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
ms.assetid: 6eff30b4-b261-4f1f-b93c-1f69d754298d
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: e38a137e2aff51573bcf1284c36cd3658e970591
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47624291"
---
# <a name="sysspcleanuptemporalhistory-transact-sql"></a>sys.sp_cleanup_temporal_history (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

단일 트랜잭션 내에서 구성 된 HISTORY_RETENTION 기간 일치 하는 temporal 기록 테이블에서 모든 행을 제거 합니다.
  
## <a name="syntax"></a>구문  
```  
sp_cleanup_temporal_history [@schema_name = ] schema_name, [@table_name = ] table_name [, [@row_count=] @row_count_var [OUTPUT]]
```  
  
## <a name="arguments"></a>인수  

*@table_name*

호출 되는 보존 정리 temporal 테이블의 이름입니다.

*schema_name*

현재 temporal 테이블이 속한 스키마의 이름

*row_count_var* [OUTPUT]

삭제 된 행 수를 반환 하는 출력 매개 변수입니다. 이 매개 변수를 반환 됩니다 경우 기록 테이블에 클러스터형 columnstore 인덱스 있음, 항상 0입니다.
  
## <a name="remarks"></a>Remarks
이 저장된 프로시저는 한정 된 재방문 주기 기간 지정한 temporal 테이블 함께만 사용할 수 있습니다.
즉시 기록 테이블에서 오래 된 모든 행을 제거 해야 하는 경우에이 저장된 프로시저를 사용 합니다. 동일한 트랜잭션 내의 모든 적격 행을 삭제 하는 대로 데이터베이스 로그 및 I/O 하위 시스템에 상당한 영향 있을 수 있음을 알아야 합니다. 

항상 오래 된 일반 워크 로드 및 일반적인 데이터베이스에 대 한 최소한의 영향을 사용 하 여 행을 제거는 정리를 위한 내부 백그라운드 태스크를 사용 하는 것이 좋습니다.

## <a name="permissions"></a>사용 권한  
 Db_owner 권한이 필요합니다.  

## <a name="example"></a>예제

```
declare @rowcnt int
EXEC sys.sp_cleanup_temporal_history 'dbo', 'Department', @rowcnt output
select @rowcnt
```

## <a name="see-also"></a>참고자료

[임시 테이블 보존 정책](https://docs.microsoft.com/azure/sql-database/sql-database-temporal-tables-retention-policy)
