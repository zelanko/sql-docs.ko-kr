---
description: DBCC PDW_SHOWSPACEUSED (Transact-SQL)
title: DBCC PDW_SHOWSPACEUSED (Transact-SQL)
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
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: b5f8274b7d73bb0119b165b1cfbe65473b499d55
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88479825"
---
# <a name="dbcc-pdw_showspaceused-transact-sql"></a>DBCC PDW_SHOWSPACEUSED (Transact-SQL)

[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 데이터베이스의 모든 테이블 또는 특정 테이블에 대해 행 수, 예약된 디스크 공간, 사용한 디스크 공간을 표시합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙&#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문
  
```syntaxsql
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
  
|열|데이터 형식|Description|  
|------------|---------------|-----------------|  
|reserved_space|bigint|데이터베이스에 사용된 총 공간(KB)입니다.|  
|data_space|bigint|데이터에 사용된 공간(KB)입니다.|  
|index_space|bigint|인덱스에 사용된 공간(KB)입니다.|  
|unused_space|bigint|예약된 공간이면서 사용되지 않은 공간(KB)입니다.|  
|pdw_node_id|int|데이터에 대해 사용되는 컴퓨팅 노드입니다.|  
  
한 테이블에 관한 결과 집합입니다.
  
|열|데이터 형식|Description|범위|  
|------------|---------------|-----------------|-----------|  
|rows|bigint|행 수입니다.||  
|reserved_space|bigint|개체에 예약된 총 공간(KB)입니다.||  
|data_space|bigint|데이터에 사용된 공간(KB)입니다.||  
|index_space|bigint|인덱스에 사용된 공간(KB)입니다.||  
|unused_space|bigint|예약된 공간이면서 사용되지 않은 공간(KB)입니다.||  
|pdw_node_id|int|공간 사용량 보고에 사용되는 컴퓨팅 노드입니다.||  
|distribution_id|int|공간 사용량 보고에 사용되는 배포입니다.|복제된 테이블의 경우 값이 -1입니다.|  
  
## <a name="examples-sssdw-and-sspdw"></a>예: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="a-dbcc-pdw_showspaceused-basic-syntax"></a>A. DBCC PDW_SHOWSPACEUSED 기본 구문  
다음 예제에서는 행 수, 예약된 디스크 공간, [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)] 데이터베이스의 FactInternetSales 테이블에서 사용하는 디스크 공간을 표시합니다.
  
```sql
-- Uses AdventureWorks  
  
DBCC PDW_SHOWSPACEUSED ( "AdventureWorksPDW2012.dbo.FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( "AdventureWorksPDW2012..FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( "dbo.FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( FactInternetSales );  
```  
  
### <a name="b-show-the-disk-space-used-by-all-tables-in-the-current-database"></a>B. 현재 데이터베이스의 모든 테이블에 사용된 디스크 공간 표시  

 다음 예제에서는 예약된 디스크 공간과, [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)] 데이터베이스의 모든 사용자 테이블 및 시스템 테이블에서 사용된 디스크 공간을 표시합니다.  
  
```sql
-- Uses AdventureWorks  
  
DBCC PDW_SHOWSPACEUSED;  
```  

## <a name="see-also"></a>참고 항목

- [DBCC PDW_SHOWEXECUTIONPLAN &#40;Transact-SQL&#41;](dbcc-pdw-showexecutionplan-transact-sql.md)  
- [DBCC PDW_SHOWPARTITIONSTATS &#40;Transact-SQL&#41;](dbcc-pdw-showpartitionstats-transact-sql.md)
