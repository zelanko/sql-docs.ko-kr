---
title: "상태가 아니므로 DBCC PDW_SHOWEXECUTIONPLAN (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.service: sql-data-warehouse
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
caps.latest.revision: 12
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 461ee87f41692172b31125e36553c0eab0b09772
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-pdwshowexecutionplan-transact-sql"></a>상태가 아니므로 DBCC PDW_SHOWEXECUTIONPLAN (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

표시는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 특정에서 실행 되는 쿼리 실행 계획 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 컨트롤 노드 또는 계산 합니다. 이 사용 하 여 계산 노드 및 제어 노드가에서 실행 되 고 쿼리 하는 동안 쿼리 성능 문제를 해결 합니다.
  
SMP에 대 한 쿼리 성능 문제는 인식 되 면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계산 노드에서 실행 되는 쿼리 성능 향상을 위해 여러 가지 있습니다. 계산 노드에서 쿼리 성능을 향상 시키는 가능한 방법에는 여러 열 통계를 만들거나 비클러스터형 인덱스를 만드는 하 쿼리 힌트를 사용 하 여 포함 됩니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [TRANSACT-SQL 구문 표기 규칙 &#40; Transact SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
SQL Server에 대 한 구문:

```sql
DBCC PDW_SHOWEXECUTIONPLAN ( distribution_id, spid )  
[;]  
```  
Azure 병렬 데이터 웨어하우스 구문:
  
```sql
DBCC PDW_SHOWEXECUTIONPLAN ( pdw_node_id, spid )  
[;]  
```  
  
## <a name="arguments"></a>인수  
 *distribution_id*  
 쿼리 계획을 실행 하는 분포에 대 한 식별자입니다. 정수 이며 NULL 일 수 없습니다. 대상으로 할 때 사용 되는 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]합니다.  
  
 *pdw_node_id*  
 쿼리 계획을 실행 하는 노드에 대 한 식별자입니다. 정수 이며 NULL 일 수 없습니다. 어플라이언스를 대상으로 할 때 사용 합니다.  
  
 *spid*  
 에 대 한 식별자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 계획을 실행 중인 세션입니다. 정수 이며 NULL 일 수 없습니다.  
  
## <a name="permissions"></a>Permissions  
 에 대 한 CONTROL 권한이 필요 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]합니다.  
  
어플라이언스에서 서버 상태 보기 권한이 필요합니다.
  
## <a name="examples-includesssdwincludessssdw-mdmd"></a>예제:[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]  
  
### <a name="a-dbcc-pdwshowexecutionplan-basic-syntax"></a>1. 상태가 아니므로 DBCC PDW_SHOWEXECUTIONPLAN 기본 구문  
 실행 되는 경우는 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 인스턴스를 위의 쿼리는 distribution_id ± ֳ ֵ를 수정 합니다.  
  
```sql
SELECT [sql_spid], [pdw_node_id], [request_id], [dms_step_index], [type], [start_time], [end_time], [status], [distribution_id]  
FROM sys.dm_pdw_dms_workers   
WHERE [status] <> 'StepComplete' and [status] <> 'StepError'  
order by request_id, [dms_step_index];  
```  
  
이렇게 하면 각 적극적으로 배포를 실행 하기 위한 spid를 반환 됩니다. 어떤 배포 1 375 세션에서 실행에 대 한 자세한 내용을 보려면 인 경우 다음 명령을 실행 합니다.
  
```sql
DBCC PDW_SHOWEXECUTIONPLAN ( 1, 375 );  
```  

## <a name="examples-includesspdwincludessspdw-mdmd"></a>예제:[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="b-dbcc-pdwshowexecutionplan-basic-syntax"></a>2. 상태가 아니므로 DBCC PDW_SHOWEXECUTIONPLAN 기본 구문  
 너무 오래 실행 되는 쿼리는 쿼리를 실행 하거나 실행 한 DMS 계획 작업이 또는 SQL 쿼리 계획 작업.  
  
쿼리 DMS 쿼리 계획 작업을 실행 중인 경우에 노드 Id 및 완료 된 단계에 대 한 세션 Id의 목록을 검색 하려면 다음 쿼리를 사용할 수 있습니다.
  
```sql
SELECT [sql_spid], [pdw_node_id], [request_id], [dms_step_index], [type], [start_time], [end_time], [status]   
FROM sys.dm_pdw_dms_workers   
WHERE [status] <> 'StepComplete' and [status] <> 'StepError'  
AND pdw_node_id = 201001   
order by request_id, [dms_step_index], [distribution_id];  
```  
  
앞의 쿼리 결과에 based를 sql_spid 및 pdw_node_id DBCC PDW_SHOWEXEUCTIONPLAN에 매개 변수로 사용 합니다. 예를 들어 다음 명령은 pdw_node_id 201001 및 sql_spid 375에 대 한 실행 계획을 보여 줍니다.
  
```sql
DBCC PDW_SHOWEXECUTIONPLAN ( 201001, 375 );  
```  

## <a name="see-also"></a>참고 항목
[DBCC PDW_SHOWPARTITIONSTATS &#40; Transact SQL &#41;](dbcc-pdw-showpartitionstats-transact-sql.md)  
[DBCC PDW_SHOWSPACEUSED &#40; Transact SQL &#41;](dbcc-pdw-showspaceused-transact-sql.md)
