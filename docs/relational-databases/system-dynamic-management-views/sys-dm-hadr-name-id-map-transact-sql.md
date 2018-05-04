---
title: sys.dm_hadr_name_id_map (Transact SQL) | Microsoft Docs
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
- sys.dm_hadr_name_id_map
- sys.dm_hadr_name_id_map_TSQL
- dm_hadr_name_id_map
- dm_hadr_name_id_map_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_hadr_name_id_map dynamic management view
ms.assetid: e07bb8a9-37de-4a39-a257-950d7c3ae8fb
caps.latest.revision: 8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 69b1fd2e09b4f7c13540928328e4d5ca0697a530
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmhadrnameidmap-transact-sql"></a>sys.dm_hadr_name_id_map(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Always On 가용성 그룹의 매핑의 보여 줍니다의 현재 인스턴스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 세 가지 고유한 Id에 조인 된: 가용성 그룹 ID, WSFC 리소스 ID 및 WSFC 그룹 id입니다. 이 매핑의 목적은 WSFC 리소스/그룹의 이름이 바뀐 시나리오를 처리하기 위한 것입니다.  
   
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**ag_name**|**nvarchar(256)**|가용성 그룹의 이름으로, WSFC(Windows Server 장애 조치(Failover) 클러스터) 클러스터 내에서 고유해야 하는 사용자 지정 이름입니다.|  
|**ag_id**|**uniqueidentifier**|가용성 그룹의 GUID(Globally Unique Identifier)입니다.|  
|**ag_resource_id**|**nvarchar(256)**|가용성 그룹의 고유 ID를 WSFC 클러스터의 리소스로 나타낸 것입니다.|  
|**ag_group_id**|**nvarchar(256)**|가용성 그룹의 WSFC 그룹 ID입니다.|  
  
## <a name="permissions"></a>Permissions  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Always On 가용성 그룹 동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [AlwaysOn 가용성 그룹 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [가용성 그룹 모니터링 & #40; Transact SQL & #41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Always On 가용성 그룹&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
