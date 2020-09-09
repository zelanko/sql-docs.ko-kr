---
description: sp_createstats(Transact-SQL)
title: sp_createstats (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_createstats_TSQL
- sp_createstats
dev_langs:
- TSQL
helpviewer_keywords:
- sp_createstats
ms.assetid: 8204f6f2-5704-40a7-8d51-43fc832eeb54
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6c49367f78a257b1ba4e19d9916b590a67991d1a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536711"
---
# <a name="sp_createstats-transact-sql"></a>sp_createstats(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  [CREATE statistics](../../t-sql/statements/create-statistics-transact-sql.md) 문을 호출 하 여 통계 개체의 첫 번째 열이 아닌 열에 대 한 단일 열 통계를 만듭니다. 단일 열 통계를 만들면 히스토그램의 수가 늘어나며 이에 따라 카디널리티 예상치, 쿼리 계획 및 쿼리 성능이 향상될 수 있습니다. 히스토그램은 통계 개체의 첫 번째 열에 있으며 다른 열에는 없습니다.  
  
 sp_createstats는 쿼리 실행 시간이 중요하며 쿼리 최적화 프로그램에서 단일 열 통계를 생성할 때까지 기다릴 수 없는 경우, 즉 벤치마킹 등과 같은 애플리케이션에 유용합니다. 대부분의 경우 sp_createstats를 사용할 필요가 없습니다. **AUTO_CREATE_STATISTICS** 옵션을 on으로 설정 하면 쿼리 최적화 프로그램에서 필요에 따라 단일 열 통계를 생성 하 여 쿼리 계획을 향상 시킵니다.  
  
 통계에 대한 자세한 내용은 [통계](../../relational-databases/statistics/statistics.md)를 참조하세요. 단일 열 통계를 생성 하는 방법에 대 한 자세한 내용은 [ALTER DATABASE SET Options &#40;transact-sql&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)에서 **AUTO_CREATE_STATISTICS** 옵션을 참조 하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_createstats   
    [   [ @indexonly =   ] { 'indexonly'   | 'NO' } ]   
    [ , [ @fullscan =    ] { 'fullscan'    | 'NO' } ]   
    [ , [ @norecompute = ] { 'norecompute' | 'NO' } ]  
    [ , [ @incremental = ] { 'incremental' | 'NO' } ]  
```  
  
## <a name="arguments"></a>인수  
`[ @indexonly = ] 'indexonly'` 기존 인덱스에 있으며 인덱스 정의의 첫 번째 열이 아닌 열에 대해서만 통계를 만듭니다. **indexonly** 는 **char (9)** 입니다. 기본값은 NO입니다.  
  
`[ @fullscan = ] 'fullscan'`[CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) 문을 **FULLSCAN** 옵션과 함께 사용 합니다. **fullscan** 은 **char (9)** 입니다.  기본값은 NO입니다.  
  
`[ @norecompute = ] 'norecompute'`[CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) 문을 **NORECOMPUTE** 옵션과 함께 사용 합니다. **norecompute** 은 **char (12)** 입니다.  기본값은 NO입니다.  
  
`[ @incremental = ] 'incremental'`[CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) 문을 **증분 = ON** 옵션과 함께 사용 합니다. **증분** 은 **char (12)** 입니다.  기본값은 NO입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 새로운 각 통계 개체는 해당 통계가 만들어진 열과 동일한 이름을 갖습니다.  
  
## <a name="remarks"></a>설명  
 sp_createstats는 기존 통계 개체의 첫 번째 열인 열에 대해서는 통계를 만들거나 업데이트 하지 않습니다.  여기에는 인덱스에 대해 만들어진 통계의 첫 번째 열, AUTO_CREATE_STATISTICS 옵션으로 생성 된 단일 열 통계를 포함 하는 열 및 CREATE STATISTICS 문으로 만든 통계의 첫 번째 열이 포함 됩니다. 사용 하지 않도록 설정 된 다른 인덱스에서 열을 사용 하지 않는 한 sp_createstats는 비활성화 된 인덱스의 첫 번째 열에 대 한 통계를 만들지 않습니다. sp_createstats는 비활성화 된 클러스터형 인덱스가 있는 테이블에 대 한 통계를 만들지 않습니다.  
  
 테이블에 열이 하나인 경우 sp_createstats는 스파스 열에 대한 통계를 만들지 않습니다. 열 집합 및 스파스 열에 대 한 자세한 내용은 [열 집합 사용](../../relational-databases/tables/use-column-sets.md) 및 [스파스 열 사용](../../relational-databases/tables/use-sparse-columns.md)을 참조 하세요.  
  
## <a name="permissions"></a>사용 권한  
 db_owner 고정 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-create-single-column-statistics-on-all-eligible-columns"></a>A. 적합한 모든 열에 대한 단일 열 통계 만들기  
 다음 예에서는 현재 데이터베이스에 있는 적합한 모든 열에 대한 단일 열 통계를 만듭니다.  
  
```  
EXEC sp_createstats;  
GO  
```  
  
### <a name="b-create-single-column-statistics-on-all-eligible-index-columns"></a>B. 적합한 모든 인덱스 열에 대한 단일 열 통계 만들기  
 다음 예에서는 인덱스에 있으며 인덱스의 첫 번째 열이 아닌, 적합한 모든 열에 대한 단일 열 통계를 만듭니다.  
  
```  
EXEC sp_createstats 'indexonly';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [통계](../../relational-databases/statistics/statistics.md)   
 [CREATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [DBCC SHOW_STATISTICS&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [UPDATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [Transact-sql&#41;&#40;저장 프로시저 데이터베이스 엔진 ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
