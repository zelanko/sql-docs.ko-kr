---
description: sys.dm_database_copies(Azure SQL Database)
title: sys.dm_database_copies (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- dm_database_copies_TSQL
- sys.dm_database_copies
- dm_database_copies
- sys.dm_database_copies_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dm_database_copies
- sys.dm_database_copies
ms.assetid: d03d4657-86d1-4496-97e6-cc3bc292e0b1
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: acdb347af36812095df03f61ae9f118493496e51
ms.sourcegitcommit: b3a711a673baebb2ff10d7142b209982b46973ae
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2020
ms.locfileid: "93364775"
---
# <a name="sysdm_database_copies-azure-sql-database"></a>sys.dm_database_copies(Azure SQL Database)
[!INCLUDE[Azure SQL Database](../../includes/applies-to-version/asdb.md)]

  데이터베이스 복사본에 대한 정보를 반환합니다.  
  
지역에서 복제 링크에 대 한 정보를 반환 하려면 [sys.geo_replication_links](../../relational-databases/system-dynamic-management-views/sys-geo-replication-links-azure-sql-database.md) 또는 [sys.dm_geo_replication_link_status](../../relational-databases/system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md) 뷰 (SQL Database V12에서 사용 가능)를 사용 합니다.
  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|`sys.databases` 뷰의 현재 데이터베이스 ID입니다.|  
|**start_date**|**datetimeoffset**|지역의 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 데이터 센터에서 데이터베이스 복사가 시작된 UTC 시간입니다.|  
|**modify_date**|**datetimeoffset**|지역의 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 데이터 센터에서 데이터베이스 복사가 완료된 UTC 시간입니다. 새 데이터베이스는 현 시점에서 주 데이터베이스와 트랜잭션 일관성이 유지됩니다. 완료 정보는 1 분 마다 업데이트 됩니다.<br /><br />Percent_complete 필드의 마지막 업데이트를 반영 하는 UTC 시간입니다.|  
|**percent_complete**|**real**|복사된 바이트의 백분율입니다. 값은 0에서 100 사이입니다. [!INCLUDE[ssSDS](../../includes/sssds-md.md)]는 자동으로 장애 조치와 같은 몇 가지 오류에서 복구하고 데이터베이스 복사를 다시 시작 수 있습니다. 이 경우 percent_complete는 0에서 다시 시작합니다.|  
|**error_code**|**int**|복사하는 동안 발생한 오류를 나타내는 코드 0보다 큰 경우. 오류가 발생하지 않은 경우 값은 0과 같습니다.|  
|**error_desc**|**nvarchar (4096)**|복사하는 동안 발생한 오류에 대한 설명입니다.|  
|**error_severity**|**int**|데이터베이스 복사가 실패한 경우 16을 반환합니다.|  
|**error_state**|**int**|복사가 실패한 경우 1을 반환합니다.|  
|**copy_guid**|**uniqueidentifier**|복사 작업의 고유 ID입니다.|  
|**partner_server**|**sysname**|복사본이 생성 되는 SQL Database 서버의 이름입니다.|  
|**partner_database**|**sysname**|파트너 서버의 데이터베이스 복사본 이름입니다.|  
|**replication_state**|**tinyint**|이 데이터베이스에 대 한 연속 복사 복제 상태입니다. 값:<br /><br /> 0 = 보류 중. 데이터베이스 복사본 만들기가 예약 되었지만 필요한 준비 단계가 아직 완료 되지 않았거나 시드 할당량에 의해 일시적으로 차단 되었습니다.<br /><br /> 1 = 시드 시드 중인 복사 데이터베이스가 아직 원본 데이터베이스와 완전히 동기화 되지 않았습니다. 이 상태에서는 복사본에 연결할 수 없습니다. 진행 중인 시드 작업을 취소 하려면 복사 데이터베이스를 삭제 해야 합니다.|  
|**replication_state_desc**|**nvarchar(256)**|replication_state에 대한 설명으로, 다음 중 하나입니다.<br /><br /> PENDING<br /><br /> SEEDING<br />|  
|**maximum_lag**|**int**|예약된 필드입니다.|  
|**is_continuous_copy**|**bit**|0 = 0을 반환 합니다.|  
|**is_target_role**|**bit**|0 = 원본 데이터베이스<br /><br /> 1 = 데이터베이스 복사|  
|**is_interlink_connected**|bit|예약된 필드입니다.|  
|**is_offline_secondary**|bit|예약된 필드입니다.|  
  
## <a name="permissions"></a>사용 권한  
 이 뷰는 **master** 데이터베이스에서 서버 수준 보안 주체 로그인에 대해서만 사용할 수 있습니다.  
  
## <a name="remarks"></a>설명  
 원본 또는 대상 서버의 **master** 데이터베이스에서 **sys.dm_database_copies** 뷰를 사용할 수 있습니다 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] . 데이터베이스 복사가 성공적으로 완료 되 고 새 데이터베이스가 온라인 상태가 되 면 **sys.dm_database_copies** 보기의 행이 자동으로 제거 됩니다.  
  
  
