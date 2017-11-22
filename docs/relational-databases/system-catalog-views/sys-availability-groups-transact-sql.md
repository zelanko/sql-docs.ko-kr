---
title: sys.availability_groups (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.availability_groups_TSQL
- availability_groups_TSQL
- sys.availability_groups
- availability_groups
dev_langs: TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.availability_groups catalog view
ms.assetid: da7fa55f-c008-45d9-bcfc-3513b02d9e71
caps.latest.revision: "42"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d2d5deb9a29270c70e5f19b311889f2d6e1f8f48
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="sysavailabilitygroups-transact-sql"></a>sys.availability_groups(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  SQL Server의 로컬 인스턴스에 가용성 복제본을 호스팅하는 각 가용성 그룹에 대 한 행을 반환 합니다. 각 행에는 가용성 그룹 메타데이터의 캐시된 복사본이 포함됩니다.  
   
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|가용성 그룹의 GUID(Globally Unique Identifier)입니다.|  
|**name**|**sysname**|가용성 그룹의 이름으로, WSFC(Windows Server 장애 조치(failover) 클러스터) 내에서 고유해야 하는 사용자 지정 이름입니다.|  
|**resource_id**|**nvarchar (40)**|WSFC 클러스터 리소스의 리소스 ID입니다.|  
|**resource_group_id**|**nvarchar (40)**|가용성 그룹의 WSFC 클러스터 리소스 그룹에 대한 리소스 그룹 ID입니다.|  
|**failure_condition_level**|**int**|사용자 정의 오류 상태 수준은 자동 장애 조치를 트리거해야 하,이 테이블의 바로 아래 표에 표시 된 정수 값 중 하나입니다.<br /><br /> 오류 상태 수준(1–5)의 범위는 가장 낮은 제한 수준 1에서 가장 높은 제한 수준 5까지입니다. 특정 상태 수준은 그보다 낮은 모든 제한 수준을 포함합니다. 따라서 가장 엄격한 상태 수준 5에는 그보다 낮은 네 개의 제한 상태 수준(1~4)이 포함되고, 수준 4에는 수준 1~3이 포함됩니다.<br /><br /> 이 값을 변경 하려면 FAILURE_CONDITION_LEVEL 옵션을 사용 하 여는 [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] 문.|  
|**health_check_timeout**|**int**|에 대 한 대기 시간 (밀리초)는 [sp_server_diagnostics](../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) 시스템 저장 프로시저를 서버 인스턴스가 느리거나 중지 간주 하기 전에 서버 상태 정보를 반환 합니다. 기본값은 30000밀리초(30초)입니다.<br /><br /> 이 값을 변경 하려면 HEALTH_CHECK_TIMEOUT 옵션을 사용 하 여는 [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] 문.|  
|**automated_backup_preference**|**tinyint**|이 가용성 그룹의 가용성 데이터베이스에서 백업을 수행하기 위한 기본 위치입니다. 가능한 값 및 해당 설명을 보려면은 다음과 같습니다.<br /><br /> <br /><br /> 0: 기본 합니다. 백업이 항상 주 복제본에서만 수행됩니다.<br /><br /> 1: 보조만. 기본적으로 보조 복제본에서 백업을 수행합니다.<br /><br /> 2: 보조 사용 합니다. 기본적으로 보조 복제본에서 백업을 수행하지만, 보조 복제본을 백업 작업에 사용할 수 없는 경우에는 주 복제본에서 백업을 수행합니다. 이것이 기본 동작입니다.<br /><br /> 3: 임의의 복제본. 백업이 주 복제본에서 수행되는지 보조 복제본에서 수행되는지에 대한 기본 설정이 없습니다.<br /><br /> <br /><br /> 자세한 내용은 [활성 보조: 보조 복제본에 백업&#40;Always On 가용성 그룹&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)을 참조하세요.|  
|**automated_backup_preference_desc**|**nvarchar (60)**|에 대 한 설명 **automated_backup_preference**이며 다음 중 하나입니다.<br /><br /> PRIMARY<br /><br /> SECONDARY_ONLY<br /><br /> SECONDARY<br /><br /> 없음|  
|**version**|**smallint**|Windows 장애 조치 클러스터에 저장 된 가용성 그룹 메타 데이터의 버전입니다. 새 기능을 추가 하는 경우이 버전 번호가 증가 합니다.|  
|**basic_features**|**bit**|기본 가용성 그룹 인지 여부를 지정 합니다. 자세한 내용은 참조 [기본 가용성 그룹 &#40; Always On 가용성 그룹 &#41; ](../../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md).|  
|**dtc_support**|**bit**|이 가용성 그룹에 대 한 DTC 지원이 사용 여부를 지정 합니다. **DTC_SUPPORT** 옵션의 **CREATE AVAILABILITY GROUP** 이 설정을 제어 합니다.|  
|**db_failover**|**bit**|가용성 그룹 데이터베이스 상태 조건에 대 한 장애 조치를 지원 하는지 여부를 지정 합니다. **DB_FAILOVER** 옵션의 **CREATE AVAILABILITY GROUP** 이 설정을 제어 합니다.|  
|**is_distributed**|**bit**|분산형된 가용성 그룹 인지 여부를 지정 합니다. 자세한 내용은 [분산된 가용성 그룹&#40;Always On 가용성 그룹&#41;](../../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md)을 참조하세요.|  
  
## <a name="failure-condition-level--values"></a>실패 조건 수준 값  
 다음 표에서 가능한 실패 조건 수준에 대 한 설명의 **failure_condition_level** 열입니다.  
  
|값|오류 상태|  
|-----------|-----------------------|  
|1.|다음과 같은 경우 자동 장애 조치(failover)를 시작하도록 지정합니다.<br /><br /> <br /><br /> - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스가 중지 되었습니다.<br /><br /> -WSFC 장애 조치 클러스터에 연결 하기 위한 가용성 그룹의 임대가 서버 인스턴스로부터 ACK를 받지 못해 만료 됩니다. 자세한 내용은 [작동 방법: SQL Server Always On 임대 시간 제한](http://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-Always%20On-lease-timeout.aspx)을 참조하세요.|  
|2|다음과 같은 경우 자동 장애 조치(failover)를 시작하도록 지정합니다.<br /><br /> <br /><br /> -인스턴스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 되어 있지 않고 클러스터 및 사용자 지정 **health_check_timeout** 가용성 그룹의 임계값을 초과 합니다.<br /><br /> -가용성 복제본이 실패 상태입니다.|  
|3|분리된 spinlock, 중대한 쓰기 액세스 위반 또는 과도한 덤프와 같이 심각한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내부 오류가 발생할 경우 자동 장애 조치(failover)를 시작하도록 지정합니다.<br /><br /> 이 값은 기본값입니다.|  
|4|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내부 리소스 풀에서 지속적인 메모리 부족 상태와 같은 일반적인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내부 오류가 발생할 경우 자동 장애 조치(failover)를 시작하도록 지정합니다.|  
|5|다음과 같은 오류 상태가 발생할 경우 자동 장애 조치(failover)를 시작하도록 지정합니다.<br /><br /> <br /><br /> -SQL 엔진 작업자 스레드가 소진 된 경우<br /><br /> -해결할 수 없는 교착 상태가 발견 된 합니다.|  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>Permissions  
 서버 인스턴스에 대한 VIEW  ANY  DEFINITION  권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sys.availability_replicas&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)   
 [Always On 가용성 그룹&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [가용성 그룹 모니터링&#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [가용성 그룹 모니터링&#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
