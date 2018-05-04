---
title: sys.dm_xe_session_targets (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_xe_session_targets
- dm_xe_session_targets_TSQL
- dm_xe_session_targets
- sys.dm_xe_session_targets_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xe_session_targets dynamic management view
- extended events [SQL Server], views
ms.assetid: 76fbc3e1-ad88-4a47-8bf1-471c3bee5ad8
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c175bb226f668ecf6d1f4b1935b6847f738cb929
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmxesessiontargets-transact-sql"></a>sys.dm_xe_session_targets(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  세션 대상에 대한 정보를 반환합니다.  
  
  |열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary(8)**|이벤트 세션의 메모리 주소입니다. sys.dm_xe_sessions.address와 다 대 일 관계를 갖습니다. Null을 허용하지 않습니다.|  
|target_name|**nvarchar(60)**|세션 내에 있는 대상의 이름입니다. Null을 허용하지 않습니다.|  
|target_package_guid|**uniqueidentifier**|대상이 포함된 패키지의 GUID입니다. Null을 허용하지 않습니다.|  
|execution_count|**bigint**|세션에 대해 대상이 실행된 횟수입니다. Null을 허용하지 않습니다.|  
|execution_duration_ms|**bigint**|대상이 실행된 총 시간(밀리초)입니다. Null을 허용하지 않습니다.|  
|target_data|**nvarchar(max)**|이벤트 집계 정보와 같이 대상에서 유지 관리하는 데이터입니다. Null을 허용합니다.|  
  
## <a name="permissions"></a>Permissions  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
### <a name="relationship-cardinalities"></a>관계 카디널리티  
  
|보낸 사람|수행할 작업|관계|  
|----------|--------|------------------|  
|sys.dm_xe_session_targets.event_session_address|sys.dm_xe_sessions.address|다 대 일|  
  
## <a name="change-history"></a>변경 내역  
  
|업데이트된 내용|  
|---------------------|  
|target_data 열의 데이터 형식을 수정했습니다.|  
|값이 Null을 허용함을 나타내기 위해 target_data 열의 설명을 수정했습니다.|  
|"관계 카디널리티" 표를 수정했습니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

