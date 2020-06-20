---
title: sys. workload_management_workload_groups (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 11/05/2019
ms.prod: sql
ms.technology: system-objects
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.topic: language-reference
dev_langs:
- TSQL
author: ronortloff
ms.author: rortloff
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: b103ff109c946262367467673da0bf9c8ef8f5eb
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85011432"
---
# <a name="sysworkload_management_workload_groups-transact-sql"></a>sys. workload_management_workload_groups (Transact-sql)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

 작업 그룹에 대 한 세부 정보를 반환 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|
|group_id|**int**|작업 그룹의 고유한 ID입니다. Null을 허용하지 않습니다.||
|name|**sysname**|작업 그룹의 이름입니다. 는 인스턴스에 대해 고유 해야 합니다.  Null을 허용하지 않습니다.||
|importance|**nvarchar(128)**|는이 작업 그룹의 요청에 대 한 상대적 중요도와 공유 리소스에 대 한 작업 그룹 전체에 해당 합니다. Null을 허용하지 않습니다.|낮음, below_normal, 보통 (기본값), above_normal, 높음||
|min_percentage_resource|**tinyint**|작업 그룹의 요청에 대해 보장 된 리소스의 양입니다. 리소스는 다른 작업 그룹과 공유 되지 않습니다. Null을 허용하지 않습니다.||
|cap_percentage_resource|**tinyint**|작업 그룹의 요청에 대 한 리소스 백분율 할당의 하드 캡. 지정 된 수준에 할당 된 최대 리소스를 제한 합니다. 허용되는 값의 범위는 1에서 100까지입니다.||
|request_min_resource_grant_percent|**decimal (5, 2)**|요청에 할당 된 리소스의 최소 크기를 지정 합니다. 허용 되는 값 범위는 0.75에서 100 까지입니다.||
|request_max_resource_grant_percent |**decimal (5, 2)**|요청에 할당 된 리소스의 최대 크기를 지정 합니다.||
|query_execution_timeout_sec|**int**|쿼리를 취소 하기 전에 허용 되는 실행 시간 (초)입니다.  실행의 반환 단계에 도달 하면 쿼리를 취소할 수 없습니다.  query_execution_timeout_sec에는 대기 하는 데 소요 된 시간이 포함 되지 않습니다.|
|query_wait_timeout_sec|**int**|INTERNAL||
|create_time|**datetime**|작업 그룹이 만들어진 시간입니다. Null을 허용하지 않습니다.||
modify_time|**datetime**|작업 그룹이 마지막으로 수정 된 시간입니다. Null을 허용하지 않습니다.||
|&nbsp;||||
  
## <a name="permissions"></a>사용 권한

VIEW SERVER STATE 권한이 필요합니다.

## <a name="next-steps"></a>다음 단계

 SQL Data Warehouse 및 병렬 데이터 웨어하우스의 모든 카탈로그 뷰 목록은 [SQL Data Warehouse 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)를 참조 하세요. 작업 그룹을 만들려면 [작업 그룹 만들기](../../t-sql/statements/create-workload-group-transact-sql.md)를 참조 하세요. 작업 분류에 대 한 자세한 내용은 [워크 로드 격리](/azure/sql-data-warehouse/sql-data-warehouse-workload-isolation) 를 참조 하세요.
