---
description: DBCC PDW_SHOWEXECUTIONPLAN(Transact-SQL)
title: DBCC PDW_SHOWEXECUTIONPLAN(Transact-SQL)
ms.custom: ''
ms.date: 07/16/2017
ms.prod: sql
ms.technology: data-warehouse
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: pmasl
ms.author: umajay
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: b83bba2f706b88e6a11e8efb50aaf5be4c52c152
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88417629"
---
# <a name="dbcc-pdw_showexecutionplan-transact-sql"></a>DBCC PDW_SHOWEXECUTIONPLAN(Transact-SQL)

[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

특정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 컴퓨팅 노드 또는 제어 노드에서 실행되는 쿼리에 대한 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 실행 계획을 표시합니다. 이를 사용하여 쿼리가 컴퓨팅 노드 및 제어 노드에서 실행되는 동안 쿼리 성능 문제를 해결합니다.
  
컴퓨팅 노드에서 실행되는 SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리에 대한 쿼리 성능 문제를 인식한 후에는 성능을 향상시키기 위한 여러 가지 방법이 있습니다. 컴퓨팅 노드에서 쿼리 성능을 향상시키는 가능한 방법에는 여러 열 통계를 만들거나 비클러스터형 인덱스를 만들거나 쿼리 힌트를 사용하는 것이 포함됩니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙&#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
Azure SQL Data Warehouse용 구문:

```syntaxsql
DBCC PDW_SHOWEXECUTIONPLAN ( distribution_id, spid )  
[;]  
```  
구문 Azure 병렬 데이터 웨어하우스:
  
```syntaxsql
DBCC PDW_SHOWEXECUTIONPLAN ( pdw_node_id, spid )  
[;]  
```  

## <a name="arguments"></a>인수  
 *distribution_id*  
 쿼리 계획을 실행하는 분포에 대한 식별자입니다. 이는 NULL이 아닌 정수여야 합니다. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]를 대상으로 할 때 사용합니다.  
  
 *pdw_node_id*  
 쿼리 계획을 실행하는 노드에 대한 식별자입니다. 이는 NULL이 아닌 정수여야 합니다. 어플라이언스를 대상으로 할 때 사용합니다.  
  
 *spid*  
 쿼리 계획을 실행하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 세션에 대한 식별자입니다. 이는 NULL이 아닌 정수여야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]에 대한 CONTROL 권한이 필요합니다.  
  
어플라이언스에서 VIEW-SERVER-STATE 권한이 필요합니다.
  
## <a name="examples-sssdw"></a>예제: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]  
  
### <a name="a-dbcc-pdw_showexecutionplan-basic-syntax"></a>A. DBCC PDW_SHOWEXECUTIONPLAN 기본 구문  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 인스턴스에서 실행되는 경우 distribution_id를 선택하도록 위 쿼리를 수정합니다.  
  
```sql
SELECT [sql_spid], [pdw_node_id], [request_id], [dms_step_index], [type], [start_time], [end_time], [status], [distribution_id]  
FROM sys.dm_pdw_dms_workers   
WHERE [status] <> 'StepComplete' and [status] <> 'StepError'  
order by request_id, [dms_step_index];  
```  
  
이렇게 하면 각각 적극적으로 배포를 실행하기 위해 spid가 반환됩니다. 배포 1이 세션 375에서 실행되는 데 관한 자세한 내용을 보려면 다음 명령을 실행합니다.
  
```sql
DBCC PDW_SHOWEXECUTIONPLAN ( 1, 375 );  
```  

## <a name="examples-sspdw"></a>예제: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="b-dbcc-pdw_showexecutionplan-basic-syntax"></a>B. DBCC PDW_SHOWEXECUTIONPLAN 기본 구문  
 너무 오래 실행되는 쿼리는 DMS 쿼리 계획 작업 또는 SQL 쿼리 계획 작업을 실행 중입니다.  
  
쿼리가 DMS 쿼리 계획 작업을 실행 중인 경우 다음 쿼리를 사용하여 완료되지 않은 단계에 대한 노드 ID 및 세션 ID의 목록을 검색할 수 있습니다.
  
```sql
SELECT [sql_spid], [pdw_node_id], [request_id], [dms_step_index], [type], [start_time], [end_time], [status]   
FROM sys.dm_pdw_dms_workers   
WHERE [status] <> 'StepComplete' and [status] <> 'StepError'  
AND pdw_node_id = 201001   
order by request_id, [dms_step_index], [distribution_id];  
```  
  
이전 쿼리 결과를 기반으로 DBCC PDW_SHOWEXECUTIONPLAN에 sql_spid 및 pdw_node_id 매개 변수를 사용합니다. 예를 들어 다음 명령은 pdw_node_id 201001 및 sql_spid 375에 대한 실행 계획을 보여 줍니다.
  
```sql
DBCC PDW_SHOWEXECUTIONPLAN ( 201001, 375 );  
```  

## <a name="see-also"></a>참고 항목

- [DBCC PDW_SHOWPARTITIONSTATS &#40;Transact-SQL&#41;](dbcc-pdw-showpartitionstats-transact-sql.md)  
- [DBCC PDW_SHOWSPACEUSED&#40;Transact-SQL&#41;](dbcc-pdw-showspaceused-transact-sql.md)
