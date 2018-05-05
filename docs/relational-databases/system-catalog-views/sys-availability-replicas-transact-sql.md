---
title: sys.availability_replicas (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- availability_replicas_TSQL
- availability_replicas
- sys.availability_replicas
- sys.availability_replicas_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.availability_replicas catalog view
ms.assetid: 0a06e9b6-a1e4-4293-867b-5c3f5a8ff62c
caps.latest.revision: 62
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 016a65e7606e43ec0eb567b7a4e17f07fd2d950f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sysavailabilityreplicas-transact-sql"></a>sys.availability_replicas(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

각 WSFC 장애 조치 클러스터의 Always On 가용성 그룹에 속해 있는 가용성 복제본에 대 한 행을 반환 합니다.  
  
클러스터가 다운되거나 쿼럼이 손실되는 등의 이유로 로컬 서버 인스턴스에서 WSFC  장애 조치(failover)  클러스터에 연결할 수 없는 경우에는 로컬 가용성 복제본에 대한 행만 반환됩니다. 이러한 행에는 메타데이터에 로컬로 캐시된 데이터의 열만 포함됩니다.  
  
 
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**replica_id**|**uniqueidentifier**|복제본의 고유 ID입니다.|  
|**group_id**|**uniqueidentifier**|복제본이 속한 가용성 그룹의 고유 ID입니다.|  
|**replica_metadata_id**|**int**|데이터베이스 엔진에서 가용성 복제본의 로컬 메타데이터 개체를 나타내는 ID입니다.|  
|**replica_server_name**|**nvarchar(256)**|이 복제본을 호스팅하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 서버 이름(기본 인스턴스가 아닌 경우에는 인스턴스 이름)입니다.|  
|**owner_sid**|**varbinary(85)**|이 가용성 복제본의 외부 소유자에 대해 이 서버 인스턴스에 등록된 SID(보안 ID)입니다.<br /><br /> 로컬이 아닌 가용성 복제본의 경우에는 NULL입니다.|  
|**endpoint_url**|**nvarchar(128)**|데이터 동기화를 위해 주 복제본과 보조 복제본 간의 연결에 사용되는 사용자 지정 데이터베이스 미러링 끝점의 문자열 표현입니다. 끝점 URL의 구문에 대한 자세한 내용은 [가용성 복제본 추가 또는 수정 시 끝점 URL 지정&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)을 참조하세요.<br /><br /> NULL  =  WSFC  장애 조치(failover)  클러스터와 통신할 수 없습니다.<br /><br /> 이 끝점을 변경 하려면 ENDPOINT_URL 옵션을 사용 하 여 [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] 문.|  
|**availability_mode**|**tinyint**|복제본의 가용성 모드로,  다음 중 하나입니다.<br /><br /> 0 &#124; 비동기 커밋입니다. 주 복제본은 보조 복제본이 로그를 디스크에 쓸 때까지 기다리지 않고 트랜잭션을 커밋할 수 있습니다.<br /><br /> 1 &#124; 동기 커밋입니다. 주 복제본은 보조 복제본이 트랜잭션을 디스크에 쓸 때까지 기다렸다가 지정된 트랜잭션을 커밋합니다.<br /><br />4 &#124; 만 구성 합니다. 주 복제본 가용성 그룹 구성 메타 데이터는를 복제본에 보내는 동기적으로 처리 합니다. 사용자 데이터의 복제본에 전송 되지 않습니다. SQL Server 2017 c u 1에서 이동 하 고 나중에 사용할 수 있습니다.<br /><br /> 자세한 내용은 [가용성 모드&#40;Always On 가용성 그룹&#41;](../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)라는 프로세스에서 서로 바꿀 수 있습니다.|  
|**availability_mode_desc**|**nvarchar(60)**|에 대 한 설명 **가용성\_모드**이며 다음 중 하나입니다.<br /><br /> 비동기\_커밋<br /><br /> 동기\_커밋<br /><br /> 구성\_전용<br /><br /> 이 가용성 복제본의 가용성 모드를 변경 하려면 AVAILABILITY_MODE 옵션을 사용 하 여 [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] 문.<br/><br>구성 된 복제본의 가용성 모드를 변경할 수 없습니다\_전용입니다. 구성을 변경할 수 없는\_전용 복제본을 주 또는 보조 복제본으로 합니다. |  
|**failover\_mode**|**tinyint**|[장애 조치 모드](../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md) 중 하나는 가용성 복제본의:<br /><br /> 0 &#124; 수동 장애 조치 합니다. 수동 장애 조치(failover)로 설정된 보조 복제본에 대한 장애 조치(failover)를 데이터베이스 관리자가 수동으로 시작해야 합니다. 수행되는 장애 조치(failover)의 유형은 다음과 같이 보조 복제본이 동기화되는지 여부에 따라 달라집니다.<br /><br /> 가용성 복제본이 동기화되고 있지 않거나 아직 동기화 중인 경우 데이터가 손실될 수 있는 강제 장애 조치(failover)만 발생할 수 있습니다.<br /><br /> 가용성 모드가 동기 커밋으로 설정 되어 있으면 (**가용성\_모드** = 1) 데이터 손실이 발생할 수 없는 가용성 복제본이 현재 동기화 된 수동 장애 조치 합니다.<br /><br /> 1 &#124; 자동 장애 조치 합니다. 복제본이 자동 장애 조치(failover)의 잠재적인 대상입니다.  가용성 모드가 동기 커밋으로 설정 된 경우에 자동 장애 조치가 지원 됩니다 (**가용성\_모드** = 1) 및 가용성 복제본이 현재 동기화 합니다.<br /><br /> 가용성 복제본의 모든 가용성 데이터베이스의 데이터베이스 동기화 상태 롤업을 보려면에서 사용 하 여는 **동기화\_상태** 및 **동기화\_상태\_desc** 의 열은 [sys.dm_hadr_availability_replica_states](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql.md) 동적 관리 뷰. 롤업에서는 모든 가용성 데이터베이스의 동기화 상태와 해당 가용성 복제본의 가용성 모드를 고려합니다.<br /><br /> **참고:** 지정된 된 가용성 데이터베이스의 동기화 상태를 보려면 쿼리는 **동기화\_상태** 및 **동기화\_상태** 열은 [sys.dm_hadr_database_replica_states](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) 동적 관리 뷰.|  
|**failover\_mode\_desc**|**nvarchar(60)**|에 대 한 설명 **장애 조치\_모드**이며 다음 중 하나입니다.<br /><br /> MANUAL<br /><br /> AUTOMATIC<br /><br /> 장애 조치 모드를 변경 하려면 장애 조치를 사용 하 여\_모드 옵션의 [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] 문.|  
|**session\_timeout**|**int**|제한 시간(초)입니다. 제한 시간은 복제본이 주 복제본과 보조 복제본 간의 연결이 실패한 것으로 간주하기 전에 복제본에서 다른 복제본의 메시지를 받기 위해 기다리는 최대 시간입니다. 세션 제한 시간은 보조 복제본이 주 복제본에 연결되어 있는지 여부를 검색합니다.<br /><br /> 주 복제본에서 보조 복제본과의 실패 한 연결 검색 하 고, 해제 되도록 보조 복제본을 고려\_SYNCHRONIZED 합니다. 주 복제본과의 실패한 연결을 검색할 경우 보조 복제본에서는 단순히 다시 연결을 시도합니다.<br /><br /> **참고:** 세션 제한 시간은 자동 장애 조치가 발생 하지 않습니다.<br /><br /> 이 값을 변경 하려면 SESSION_TIMEOUT 옵션을 사용 하 여 [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] 문.|  
|**기본\_역할\_허용\_연결**|**tinyint**|가용성이 모든 연결을 허용하는지 읽기/쓰기 연결만 허용하는지를 나타내며,  다음 중 하나입니다.<br /><br /> 2  =  모두(기본값)<br /><br /> 3  =  읽기/쓰기|  
|**기본\_역할\_허용\_연결\_desc**|**nvarchar(60)**|에 대 한 설명 **기본\_역할\_허용\_연결**이며 다음 중 하나입니다.<br /><br /> ALL<br /><br /> 읽기\_쓰기|  
|**보조\_역할\_허용\_연결**|**tinyint**|보조 역할을 수행하는 가용성 복제본,  즉 보조 복제본이 클라이언트로부터의 연결을 허용할 수 있는지 여부를 나타내며,  다음 중 하나입니다.<br /><br /> 0 = 아니요 보조 복제본의 데이터베이스에 대한 연결이 허용되지 않으며 읽기 액세스를 위해 데이터베이스에 연결할 수 없습니다. 이 값은 기본 설정입니다.<br /><br /> 1  =  읽기 전용. 보조 복제본의 데이터베이스에 대해 읽기 전용 연결만 허용됩니다. 복제본의 모든 데이터베이스에 대한 읽기 액세스가 가능합니다.<br /><br /> 2  =  모두. 보조 복제본의 데이터베이스에 대해 읽기 전용 액세스를 위한 모든 연결이 허용됩니다.<br /><br /> 자세한 내용은 [활성 보조: 읽기 가능한 보조 복제본&#40;Always On 가용성 그룹&#41;](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)개념을 소개합니다.|  
|**secondary_role_allow_connections_desc**|**nvarchar(60)**|에 대 한 설명 **secondary_role_allow_connections**이며 다음 중 하나입니다.<br /><br /> 아니요<br /><br /> READ_ONLY<br /><br /> ALL|  
|**create_date**|**datetime**|복제본을 만든 날짜입니다.<br /><br /> NULL  =  복제본이 이 서버 인스턴스에 없습니다.|  
|**modify_date**|**datetime**|복제본이 마지막으로 수정된 날짜입니다.<br /><br /> NULL  =  복제본이 이 서버 인스턴스에 없습니다.|  
|**backup_priority**|**int**|이 복제본에 대한 백업을 수행하기 위한 사용자 지정 우선 순위를 나타내며 동일한 가용성 그룹의 다른 복제본을 기준으로 합니다. 이 값은 0에서 100  사이의 정수입니다.<br /><br /> 자세한 내용은 [활성 보조: 보조 복제본에 백업&#40;Always On 가용성 그룹&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)개념을 소개합니다.|  
|**read_only_routing_url**|**nvarchar(256)**|읽기 전용 가용성 복제본의 연결 끝점(URL)입니다. 자세한 내용은 [가용성 그룹에 대한 읽기 전용 라우팅 구성&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)을 참조하세요.|  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>Permissions  
 서버 인스턴스에 대한 VIEW  ANY  DEFINITION  권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sys.availability_groups&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Always On 가용성 그룹&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [가용성 그룹 모니터링 & #40; Transact SQL & #41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [가용성 그룹 모니터링&#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
