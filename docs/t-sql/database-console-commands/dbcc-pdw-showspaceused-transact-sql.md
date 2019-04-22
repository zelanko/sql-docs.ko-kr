---
title: DBCC PDW_SHOWSPACEUSED (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 73f598cf-b02a-4dba-8d89-9fc0b55a12b8
author: pmasl
ms.author: umajay
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: fc06dca68c6b6a4cedc730433401076ca07b126b
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59042342"
---
# <a name="dbcc-pdwshowspaceused-transact-sql"></a>DBCC PDW_SHOWSPACEUSED (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 데이터베이스의 모든 테이블 또는 특정 테이블에 대해 행 수, 예약된 디스크 공간, 사용한 디스크 공간을 표시합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙&#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
-- Show the space used for all user tables and system tables in the current database  
DBCC PDW_SHOWSPACEUSED  
[;]  
  
-- Show the space used for a table  
DBCC PDW_SHOWSPACEUSED ( " [ database_name . [ schema_name ] . ] | [ schema_name .] table_name  " )  
[;]  
```  
  
## <a name="arguments"></a>인수  
 `[ database_name . [ schema_name ] . | schema_name . ] table_name`  
 표시될 테이블의 한 부분, 두 부분 또는 세 부분으로 이루어진 이름입니다. 두 부분 또는 세 부분으로 구성된 테이블 이름의 경우 이름을 큰따옴표(“”)로 묶어야 합니다. 한 부분으로 이루어진 테이블 이름을 따옴표로 묶는 것은 선택 사항입니다. 지정한 테이블 이름이 없으면 현재 데이터베이스에 대한 정보가 표시됩니다.  
  
## <a name="permissions"></a>사용 권한  
VIEW SERVER STATE 권한이 필요합니다.
  
## <a name="result-sets"></a>결과 집합  
다음은 모든 테이블에 관한 결과 집합입니다.
  
|Column|데이터 형식|설명|  
|------------|---------------|-----------------|  
|reserved_space|BIGINT|데이터베이스에 사용된 총 공간(KB)입니다.|  
|data_space|BIGINT|데이터에 사용된 공간(KB)입니다.|  
|index_space|BIGINT|인덱스에 사용된 공간(KB)입니다.|  
|unused_space|BIGINT|예약된 공간이면서 사용되지 않은 공간(KB)입니다.|  
|pdw_node_id|ssNoversion|데이터에 대해 사용되는 컴퓨팅 노드입니다.|  
  
한 테이블에 관한 결과 집합입니다.
  
|Column|데이터 형식|설명|범위|  
|------------|---------------|-----------------|-----------|  
|rows|BIGINT|행 수입니다.||  
|reserved_space|BIGINT|개체에 예약된 총 공간(KB)입니다.||  
|data_space|BIGINT|데이터에 사용된 공간(KB)입니다.||  
|index_space|BIGINT|인덱스에 사용된 공간(KB)입니다.||  
|unused_space|BIGINT|예약된 공간이면서 사용되지 않은 공간(KB)입니다.||  
|pdw_node_id|ssNoversion|공간 사용량 보고에 사용되는 컴퓨팅 노드입니다.||  
|distribution_id|ssNoversion|공간 사용량 보고에 사용되는 배포입니다.|복제된 테이블의 경우 값이 -1입니다.|  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="a-dbcc-pdwshowspaceused-basic-syntax"></a>1. DBCC PDW_SHOWSPACEUSED 기본 구문  
다음 예제에서는 행 수, 예약된 디스크 공간, [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)] 데이터베이스의 FactInternetSales 테이블에서 사용하는 디스크 공간을 표시합니다.
  
```sql
-- Uses AdventureWorks  
  
DBCC PDW_SHOWSPACEUSED ( "AdventureWorksPDW2012.dbo.FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( "AdventureWorksPDW2012..FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( "dbo.FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( FactInternetSales );  
```  
  
### <a name="b-show-the-disk-space-used-by-all-tables-in-the-current-database"></a>2. 현재 데이터베이스의 모든 테이블에 사용된 디스크 공간 표시  
 다음 예제에서는 예약된 디스크 공간과, [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)] 데이터베이스의 모든 사용자 테이블 및 시스템 테이블에서 사용된 디스크 공간을 표시합니다.  
  
```sql
-- Uses AdventureWorks  
  
DBCC PDW_SHOWSPACEUSED;  
```  
 ## <a name="see-also"></a>관련 항목:
[DBCC PDW_SHOWEXECUTIONPLAN &#40;Transact-SQL&#41;](dbcc-pdw-showexecutionplan-transact-sql.md)  
[DBCC PDW_SHOWPARTITIONSTATS &#40;Transact-SQL&#41;](dbcc-pdw-showpartitionstats-transact-sql.md)

  
