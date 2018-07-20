---
title: MSdistribution_agents (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/28/2015
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSdistribution_agents_TSQL
- MSdistribution_agents
dev_langs:
- TSQL
helpviewer_keywords:
- MSdistribution_agents system table
ms.assetid: 0e8f0653-1351-41d1-95d2-40f6d5a050ca
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a2fbcec90b48f283d6d486819264faf02cf88b4c
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39103301"
---
# <a name="msdistributionagents-transact-sql"></a>MSdistribution_agents(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **MSdistribution_agents** 테이블은 로컬 배포자에서 실행 되는 각 배포 에이전트에 대 한 하나의 행을 포함 합니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|배포 에이전트의 ID입니다.|  
|**name**|**nvarchar(100)**|배포 에이전트의 이름입니다.|  
|**publisher_database_id**|**int**|게시자 데이터베이스의 ID입니다.|  
|**publisher_id**|**smallint**|게시자의 ID입니다.|  
|**publisher_db**|**sysname**|게시자 데이터베이스의 이름입니다.|  
|**게시**|**sysname**|게시의 이름입니다.|  
|**subscriber_id**|**smallint**|잘 알려진 에이전트에서만 사용하는 구독자의 ID입니다. 익명 에이전트를 위해 이 열이 예약됩니다.|  
|**subscriber_db**|**sysname**|구독 데이터베이스의 이름입니다.|  
|**subscription_type**|**int**|구독 유형은 다음과 같습니다.<br /><br /> **0** = 밀어넣기 합니다.<br /><br /> **1** = 끌어오기.<br /><br /> **2** = 익명입니다.|  
|**local_job**|**bit**|로컬 배포자에는 SQL Server 에이전트 작업이 있는지 여부를 나타냅니다.|  
|**job_id**|**binary(16)**|작업 ID입니다.|  
|**subscription_guid**|**binary(16)**|이 에이전트의 구독 ID입니다.|  
|**profile_id**|**int**|구성 ID를 [MSagent_profiles &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/msagent-profiles-transact-sql.md) 테이블입니다.|  
|**anonymous_subid**|**uniqueidentifier**|익명 에이전트의 ID입니다.|  
|**subscriber_name**|**sysname**|익명 에이전트에서만 사용하는 구독자의 이름입니다.|  
|**virtual_agent_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**anonymous_agent_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**creation_date**|**datetime**|배포 또는 병합 에이전트가 생성된 datetime입니다.|  
|**queue_id**|**sysname**|지연 업데이트 구독의 큐 위치를 나타내는 식별자입니다. 지연 구독이 아닌 경우 이 값은 NULL입니다. MSMQ([!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing)를 기반으로 하는 게시의 경우 이 값은 구독에 사용할 큐를 고유하게 식별하는 GUID입니다. SQL Server 기반 큐 게시의 경우 열 값을 포함 **SQL**합니다.<br /><br /> 참고:를 사용 하 여 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 메시지 큐가 사용 되지 않으며 더 이상 지원 되지.|  
|**queue_status**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**offload_enabled**|**bit**|에이전트를 원격으로 활성화할 수 있는지 여부를 나타냅니다.<br /><br /> **0** 에이전트를 원격으로 활성화할 수 없습니다 지정 합니다.<br /><br /> **1** 에 지정 된 원격 컴퓨터를 원격으로 에이전트를 활성화할 수 있도록 지정 합니다 *offload_server* 속성입니다.|  
|**offload_server**|**sysname**|원격 에이전트 활성화에 사용할 서버의 네트워크 이름입니다.|  
|**dts_package_name**|**sysname**|DTS 패키지의 이름입니다. 명명 된 예 패키지용 **DTSPub_Package**, 지정 `@dts_package_name = N'DTSPub_Package'`합니다.|  
|**dts_package_password**|**nvarchar(524)**|패키지의 암호입니다.|  
|**dts_package_location**|**int**|패키지 위치입니다. 패키지의 위치 일 수 있습니다 **배포자** 하거나 **구독자**합니다.|  
|**sid**|**varbinary(85)**|첫 번째 실행 시 배포 에이전트 또는 병합 에이전트의 SID(보안 ID)입니다.|  
|**queue_server**|**sysname**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**subscriber_security_mode**|**smallint**|에이전트가 구독자에 연결할 때 사용하는 보안 모드로 다음 중 하나일 수 있습니다.<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQL Server 인증<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 인증입니다.|  
|**subscriber_login**|**sysname**|구독자에 연결할 때 사용하는 로그인입니다.|  
|**subscriber_password**|**nvarchar(524)**|구독자에 연결할 때 사용하는 암호의 암호화된 값입니다.|  
|**reset_partial_snapshot_progress**|**bit**|스냅숏이 일부분만 다운로드된 경우 이를 삭제하여 전체 스냅숏 과정을 다시 시작하도록 할지 여부입니다.|  
|**job_step_uid**|**uniqueidentifier**|에이전트가 시작 되는 단계의 SQL Server 에이전트 작업의 고유 ID입니다.|  
|**subscriptionstreams**|**tinyint**|변경 내용을 구독자에 병렬로 일괄 적용하기 위해 허용되는 배포 에이전트당 연결 수를 설정합니다. 1에서 64 사이의 값 범위가 지원됩니다.|  
|**메모리 액세스에 최적화**|**bit**|1은 메모리 액세스에 최적화 된 테이블에 대 한 구독자를 사용할 수 있다는 것을 나타냅니다.|  
|**job_login**|**sysname**||  
|**job_password**|**nvarchar(524)**||  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
