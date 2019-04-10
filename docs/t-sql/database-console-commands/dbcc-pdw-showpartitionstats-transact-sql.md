---
title: DBCC PDW_SHOWPARTITIONSTATS(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: pmasl
ms.author: umajay
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 7b80b96436b8cc7346a69a8b2448ade60dd009b5
ms.sourcegitcommit: 3cfedfeba377560d460ca3e42af1e18824988c07
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/05/2019
ms.locfileid: "59042302"
---
# <a name="dbcc-pdwshowpartitionstats-transact-sql"></a>DBCC PDW_SHOWPARTITIONSTATS(Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 데이터베이스에 있는 테이블의 각 파티션에 대한 크기와 행 수를 표시합니다.
  
![문서 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "문서 링크 아이콘") [Transact-SQL 구문 표기 규칙&#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
Show the partition stats for a table  
DBCC PDW_SHOWPARTITIONSTATS ( " [ database_name . [ schema_name ] . ] | [ schema_name.] table_name  ")  
[;]  
```  
  
## <a name="arguments"></a>인수  
 `[ database_name . [ schema_name ] . | schema_name . ] table_name`  
 표시될 테이블의 한 부분, 두 부분 또는 세 부분으로 이루어진 이름입니다.  두 부분 또는 세 부분으로 구성된 테이블 이름의 경우 이름을 큰따옴표(“”)로 묶어야 합니다. 한 부분으로 이루어진 테이블 이름을 따옴표로 묶는 것은 선택 사항입니다.  
  
## <a name="permissions"></a>사용 권한
**VIEW SERVER STATE** 권한이 필요합니다.
  
## <a name="result-sets"></a>결과 집합  
이 집합은 DBCC PDW_SHOWPARTITIONSTATS 명령에 대한 결과입니다.
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|partition_number|ssNoversion|파티션 번호입니다.|  
|used_page_count|BIGINT|데이터에 사용되는 페이지 수입니다.|  
|reserved_page_count|BIGINT|파티션에 사용하도록 예약된 페이지의 수입니다.|  
|row_count|BIGINT|파티션의 행 수입니다.|  
|pdw_node_id|ssNoversion|데이터에 대한 노드를 컴퓨팅합니다.|  
|distribution_id|ssNoversion|데이터의 배포 식별자입니다.|  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="a-dbcc-pdwshowpartitionstats-basic-syntax-examples"></a>1. DBCC PDW_SHOWPARTITIONSTATS 기본 구문 예제  
다음 예제에서는 [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)] 데이터베이스의 FactInternetSales 테이블에 대해 파티션별 사용된 공간 및 행 수를 표시합니다.
  
```sql
DBCC PDW_SHOWPARTITIONSTATS ("ssawPDW.dbo.FactInternetSales");  
DBCC PDW_SHOWPARTITIONSTATS ("dbo.FactInternetSales");  
DBCC PDW_SHOWPARTITIONSTATS (FactInternetSales);  
```  
## <a name="see-also"></a>관련 항목:
[DBCC PDW_SHOWEXECUTIONPLAN &#40;Transact-SQL&#41;](dbcc-pdw-showexecutionplan-transact-sql.md)  
[DBCC PDW_SHOWSPACEUSED &#40;Transact-SQL&#41;](dbcc-pdw-showspaceused-transact-sql.md)  
 
