---
title: sys.dm_pdw_nodes_exec_text_query_plan (Transact-sql) | Microsoft Docs
description: TSQL 일괄 처리 또는 일괄 처리 내 특정 문에 대 한 텍스트 형식의 실행 계획을 반환 하는 동적 관리 뷰
ms.custom: ''
ms.date: 10/14/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: ''
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: =azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 5ac37e8c768068244c549d28d9bf6d157d46e853
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92035296"
---
# <a name="sysdm_pdw_nodes_exec_text_query_plan--transact-sql"></a>sys.dm_pdw_nodes_exec_text_query_plan (Transact-sql)
[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

[!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리 또는 일괄 처리 내 특정 문에 대한 텍스트 형식의 실행 계획을 반환합니다.

## <a name="table-returned"></a>반환 된 테이블  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**pdw_node_ID**|**int**|노드와 연결 된 고유 숫자 ID입니다.|
|**dbid**|**smallint**|이 계획에 해당하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 컴파일할 당시 유효했던 컨텍스트 데이터베이스의 ID입니다. 임시 및 준비된 SQL 문의 경우 문이 컴파일된 데이터베이스의 ID입니다.<br /><br /> 열이 Null 값을 허용합니다.|  
|**objectid**|**int**|이 쿼리 계획에 대한 저장 프로시저나 사용자 정의 함수와 같은 개체의 ID입니다. 임시 및 준비된 일괄 처리의 경우 이 열은 **Null**입니다.<br /><br /> 열이 Null 값을 허용합니다.|  
|**number**|**smallint**|번호가 매겨진 저장 프로시저 정수입니다. 임시 및 준비된 일괄 처리의 경우 이 열은 **Null**입니다.<br /><br /> 열이 Null 값을 허용합니다.| 
|**됨**|**bit**|해당 저장 프로시저가 암호화되었는지 여부를 나타냅니다.<br /><br /> 0 = 암호화되지 않음<br /><br /> 1 = 암호화됨<br /><br /> 열은 Null을 허용하지 않습니다.|  
|**query_plan**|**nvarchar(max)**|*Plan_handle*지정 된 쿼리 실행 계획의 컴파일 시간 실행 계획 표현을 포함 합니다. 실행 계획은 텍스트 형식입니다. 임시 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문, 저장 프로시저 호출, 사용자 정의 함수 호출 등이 포함된 각 일괄 처리에 대해 계획 하나가 생성됩니다.<br /><br /> 열이 Null 값을 허용합니다.|  

## <a name="remarks"></a>설명  
[Sys.dm_exec_text_query_plan](./sys-dm-exec-text-query-plan-transact-sql.md?view=sql-server-ver15) 에 동일한 설명이 적용 됩니다.  

## <a name="permissions"></a>사용 권한  
 서버에 대 한 **sysadmin** 서버 역할 또는 `VIEW SERVER STATE` 권한이 필요 합니다.  
  
## <a name="see-also"></a>참조  
 [Transact-sql&#41;&#40;Azure Synapse 분석 및 병렬 데이터 웨어하우스 동적 관리 뷰 ](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  

  ## <a name="next-steps"></a>다음 단계
 더 많은 개발 팁은 [SQL Data Warehouse 개발 개요](/azure/sql-data-warehouse/sql-data-warehouse-overview-develop)를 참조하세요.