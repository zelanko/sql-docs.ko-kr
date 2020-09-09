---
description: sys.availability_group_listeners(Transact-SQL)
title: sys. availability_group_listeners (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- availability_group_listeners_TSQL
- sys.availability_group_listeners
- sys.availability_group_listeners_TSQL
- availability_group_listeners
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.availability_group_listeners catalog view
- Availability Groups [SQL Server], listeners
ms.assetid: b5e7d1fb-3ffb-4767-8135-604c575016b1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 029f407b453dd4667fd888bbd1351a718173d9cf
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89550537"
---
# <a name="sysavailability_group_listeners-transact-sql"></a>sys.availability_group_listeners(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  각 Always On 가용성 그룹에 대해 0개의 행을 반환하여 가용성 그룹에 연결된 네트워크 이름이 없음을 나타내거나 WSFC(Windows Server 장애 조치(Failover) 클러스터링) 클러스터의 각 가용성 그룹 수신기 구성에 대해 하나의 행을 반환합니다. 이 뷰에는 클러스터에서 수집되는 실시간 구성이 표시됩니다.  
  
> [!NOTE]  
>  이 카탈로그 뷰는 WSFC 클러스터에 정의된 IP 구성을 자세히 설명하지 않습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|[Availability_groups](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)의 가용성 그룹 ID (**group_id**)입니다.|  
|**listener_id**|**nvarchar (36)**|클러스터 리소스 ID의 GUID입니다.|  
|**dns_name**|**nvarchar (63)**|가용성 그룹 수신기에 대해 구성된 네트워크 이름(호스트 이름)입니다.|  
|**port**|**int**|가용성 그룹 수신기에 대해 구성된 TCP 포트 번호입니다.<br /><br /> NULL = 수신기가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 외부에 구성되어서 포트 번호가 가용성 그룹에 추가되지 않았습니다. 포트를 추가 하려면 [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) 문의 MODIFY LISTENER 옵션을 pleaseuse [!INCLUDE[tsql](../../includes/tsql-md.md)] .|  
|**is_conformant**|**bit**|이 IP 구성이 규칙에 부합하는지 여부를 나타내며 다음 중 하나입니다.<br /><br /> 1 = 수신기가 규칙에 부합함. IP (인터넷 프로토콜) 주소 사이에는 "OR" 관계가 있습니다. *규칙* 은 [CREATE AVAILABILITY GROUP](../../t-sql/statements/create-availability-group-transact-sql.md) 문에 의해 만들어진 모든 IP 구성을 포함 [!INCLUDE[tsql](../../includes/tsql-md.md)] 합니다. 예를 들어 WSFC 장애 조치(Failover) 클러스터 관리자를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 외부에서 만든 IP 구성을 ALTER AVAILABILITY GROUP tsql 문을 사용하여 수정할 수 있는 경우에도 IP 구성은 규칙에 부합하는 것으로 한정됩니다.<br /><br /> 0 = 수신기가 규칙에 부합하지 않음. 일반적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 명령을 사용하여 구성할 수 없고 WSFC 클러스터 내에서 직접 정의된 IP 주소를 나타냅니다.|  
|**ip_configuration_string_from_cluster**|**nvarchar(max)**|이 수신기에 대한 클러스터 IP 구성 문자열(있는 경우)입니다. NULL = 수신기에 가상 IP 주소가 없음. 예를 들면 다음과 같습니다.<br /><br /> IPv4  `65.55.39.10` 주소:<br /><br /> IPv6 주소:  `2001::4898:23:1002:20f:1fff:feff:b3a3`|  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 동적 관리 뷰 및 함수 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [AlwaysOn 가용성 그룹 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Transact-sql&#41;&#40;가용성 그룹 모니터링 ](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Always On 가용성 그룹&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
