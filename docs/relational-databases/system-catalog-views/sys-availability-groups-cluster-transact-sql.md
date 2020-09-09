---
description: sys.availability_groups_cluster(Transact-SQL)
title: sys. availability_groups_cluster (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.availability_groups_cluster
- availability_groups_cluster
- availability_groups_cluster_TSQL
- sys.availability_groups_cluster_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.availability_groups_cluster catalog view
- Availability Groups [SQL Server], WSFC clusters
ms.assetid: d0f4683f-cdf0-4227-8b68-720ffe58f158
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 26a33fd75d392ea847fd2e27aa8dde6166e10bca
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537510"
---
# <a name="sysavailability_groups_cluster-transact-sql"></a>sys.availability_groups_cluster(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  WSFC(Windows Server 장애 조치(Failover) 클러스터링)의 각 Always On 가용성 그룹에 대해 하나의 행을 반환합니다. 각 행에는 WSFC 클러스터의 가용성 그룹 메타데이터가 포함됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|가용성 그룹의 GUID(Globally Unique Identifier)입니다.|  
|**name**|**sysname**|가용성 그룹의 이름으로, WSFC(Windows Server 장애 조치(failover) 클러스터) 내에서 고유해야 하는 사용자 지정 이름입니다.|  
|**resource_id**|**nvarchar(40)**|WSFC 클러스터 리소스의 리소스 ID입니다.|  
|**resource_group_id**|**nvarchar(40)**|가용성 그룹의 WSFC 클러스터 리소스 그룹에 대한 리소스 그룹 ID입니다.|  
|**failure_condition_level**|**int**|자동 장애 조치(failover)가 트리거되어야 하는 사용자 정의 오류 상태 수준으로, 다음 정수 값 중 하나입니다.<br /><br /> 1: 다음 중 하나가 발생할 때 자동 장애 조치 (failover)를 시작 하도록 지정 합니다. <br />- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스가 다운 되었습니다.<br />-서버 인스턴스에서 ACK를 받지 못해 WSFC 장애 조치 (failover) 클러스터에 연결 하기 위한 가용성 그룹의 임대가 만료 됩니다. 자세한 내용은 [작동 방법: SQL Server Always On 임대 시간 제한](https://techcommunity.microsoft.com/t5/sql-server-support/how-it-works-sql-server-alwayson-lease-timeout/ba-p/317268)을 참조하세요.<br /><br /> 2: 다음 중 하나가 발생할 때 자동 장애 조치 (failover)를 시작 하도록 지정 합니다.  <br />-인스턴스가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클러스터에 연결 되어 있지 않고 가용성 그룹의 사용자 지정 **health_check_timeout** 임계값이 초과 되었습니다. <br />-가용성 복제본이 실패 상태에 있습니다. <br />3: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 분리 된 spinlock, 중대 한 쓰기 액세스 위반 또는 과도 한 덤프와 같은 중요 한 내부 오류에서 자동 장애 조치 (failover)를 시작 하도록 지정 합니다. 이것은 기본값입니다. <br />4: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내부 리소스 풀에서 지속적인 메모리 부족 상태와 같은 일반적인 내부 오류에 대해 자동 장애 조치 (failover)를 시작 하도록 지정 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br />5: 자동 장애 조치 (failover)를 다음을 비롯 한 모든 정규화 된 오류 상태에서 시작 하도록 지정 합니다.<br />-SQL 엔진 작업자 스레드가 고갈 되었습니다. <br />-해결할 수 없는 교착 상태를 검색 합니다.<br /><br /> 오류 상태 수준(1–5)의 범위는 가장 낮은 제한 수준 1에서 가장 높은 제한 수준 5까지입니다. 특정 상태 수준은 그보다 낮은 모든 제한 수준을 포함합니다. 따라서 가장 엄격한 상태 수준 5에는 그보다 낮은 네 개의 제한 상태 수준(1~4)이 포함되고, 수준 4에는 수준 1~3이 포함됩니다.<br /><br /> 이 값을 변경 하려면 [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) 문의 FAILURE_CONDITION_LEVEL 옵션을 사용 합니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] .|  
|**health_check_timeout**|**int**|서버 인스턴스가 느리거나 응답 하지 않는 것으로 간주 되기 전에 [sp_server_diagnostics](../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) 시스템 저장 프로시저에서 서버 상태 정보를 반환 하는 대기 시간 (밀리초)입니다. 기본값은 30000밀리초(30초)입니다.<br /><br /> 이 값을 변경 하려면 [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) 문의 HEALTH_CHECK_TIMEOUT 옵션을 사용 합니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] .|  
|**automated_backup_preference**|**tinyint**|이 가용성 그룹의 가용성 데이터베이스에서 백업을 수행하기 위한 기본 위치입니다. 다음 값 중 하나입니다.<br /><br /> 0: 기본 백업이 항상 주 복제본에서만 수행됩니다.<br />1: 보조만 해당 합니다. 기본적으로 보조 복제본에서 백업을 수행합니다.<br />2: 보조를 선호 합니다. 기본적으로 보조 복제본에서 백업을 수행하지만, 보조 복제본을 백업 작업에 사용할 수 없는 경우에는 주 복제본에서 백업을 수행합니다. 기본 동작입니다.<br />3: 모든 복제본. 백업이 주 복제본에서 수행되는지 보조 복제본에서 수행되는지에 대한 기본 설정이 없습니다.<br /><br /> 자세한 내용은 [활성 보조 복제본: 보조 복제본에 백업&#40;Always On 가용성 그룹&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)을 참조하세요.|  
|**automated_backup_preference_desc**|**nvarchar(60)**|**Automated_backup_preference**에 대 한 설명 이며 다음 중 하나입니다.<br /><br /> PRIMARY<br /><br /> SECONDARY_ONLY<br /><br /> SECONDARY<br /><br /> 없음|  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 서버 인스턴스에 대한 VIEW  ANY  DEFINITION  권한이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [sys.availability_replicas&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)   
 [Always On 가용성 그룹&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Transact-sql&#41;&#40;가용성 그룹 모니터링 ](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [가용성 그룹 모니터링&#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
