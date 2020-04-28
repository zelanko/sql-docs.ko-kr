---
title: sys. dm_pdw_resource_waits (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 11/26/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a43ce9a2-5261-41e3-97f0-555ba05ebed9
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 46b1155878aae6cc7f667965cfae065ed1a9cacc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74564739"
---
# <a name="sysdm_pdw_resource_waits-transact-sql"></a>sys. dm_pdw_resource_waits (Transact-sql)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  의 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]모든 리소스 유형에 대 한 대기 정보를 표시 합니다.  
  
|열 이름|데이터 형식|설명|범위|  
|-----------------|---------------|-----------------|-----------|  
|wait_id|**bigint**|대기 목록에서 요청에 대 한 위치입니다.|0부터 기반으로 하는 서 수입니다. 이는 모든 대기 항목에서 고유 하지 않습니다.|  
|session_id|**nvarchar(32)**|대기 상태가 발생 한 세션의 ID입니다.|[Dm_pdw_exec_sessions &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)에서 session_id를 참조 하세요.|  
|type|**nvarchar(255)**|이 항목이 나타내는 대기 유형입니다.|가능한 값은 다음과 같습니다.<br /><br /> 연결<br /><br /> 로컬 쿼리 동시성<br /><br /> 분산 쿼리 동시성<br /><br /> DMS 동시성<br /><br /> 백업 동시성|  
|object_type|**nvarchar(255)**|대기의 영향을 받는 개체의 형식입니다.|가능한 값은 다음과 같습니다.<br /><br /> **개체가**<br /><br /> **DATABASE**<br /><br /> **컴퓨터**<br /><br /> **스키마**<br /><br /> **프로그램별**|  
|object_name|**nvarchar (386)**|대기의 영향을 받은 지정 된 개체의 이름 또는 GUID입니다.|테이블과 뷰는 세 부분으로 구성 된 이름으로 표시 됩니다.<br /><br /> 인덱스와 통계는 네 부분으로 구성 된 이름으로 표시 됩니다.<br /><br /> 이름, 보안 주체 및 데이터베이스는 문자열 이름입니다.|  
|request_id|**nvarchar(32)**|대기 상태가 발생 한 요청의 ID입니다.|요청의 QID 식별자입니다.<br /><br /> 로드 요청의 GUID 식별자입니다.|  
|request_time|**datetime**|잠금 또는 리소스가 요청 된 시간입니다.||  
|acquire_time|**datetime**|잠금 또는 리소스를 획득 한 시간입니다.||  
|state|**nvarchar(50)**|대기 상태의 상태입니다.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|priority|**int**|대기 중인 항목의 우선 순위입니다.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|concurrency_slots_used|**int**|내부|아래의 [모니터링 리소스 대기](#monitor-resource-waits) 를 참조 하세요.|  
|resource_class|**nvarchar (20)**|내부 |아래의 [모니터링 리소스 대기](#monitor-resource-waits) 를 참조 하세요.|  
  
## <a name="monitor-resource-waits"></a>리소스 대기 모니터링 
[작업 그룹](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-workload-isolation)의 도입으로 인해 더 이상 동시성 슬롯을 적용할 수 없습니다.  아래 쿼리 및 `resources_requested` 열을 사용 하 여 요청을 실행 하는 데 필요한 리소스를 이해 합니다.

```sql
select rw.wait_id
      ,rw.session_id
      ,rw.type
      ,rw.object_type
      ,rw.object_name
      ,rw.request_id
      ,rw.request_time
      ,rw.acquire_time
      ,rw.state
      ,resources_requested = s.effective_request_min_resource_grant_percent
      ,r.group_name
  from sys.dm_workload_management_workload_groups_stats s
  join sys.dm_pdw_exec_requests r on r.group_name = s.name collate SQL_Latin1_General_CP1_CI_AS
  join sys.dm_pdw_resource_waits rw on rw.request_id = r.request_id
```

## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;SQL Data Warehouse 및 병렬 데이터 웨어하우스 동적 관리 뷰](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
