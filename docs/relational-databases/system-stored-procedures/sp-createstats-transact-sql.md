---
title: sp_createstats (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_createstats_TSQL
- sp_createstats
dev_langs:
- TSQL
helpviewer_keywords:
- sp_createstats
ms.assetid: 8204f6f2-5704-40a7-8d51-43fc832eeb54
caps.latest.revision: 47
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 17d061eec260c1553fb03623ed392444f02ea939
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="spcreatestats-transact-sql"></a>sp_createstats(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  호출 된 [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) 문이 열 통계 개체의 첫 번째 열은 아직에서 단일 열 통계를 만들려면 합니다. 단일 열 통계를 만들면 히스토그램의 수가 늘어나며 이에 따라 카디널리티 예상치, 쿼리 계획 및 쿼리 성능이 향상될 수 있습니다. 히스토그램은 통계 개체의 첫 번째 열에 있으며 다른 열에는 없습니다.  
  
 sp_createstats는 쿼리 실행 시간이 중요하며 쿼리 최적화 프로그램에서 단일 열 통계를 생성할 때까지 기다릴 수 없는 경우, 즉 벤치마킹 등과 같은 응용 프로그램에 유용합니다. 대부분의 경우에서 필요는 없습니다; sp_createstats를 사용 하려면 경우 최적화 프로그램에서 쿼리를 개선 하기 위해 필요에 따라 단일 열 통계를 생성 하는 쿼리 계획의 **AUTO_CREATE_STATISTICS** 옵션이 설정 되어 있습니다.  
  
 통계에 대 한 자세한 내용은 참조 [통계](../../relational-databases/statistics/statistics.md)합니다. 단일 열 통계를 생성 하는 방법에 대 한 자세한 내용은 참조는 **AUTO_CREATE_STATISTICS** 옵션 [ALTER DATABASE SET 옵션 &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_createstats   
    [   [ @indexonly =   ] { 'indexonly'   | 'NO' } ]   
    [ , [ @fullscan =    ] { 'fullscan'    | 'NO' } ]   
    [ , [ @norecompute = ] { 'norecompute' | 'NO' } ]  
    [ , [ @incremental = ] { 'incremental' | 'NO' } ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@indexonly=** ] **'indexonly'**  
 기존 인덱스에 있으며 인덱스 정의의 첫 번째 열이 아닌 열에 대해서만 통계를 만듭니다. **indexonly** 은 **char (9)**합니다. 기본값은 NO입니다.  
  
 [  **@fullscan=** ] **'fullscan'**  
 사용 하 여는 [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) 문을 **FULLSCAN** 옵션입니다. **fullscan** 은 **char (9)**합니다.  기본값은 NO입니다.  
  
 [  **@norecompute=** ] **'norecompute'**  
 사용 하 여는 [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) 문을 **NORECOMPUTE** 옵션입니다. **norecompute** 은 **char(12)**합니다.  기본값은 NO입니다.  
  
 [  **@incremental=** ] **'증분'**  
 사용 하 여는 [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) 문을 **INCREMENTAL = ON** 옵션입니다. **증분** 은 **char(12)**합니다.  기본값은 NO입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 새로운 각 통계 개체는 해당 통계가 만들어진 열과 동일한 이름을 갖습니다.  
  
## <a name="remarks"></a>주의  
 sp_createstats 만들거나 기존 통계 개체;에 있는 첫 번째 열이 열에 대 한 통계를 업데이트 하지 않습니다.  인덱스, AUTO_CREATE_STATISTICS 옵션을 사용 하 여 생성 하는 단일 열 통계가 있는 열 및 CREATE STATISTICS 문을 통해 만들어진 통계의 첫 번째 열에 대해 만들어진 통계의 첫 번째 열 포함 됩니다. sp_createstats 만들지 않습니다 통계 비활성화 된 인덱스의 첫 번째 열에 활성화 된 다른 인덱스에 해당 열이 사용 하지 않는 한 합니다. sp_createstats는 비활성화 된 클러스터형된 인덱스가 있는 테이블에 대해 통계를 만들지 않습니다.  
  
 테이블에 열이 하나인 경우 sp_createstats는 스파스 열에 대한 통계를 만들지 않습니다. 열 집합 및 스파스 열에 대 한 자세한 내용은 참조 [열 집합 사용](../../relational-databases/tables/use-column-sets.md) 및 [스파스 열을 사용 하 여](../../relational-databases/tables/use-sparse-columns.md)합니다.  
  
## <a name="permissions"></a>Permissions  
 db_owner 고정 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-create-single-column-statistics-on-all-eligible-columns"></a>1. 적합한 모든 열에 대한 단일 열 통계 만들기  
 다음 예에서는 현재 데이터베이스에 있는 적합한 모든 열에 대한 단일 열 통계를 만듭니다.  
  
```  
EXEC sp_createstats;  
GO  
```  
  
### <a name="b-create-single-column-statistics-on-all-eligible-index-columns"></a>2. 적합한 모든 인덱스 열에 대한 단일 열 통계 만들기  
 다음 예에서는 인덱스에 있으며 인덱스의 첫 번째 열이 아닌, 적합한 모든 열에 대한 단일 열 통계를 만듭니다.  
  
```  
EXEC sp_createstats 'indexonly';  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [통계](../../relational-databases/statistics/statistics.md)   
 [CREATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [DBCC SHOW_STATISTICS&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [UPDATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [데이터베이스 엔진 저장 프로시저 &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
