---
title: sys.dm_pdw_resource_waits (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
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
ms.openlocfilehash: 35868774efc7083b835bb6f44b6c71cbffc7ae2c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67899207"
---
# <a name="sysdmpdwresourcewaits-transact-sql"></a>sys.dm_pdw_resource_waits (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  표시에서 모든 리소스 유형에 대 한 정보를 대기 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]합니다.  
  
|열 이름|데이터 형식|설명|범위|  
|-----------------|---------------|-----------------|-----------|  
|wait_id|**bigint**|대기 목록에서 위치 요청입니다.|0부터 시작 서 수입니다. 이 고유 하지 않습니다 모든 대기 항목.|  
|session_id|**nvarchar(32)**|대기 상태에서 발생 한 세션의 ID입니다.|Session_id를 참조 하세요 [sys.dm_pdw_exec_sessions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)합니다.|  
|type|**nvarchar(255)**|이 항목을 나타내는 대기 유형입니다.|가능한 값:<br /><br /> 연결<br /><br /> 로컬 쿼리 동시성<br /><br /> 분산된 쿼리 동시성<br /><br /> DMS 동시성<br /><br /> 백업 동시성|  
|object_type|**nvarchar(255)**|대기 영향을 받는 개체의 형식입니다.|가능한 값:<br /><br /> **OBJECT**<br /><br /> **DATABASE**<br /><br /> **SYSTEM**<br /><br /> **SCHEMA**<br /><br /> **응용 프로그램**|  
|object_name|**nvarchar(386)**|이름 또는 영향을 받은 대기 지정된 된 개체의 GUID입니다.|테이블 및 뷰는 세 부분으로 된 이름을 사용 하 여 표시 됩니다.<br /><br /> 인덱스와 통계는 네 부분으로 된 이름으로 표시 됩니다.<br /><br /> 이름, 주체 및 데이터베이스는 문자열 이름입니다.|  
|request_id|**nvarchar(32)**|대기 상태에서 발생 한 요청의 ID입니다.|QID 요청의 식별자입니다.<br /><br /> 로드 요청에 대 한 GUID 식별자입니다.|  
|request_time|**datetime**|잠금 또는 리소스를 요청한 시간입니다.||  
|acquire_time|**datetime**|잠금 또는 리소스를 획득 하는 시간입니다.||  
|state|**nvarchar(50)**|대기 상태의 상태입니다.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|priority|**int**|대기 중인 항목의 우선 순위입니다.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|concurrency_slots_used|**int**|이 요청에 대 한 예약 된 동시성 슬롯 수 (최대 32)의 수입니다.|1-SmallRC<br /><br /> 3-MediumRC<br /><br /> LargeRC 7<br /><br /> XLargeRC에 대 한 22-|  
|resource_class|**nvarchar(20)**|이 요청에 대 한 리소스 클래스입니다.|SmallRC<br /><br /> MediumRC<br /><br /> LargeRC<br /><br /> XLargeRC|  
  
## <a name="see-also"></a>관련 항목  
 [SQL Data Warehouse 및 병렬 데이터 웨어하우스 동적 관리 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
