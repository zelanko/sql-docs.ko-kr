---
description: sys.availability_groups(Transact-SQL)
title: sys. availability_groups (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.availability_groups_TSQL
- availability_groups_TSQL
- sys.availability_groups
- availability_groups
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.availability_groups catalog view
ms.assetid: da7fa55f-c008-45d9-bcfc-3513b02d9e71
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9d68c407a7a9e34cf5362f34e749f414a99130bd
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537520"
---
# <a name="sysavailability_groups-transact-sql"></a>sys.availability_groups(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  SQL Server의 로컬 인스턴스에서 가용성 복제본을 호스트하는 각 가용성 그룹에 대해 하나의 행을 반환합니다. 각 행에는 가용성 그룹 메타데이터의 캐시된 복사본이 포함됩니다.  
   
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|가용성 그룹의 GUID(Globally Unique Identifier)입니다.|  
|**name**|**sysname**|가용성 그룹의 이름으로, WSFC(Windows Server 장애 조치(failover) 클러스터) 내에서 고유해야 하는 사용자 지정 이름입니다.|  
|**resource_id**|**nvarchar(40)**|WSFC 클러스터 리소스의 리소스 ID입니다.|  
|**resource_group_id**|**nvarchar(40)**|가용성 그룹의 WSFC 클러스터 리소스 그룹에 대한 리소스 그룹 ID입니다.|  
|**failure_condition_level**|**int**|자동 장애 조치 (failover)를 트리거해야 하는 사용자 정의 오류 조건 수준으로,이 테이블 바로 아래 표에 표시 된 정수 값 중 하나입니다.<br /><br /> 오류 상태 수준(1–5)의 범위는 가장 낮은 제한 수준 1에서 가장 높은 제한 수준 5까지입니다. 특정 상태 수준은 그보다 낮은 모든 제한 수준을 포함합니다. 따라서 가장 엄격한 상태 수준 5에는 그보다 낮은 네 개의 제한 상태 수준(1~4)이 포함되고, 수준 4에는 수준 1~3이 포함됩니다.<br /><br /> 이 값을 변경 하려면 [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) 문의 FAILURE_CONDITION_LEVEL 옵션을 사용 합니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] .|  
|**health_check_timeout**|**int**|서버 인스턴스가 느리거나 응답 하지 않는 것으로 간주 되기 전에 [sp_server_diagnostics](../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) 시스템 저장 프로시저에서 서버 상태 정보를 반환 하는 대기 시간 (밀리초)입니다. 기본값은 30000밀리초(30초)입니다.<br /><br /> 이 값을 변경 하려면 [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) 문의 HEALTH_CHECK_TIMEOUT 옵션을 사용 합니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] .|  
|**automated_backup_preference**|**tinyint**|이 가용성 그룹의 가용성 데이터베이스에서 백업을 수행하기 위한 기본 위치입니다. 다음은 가능한 값과 그에 대 한 설명입니다.<br /><br /> <br /><br /> 0: 기본 백업이 항상 주 복제본에서만 수행됩니다.<br /><br /> 1: 보조만 해당 합니다. 기본적으로 보조 복제본에서 백업을 수행합니다.<br /><br /> 2: 보조를 선호 합니다. 기본적으로 보조 복제본에서 백업을 수행하지만, 보조 복제본을 백업 작업에 사용할 수 없는 경우에는 주 복제본에서 백업을 수행합니다. 기본 동작입니다.<br /><br /> 3: 모든 복제본. 백업이 주 복제본에서 수행되는지 보조 복제본에서 수행되는지에 대한 기본 설정이 없습니다.<br /><br /> <br /><br /> 자세한 내용은 [활성 보조 복제본: 보조 복제본에 백업&#40;Always On 가용성 그룹&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)을 참조하세요.|  
|**automated_backup_preference_desc**|**nvarchar(60)**|**Automated_backup_preference**에 대 한 설명 이며 다음 중 하나입니다.<br /><br /> PRIMARY<br /><br /> SECONDARY_ONLY<br /><br /> SECONDARY<br /><br /> 없음|  
|**version**|**smallint**|Windows 장애 조치 (Failover) 클러스터에 저장 된 가용성 그룹 메타 데이터의 버전입니다. 이 버전 번호는 새 기능이 추가 될 때 증가 합니다.|  
|**basic_features**|**bit**|기본 가용성 그룹 인지 여부를 지정 합니다. 자세한 내용은 [기본 가용성 그룹&#40;Always On 가용성 그룹&#41;](../../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md)을 참조하세요.|  
|**dtc_support**|**bit**|이 가용성 그룹에 대해 DTC 지원을 사용할 수 있는지 여부를 지정 합니다. **CREATE AVAILABILITY GROUP** 의 **DTC_SUPPORT** 옵션은이 설정을 제어 합니다.|  
|**db_failover**|**bit**|가용성 그룹에서 데이터베이스 상태에 대 한 장애 조치 (failover)를 지원 하는지 여부를 지정 합니다. **CREATE AVAILABILITY GROUP** 의 **DB_FAILOVER** 옵션은이 설정을 제어 합니다.|  
|**is_distributed**|**bit**|분산 가용성 그룹 인지 여부를 지정 합니다. 자세한 내용은 [분산된 가용성 그룹&#40;Always On 가용성 그룹&#41;](../../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md)을 참조하세요.|
|**cluster_type**|**tinyint**|0: Windows Server 장애 조치 (failover) 클러스터 <br/><br/>1: 외부 클러스터 (예: Linux Pacemaker)<br/><br/>2: 없음|
|**cluster_type_desc**|**nvarchar(60)**|클러스터 유형에 대 한 텍스트 설명|
|**required_synchronized_secondaries_to_commit**|**int**| 커밋이 완료 되려면 동기화 된 상태 여야 하는 보조 복제본의 수입니다.|
|**sequence_number**|**bigint**|가용성 그룹 구성 시퀀스를 식별 합니다. 가용성 그룹 주 복제본이 그룹의 구성을 업데이트할 때마다 점진적으로 증가 합니다.|
|**is_contained**|**bit**|1: 고가용성을 위해 구성 된 빅 데이터 클러스터 마스터 인스턴스입니다. <br/><br/> 0: 다른 모든.|
  
## <a name="failure-condition-level--values"></a>오류 조건 수준 값  
 다음 표에서는 **failure_condition_level** 열에 대 한 가능한 오류 조건 수준을 설명 합니다.  
  
|값|오류 조건|  
|-----------|-----------------------|  
|1|다음과 같은 경우 자동 장애 조치(failover)를 시작하도록 지정합니다.<br /><br /> <br /><br /> - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스가 다운 되었습니다.<br /><br /> -서버 인스턴스에서 ACK를 받지 못해 WSFC 장애 조치 (failover) 클러스터에 연결 하기 위한 가용성 그룹의 임대가 만료 됩니다. 자세한 내용은 [작동 방법: SQL Server Always On 임대 시간 제한](https://techcommunity.microsoft.com/t5/sql-server-support/how-it-works-sql-server-alwayson-lease-timeout/ba-p/317268)을 참조하세요.|  
|2|다음과 같은 경우 자동 장애 조치(failover)를 시작하도록 지정합니다.<br /><br /> <br /><br /> -인스턴스가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클러스터에 연결 되어 있지 않고 가용성 그룹의 사용자 지정 **health_check_timeout** 임계값이 초과 되었습니다.<br /><br /> -가용성 복제본이 실패 상태에 있습니다.|  
|3|분리된 spinlock, 중대한 쓰기 액세스 위반 또는 과도한 덤프와 같이 심각한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내부 오류가 발생할 경우 자동 장애 조치(failover)를 시작하도록 지정합니다.<br /><br /> 이것은 기본값입니다.|  
|4|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내부 리소스 풀에서 지속적인 메모리 부족 상태와 같은 일반적인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내부 오류가 발생할 경우 자동 장애 조치(failover)를 시작하도록 지정합니다.|  
|5|다음과 같은 오류 상태가 발생할 경우 자동 장애 조치(failover)를 시작하도록 지정합니다.<br /><br /> <br /><br /> -SQL 엔진 작업자 스레드가 고갈 되었습니다.<br /><br /> -해결할 수 없는 교착 상태를 검색 합니다.|  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 서버 인스턴스에 대한 VIEW  ANY  DEFINITION  권한이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [sys.availability_replicas&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)   
 [Always On 가용성 그룹&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Transact-sql&#41;&#40;가용성 그룹 모니터링 ](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [가용성 그룹 모니터링&#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
