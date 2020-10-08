---
title: sys.dm_pdw_nodes_exec_query_statistics_xml (Transact-sql) | Microsoft Docs
description: 진행 중인 요청에 대 한 쿼리 실행 계획을 반환 하는 동적 관리 뷰 이 DMV를 사용 하 여 임시 통계를 사용 하 여 실행 계획 XML을 검색 합니다.
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
ms.openlocfilehash: 790431cd6effe4d1b3d21db46325782e05419e4f
ms.sourcegitcommit: 32135463a8494d9ed1600a58f51819359e3c09dc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/08/2020
ms.locfileid: "91834195"
---
# <a name="dm_pdw_nodes_exec_query_statistics_xml-transact-sql"></a>dm_pdw_nodes_exec_query_statistics_xml (Transact-sql)
[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

진행 중인 요청에 대 한 쿼리 실행 계획을 반환 합니다. 이 DMV를 사용 하 여 임시 통계를 사용 하 여 실행 계획 XML을 검색 합니다.

## <a name="table-returned"></a>반환 된 테이블

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|
|node_id|**int**|노드와 연결 된 고유 숫자 ID입니다.|
|session_id|**smallint**|세션의 ID입니다. Null을 허용하지 않습니다.|
|request_id|**int**|요청의 ID입니다. Null을 허용하지 않습니다.|
|sql_handle|**varbinary(64)**|쿼리가 속하는 일괄 처리 또는 저장 프로시저를 고유 하 게 식별 하는 토큰입니다. Null을 허용합니다.|
|plan_handle|**varbinary(64)**|현재 실행 중인 일괄 처리에 대 한 쿼리 실행 계획을 고유 하 게 식별 하는 토큰입니다. Null을 허용합니다.|
|query_plan|**xml**|부분 통계를 포함 하 *plan_handle* 로 지정 된 쿼리 실행 계획의 런타임 실행 계획 표현을 포함 합니다. 실행 계획은 XML 형식입니다. 임시 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문, 저장 프로시저 호출, 사용자 정의 함수 호출 등이 포함된 각 일괄 처리에 대해 계획 하나가 생성됩니다. Null을 허용합니다.|

## <a name="remarks"></a>설명
[Sys.dm_exec_query_statistics_xml](./sys-dm-exec-query-statistics-xml-transact-sql.md?view=sql-server-ver15) 에 동일한 설명이 적용 됩니다.   

## <a name="permissions"></a>사용 권한  
 서버에 대한 `VIEW SERVER STATE` 권한이 필요합니다.  

## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;SQL Data Warehouse 및 병렬 데이터 웨어하우스 동적 관리 뷰 ](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  

 ## <a name="next-steps"></a>다음 단계
 더 많은 개발 팁은 [SQL Data Warehouse 개발 개요](/azure/sql-data-warehouse/sql-data-warehouse-overview-develop)를 참조하세요.