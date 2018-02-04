---
title: sys.database_mirroring (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.database_mirroring
- database_mirroring
- sys.database_mirroring_TSQL
- database_mirroring_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_mirroring catalog view
ms.assetid: 480de2b0-2c16-497d-a6a3-bf7f52a7c9a0
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c17cf0f7b1ad2a5fd45dcd356546f5e91c4b610b
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="sysdatabasemirroring-transact-sql"></a>sys.database_mirroring(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 있는 각 데이터베이스에 대해 한 행을 포함합니다. 데이터베이스가 온라인 또는 데이터베이스 미러링이 활성화 되어 있지 database_id 제외한 모든 열 값의 NULL이 됩니다.  
  
 Master 또는 tempdb 이외의 데이터베이스에 대 한 행을 보려면 하면 데이터베이스 소유자 이거나 최소한 ALTER ANY DATABASE 또는 VIEW ANY DATABASE 서버 수준 사용 권한 또는 master 데이터베이스에서 CREATE DATABASE 권한입니다. 미러 데이터베이스에서 NULL이 아닌 값을 보려면의 구성원 이어야는 **sysadmin** 고정된 서버 역할입니다.  
  
> [!NOTE]  
>  데이터베이스가 미러링에 참여하지 않으면 접두사가 "mirroring_"인 모든 열이 NULL입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|데이터베이스의 ID입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 내에서 고유합니다.|  
|**mirroring_guid**|**uniqueidentifier**|미러링 파트너 관계의 ID입니다.<br /><br /> NULL = 데이터베이스가 가능 하지 않거나 미러되지 않습니다.<br /><br /> 참고: 데이터베이스 미러링에 참가 하지 않으면, 접두사가 "mirroring_" 인 모든 열은 NULL입니다.|  
|**mirroring_state**|**tinyint**|미러 데이터베이스 및 데이터베이스 미러링 세션의 상태입니다.<br /><br /> 0 = 일시 중지됨<br /><br /> 1 = 다른 파트너와 연결이 끊어짐<br /><br /> 2 = 동기화 중<br /><br /> 3 = 장애 조치(Failover) 보류 중<br /><br /> 4 = 동기화됨<br /><br /> 5 = 파트너가 동기화되지 않았습니다. 지금은 장애 조치를 수행할 수 없습니다.<br /><br /> 6 = 파트너가 동기화되었습니다. 장애 조치를 수행할 수 있습니다. 장애 조치 참조에 대 한 요구 사항에 대 한 내용은 [Database Mirroring Operating Modes](../../database-engine/database-mirroring/database-mirroring-operating-modes.md)합니다.<br /><br /> NULL= 데이터베이스가 액세스 가능하지 않거나 미러되지 않습니다.|  
|**mirroring_state_desc**|**nvarchar(60)**|미러 데이터베이스 및 데이터베이스 미러링 세션의 상태에 대한 설명이며 다음 값 중 하나일 수 있습니다.<br /><br /> DISCONNECTED<br /><br /> SYNCHRONIZED<br /><br /> SYNCHRONIZING<br /><br /> PENDING_FAILOVER<br /><br /> SUSPENDED<br /><br /> UNSYNCHRONIZED<br /><br /> SYNCHRONIZED<br /><br /> NULL<br /><br /> 자세한 내용은 [미러링 상태&#40;SQL Server&#41;](../../database-engine/database-mirroring/mirroring-states-sql-server.md)를 참조하세요.|  
|**mirroring_role**|**tinyint**|데이터베이스 미러링 세션에서 로컬 데이터베이스가 수행하는 현재 역할입니다.<br /><br /> 1 = 주 서버<br /><br /> 2 = 미러 서버<br /><br /> NULL= 데이터베이스가 액세스 가능하지 않거나 미러되지 않습니다.|  
|**mirroring_role_desc**|**nvarchar(60)**|미러링에서 로컬 데이터베이스가 수행하는 역할에 대한 설명이며 다음 값 중 하나일 수 있습니다.<br /><br /> PRINCIPAL<br /><br /> MIRROR|  
|**mirroring_role_sequence**|**int**|장애 조치 또는 강제 서비스로 인해 미러링 파트너가 주 서버 및 미러 서버 역할을 전환한 횟수입니다.<br /><br /> NULL= 데이터베이스가 액세스 가능하지 않거나 미러되지 않습니다.|  
|**mirroring_safety_level**|**tinyint**|미러 데이터베이스 업데이트를 위한 보안 설정입니다.<br /><br /> 0 = 알 수 없는 상태<br /><br /> 1 = Off[비동기]<br /><br /> 2 = Full[동기]<br /><br /> NULL= 데이터베이스가 액세스 가능하지 않거나 미러되지 않습니다.|  
|**mirroring_safety_level_desc**|**nvarchar(60)**|미러 데이터베이스 업데이트를 위한 트랜잭션 보안 설정이며 다음 값 중 하나일 수 있습니다.<br /><br /> UNKNOWN<br /><br /> OFF<br /><br /> FULL<br /><br /> NULL|  
|**mirroring_safety_sequence**|**int**|트랜잭션 보안 수준 변경 내용에 대한 시퀀스 번호를 업데이트합니다.<br /><br /> NULL= 데이터베이스가 액세스 가능하지 않거나 미러되지 않습니다.|  
|**mirroring_partner_name**|**nvarchar(128)**|데이터베이스 미러링 파트너의 서버 이름입니다.<br /><br /> NULL= 데이터베이스가 액세스 가능하지 않거나 미러되지 않습니다.|  
|**mirroring_partner_instance**|**nvarchar(128)**|다른 파트너의 인스턴스 이름 및 컴퓨터 이름입니다. 클라이언트는 파트너가 주 서버가 되면 이 정보를 사용하여 파트너에 연결합니다.<br /><br /> NULL= 데이터베이스가 액세스 가능하지 않거나 미러되지 않습니다.|  
|**mirroring_witness_name**|**nvarchar(128)**|데이터베이스 미러링 모니터 서버의 이름입니다.<br /><br /> NULL = 미러링 모니터 서버가 없음|  
|mirroring_witness_state|**tinyint**|데이터베이스의 데이터베이스 미러링 세션에 있는 미러링 모니터 서버의 상태이며 다음 값 중 하나일 수 있습니다.<br /><br /> 0 = 알 수 없음<br /><br /> 1 = 연결됨<br /><br /> 2 = 연결 끊김<br /><br /> NULL = 미러링 모니터가 없거나, 데이터베이스가 온라인 상태가 아니거나, 데이터베이스가 미러되지 않음|  
|**mirroring_witness_state_desc**|**nvarchar(60)**|상태에 대한 설명이며 다음 값 중 하나일 수 있습니다.<br /><br /> UNKNOWN<br /><br /> CONNECTED<br /><br /> DISCONNECTED<br /><br /> NULL|  
|**mirroring_failover_lsn**|**numeric(25,0)**|두 파트너 모두의 디스크에 확정될 최신 트랜잭션 로그 레코드의 LSN(로그 시퀀스 번호)입니다. 장애 조치 후의 **mirroring_failover_lsn** 새 미러 데이터베이스를 새 주 데이터베이스와 동기화 하는 새 미러 서버가 시작 되는 조정 지점으로의 파트너에 의해 사용 됩니다.|  
|**mirroring_connection_timeout**|**int**|미러링 연결 제한 시간(초)입니다. 이 값은 파트너 또는 미러링 모니터 서버가 사용할 수 없는 것으로 간주되기 전에 해당 서버의 응답을 대기하는 시간(초)입니다. 기본 제한 시간 값은 10초입니다.<br /><br /> NULL= 데이터베이스가 액세스 가능하지 않거나 미러되지 않습니다.|  
|**mirroring_redo_queue**|**int**|미러에서 다시 실행할 최대 로그 크기입니다. Mirroring_redo_queue_type은 기본 설정, 설정인 unlimited로 설정 된 경우이 열은 NULL입니다. 데이터베이스가 온라인이 아닌 경우에도 이 열은 NULL입니다.<br /><br /> 그렇지 않으면 이 열에는 최대 로그 크기(MB)가 포함됩니다. 최대값에 도달하면 로그는 미러 서버가 처리할 수 있도록 주 서버에서 일시 대기합니다. 이 기능은 장애 조치 시간을 제한합니다.<br /><br /> 자세한 내용은 [역할 전환 중 서비스 중단 예측&#40;데이터베이스 미러링&#41;](../../database-engine/database-mirroring/estimate-the-interruption-of-service-during-role-switching-database-mirroring.md)을 참조하세요.|  
|**mirroring_redo_queue_type**|**nvarchar(60)**|UNLIMITED는 미러링이 Redo Queue를 방해하지 않는다는 의미입니다. 이 값은 기본 설정입니다.<br /><br /> MB는 메가바이트 단위로 표시한 Redo Queue의 최대 크기를 나타냅니다. 큐 크기(KB 또는 GB)를 지정하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 그 값을 MB로 변환합니다.<br /><br /> 데이터베이스가 온라인이 아닌 경우 이 열은 NULL입니다.|  
|**mirroring_end_of_log_lsn**|**numeric(25,0)**|디스크로 플러시된 로컬 로그 끝. 이 미러 서버에서 확정 된 LSN에 버금가 (참조는 **mirroring_failover_lsn** 열)입니다.|  
|**mirroring_replication_lsn**|**numeric(25,0)**|복제본을 보낼 수 있는 최대 LSN.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sys.database_mirroring_witnesses &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
 [sys.database_mirroring_endpoints&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)   
 [데이터베이스 및 파일 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [SQL Server 시스템 카탈로그 쿼리 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
