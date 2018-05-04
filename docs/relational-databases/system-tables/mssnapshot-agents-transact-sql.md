---
title: MSsnapshot_agents (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- MSsnapshot_agents
- MSsnapshot_agents_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsnapshot_agents system table
ms.assetid: aeae0a2e-4c21-4c45-be65-1e426fa52bdd
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 8dfe60e5ae1ad3443fde1b7655941b70f53663cd
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="mssnapshotagents-transact-sql"></a>MSsnapshot_agents(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSsnapshot_agents** 테이블은 로컬 배포자와 연결 된 각 스냅숏 에이전트에 대 한 개의 행을 포함 합니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|스냅숏 에이전트의 ID입니다.|  
|**name**|**nvarchar(100)**|스냅숏 에이전트의 이름입니다.|  
|**publisher_id**|**smallint**|게시자의 ID입니다.|  
|**publisher_db**|**sysname**|게시자 데이터베이스의 이름입니다.|  
|**게시**|**sysname**|게시의 이름입니다.|  
|**publication_type**|**int**|게시의 유형입니다.<br /><br /> **0** = 트랜잭션.<br /><br /> **1** = 스냅숏 합니다.<br /><br /> **2** = 병합 합니다.|  
|**local_job**|**bit**|로컬 배포자에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업이 있는지 여부를 나타냅니다.|  
|**job_id**|**binary(16)**|작업 ID입니다.|  
|**profile_id**|**int**|구성 ID는 [MSagent_profiles &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/msagent-profiles-transact-sql.md) 테이블입니다.|  
|**dynamic_filter_login**|**sysname**|평가 하는 데 사용 되는 값은 [SUSER_SNAME &#40;TRANSACT-SQL&#41; ](../../t-sql/functions/suser-sname-transact-sql.md) 파티션을 정의 하는 매개 변수가 있는 필터의 함수입니다. 이 열은 분할된 스냅숏에 사용됩니다.|  
|**dynamic_filter_hostname**|**sysname**|평가 하는 데 사용 되는 값은 [HOST_NAME &#40;TRANSACT-SQL&#41; ](../../t-sql/functions/host-name-transact-sql.md) 파티션을 정의 하는 매개 변수가 있는 필터의 함수입니다. 이 열은 분할된 스냅숏에 사용됩니다.|  
|**publisher_security_mode**|**smallint**|에이전트가 게시자에 연결할 때 사용하는 보안 모드로 다음 중 하나일 수 있습니다.<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 인증입니다.|  
|**publisher_login**|**sysname**|게시자에 연결할 때 사용하는 로그인입니다.|  
|**publisher_password**|**nvarchar (524)**|게시자에 연결할 때 사용하는 암호의 암호화된 값입니다.|  
|**job_step_uid**|**uniqueidentifier**|에이전트가 시작되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 단계의 고유 ID입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [복제 테이블 &#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
