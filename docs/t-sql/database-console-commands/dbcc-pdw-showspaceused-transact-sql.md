---
title: DBCC PDW_SHOWSPACEUSED (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/17/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: t-sql|database-console-commands
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 73f598cf-b02a-4dba-8d89-9fc0b55a12b8
caps.latest.revision: "10"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8c564a6debb9c110cb41f8fc90a7cc1c0c5a01f7
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="dbcc-pdwshowspaceused-transact-sql"></a>DBCC PDW_SHOWSPACEUSED (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

행 개수, 예약 된 디스크 공간 또는 모든 테이블의 특정 테이블에 사용 된 디스크 공간을 표시 한 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 데이터베이스입니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [TRANSACT-SQL 구문 표기 규칙 &#40; Transact SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
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
 [ *database_name* . [ *schema_name* ] . | *schema_name* . ] *table_name*  
 한, 두 또는 표시 될 테이블의 세 부분으로 이루어진 이름입니다. 두 또는 세 부분으로 구성 테이블 이름, 이름을 큰따옴표로 묶어야 합니다 (""). 한 부분으로 이루어진 테이블 이름 묶는 따옴표를 사용 하는 것은 선택 사항입니다. 없는 테이블 이름이 지정 된 경우 현재 데이터베이스에 대 한 정보가 표시 됩니다.  
  
## <a name="permissions"></a>Permissions  
VIEW SERVER STATE 권한이 필요합니다.
  
## <a name="result-sets"></a>결과 집합  
결과 집합에 모든 테이블입니다.
  
|열|데이터 형식|Description|  
|------------|---------------|-----------------|  
|reserved_space|bigint|총 공간 (kb)에서 데이터베이스에 사용 합니다.|  
|data_space|bigint|공간 데이터 (kb)에서에 사용 합니다.|  
|index_space|bigint|Kb에서 인덱스에 사용 되는 공간입니다.|  
|unused_space|bigint|공간을 예약 된 공간의 일부로 및 KB의 사용 되지 않습니다.|  
|pdw_node_id|int|데이터에 대해 사용 되는 노드를 계산 합니다.|  
  
결과 한 테이블 집합입니다.
  
|열|데이터 형식|Description|범위|  
|------------|---------------|-----------------|-----------|  
|rows|bigint|행 수입니다.||  
|reserved_space|bigint|Kb에서 개체에 대 한 예약 된 총 공간입니다.||  
|data_space|bigint|KB 단위로 데이터에 사용 되는 공간입니다.||  
|index_space|bigint|Kb에서 인덱스에 사용 되는 공간입니다.||  
|unused_space|bigint|공간을 예약 된 공간의 일부로 및 KB의 사용 되지 않습니다.||  
|pdw_node_id|int|공간 사용량을 보고에 사용 되는 노드를 계산 합니다.||  
|distribution_id|int|공간 사용량을 보고에 사용 되는 배포 합니다.|값은 복제 된 테이블에 대 한-1입니다.|  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="a-dbcc-pdwshowspaceused-basic-syntax"></a>1. DBCC PDW_SHOWSPACEUSED 기본 구문  
다음 예제 행 수를 표시, 디스크 공간을 예약 하는 여러 가지 방법을 보여 주고 디스크 FactInternetSales 테이블에서 사용 되는 공간은 [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)] 데이터베이스입니다.
  
```sql
-- Uses AdventureWorks  
  
DBCC PDW_SHOWSPACEUSED ( "AdventureWorksPDW2012.dbo.FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( "AdventureWorksPDW2012..FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( "dbo.FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( FactInternetSales );  
```  
  
### <a name="b-show-the-disk-space-used-by-all-tables-in-the-current-database"></a>2. 현재 데이터베이스의 모든 테이블에 사용 된 디스크 공간을 표시  
 다음 예제에서는 디스크 공간을 예약 하 여 모든 사용자 테이블과 시스템 테이블에 사용 된 [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)] 데이터베이스입니다.  
  
```sql
-- Uses AdventureWorks  
  
DBCC PDW_SHOWSPACEUSED;  
```  
 ## <a name="see-also"></a>참고 항목
[상태가 아니므로 DBCC PDW_SHOWEXECUTIONPLAN &#40; Transact SQL &#41;](dbcc-pdw-showexecutionplan-transact-sql.md)  
[DBCC PDW_SHOWPARTITIONSTATS &#40; Transact SQL &#41;](dbcc-pdw-showpartitionstats-transact-sql.md)

  
