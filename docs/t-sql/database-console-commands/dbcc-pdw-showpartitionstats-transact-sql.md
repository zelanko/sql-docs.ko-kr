---
title: DBCC PDW_SHOWPARTITIONSTATS (Transact SQL) | Microsoft Docs
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
caps.latest.revision: "10"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fb41140783d4c334e7ee701f44d523ec68e41435
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="dbcc-pdwshowpartitionstats-transact-sql"></a>DBCC PDW_SHOWPARTITIONSTATS (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

크기와 수에 있는 테이블의 각 파티션에 대 한 행의 표시는 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 데이터베이스입니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [TRANSACT-SQL 구문 표기 규칙 &#40; Transact SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
Show the partition stats for a table  
DBCC PDW_SHOWPARTITIONSTATS ( " [ database_name . [ schema_name ] . ] | [ schema_name.] table_name  ")  
[;]  
```  
  
## <a name="arguments"></a>인수  
 [ *database_name* 합니다. [ *schema_name* ]. | *schema_name* 합니다. ] *table_name*  
 한, 두 또는 표시 될 테이블의 세 부분으로 이루어진 이름입니다.  두 또는 세 부분으로 구성 테이블 이름, 이름을 큰따옴표로 묶어야 합니다 (""). 한 부분으로 이루어진 테이블 이름 묶는 따옴표를 사용 하는 것은 선택 사항입니다.  
  
## <a name="permissions"></a>Permissions
필요한 **VIEW SERVER STATE** 권한.
  
## <a name="result-sets"></a>결과 집합  
이 DBCC PDW_SHOWPARTITIONSTATS 명령에 대 한 결과입니다.
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|partition_number|int|파티션 번호입니다.|  
|used_page_count|bigint|데이터에 사용 되는 페이지 수입니다.|  
|reserved_page_count|bigint|파티션에 할당 된 페이지 수입니다.|  
|row_count|bigint|파티션에 있는 행의 수입니다.|  
|pdw_node_id|int|데이터에 대 한 노드를 계산 합니다.|  
|distribution_id|int|데이터에 대 한 배포 id입니다.|  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="a-dbcc-pdwshowpartitionstats-basic-syntax-examples"></a>1. DBCC PDW_SHOWPARTITIONSTATS 기본 구문 예제  
FactInternetSales 테이블에 대해 파티션을 사용 된 공간 및 행 수를 표시 하는 다음 예제에서는 [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)] 데이터베이스입니다.
  
```sql
DBCC PDW_SHOWPARTITIONSTATS ("ssawPDW.dbo.FactInternetSales");  
DBCC PDW_SHOWPARTITIONSTATS ("dbo.FactInternetSales");  
DBCC PDW_SHOWPARTITIONSTATS (FactInternetSales);  
```  
## <a name="see-also"></a>참고 항목
[상태가 아니므로 DBCC PDW_SHOWEXECUTIONPLAN &#40; Transact SQL &#41;](dbcc-pdw-showexecutionplan-transact-sql.md)  
[DBCC PDW_SHOWSPACEUSED &#40; Transact SQL &#41;](dbcc-pdw-showspaceused-transact-sql.md)  
  
