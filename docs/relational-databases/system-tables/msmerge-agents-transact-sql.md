---
title: MSmerge_agents (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_agents
- MSmerge_agents_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_agents system table
ms.assetid: 639d2ebb-2c37-4fe0-b14b-1637bc5fc221
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c1c4d976d97dee95e09a053525a14df632cd7e62
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82803166"
---
# <a name="msmerge_agents-transact-sql"></a>MSmerge_agents(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_agents** 테이블에는 구독자에서 실행 되는 각 병합 에이전트에 대 한 행이 하나씩 포함 되어 있습니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|병합 에이전트의 ID입니다.|  
|**name**|**nvarchar (100)**|병합 에이전트의 이름입니다.|  
|**publisher_id**|**smallint**|게시자의 ID입니다.|  
|**publisher_db**|**sysname**|게시자 데이터베이스의 이름입니다.|  
|**게시물**|**sysname**|게시의 이름입니다.|  
|**subscriber_id**|**smallint**|구독자의 ID입니다.|  
|**subscriber_db**|**sysname**|구독 데이터베이스의 이름입니다.|  
|**local_job**|**bit**|로컬 배포자에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업이 있는지 여부를 나타냅니다.|  
|**job_id**|**binary(16)**|작업 ID입니다.|  
|**profile_id**|**int**|**MSagent_profiles** 테이블의 구성 ID입니다.|  
|**anonymous_subid**|**uniqueidentifier**|익명 에이전트의 ID입니다.|  
|**subscriber_name**|**sysname**|구독자 이름입니다.|  
|**creation_date**|**datetime**|배포 또는 병합 에이전트를 만든 날짜와 시간입니다.|  
|**offload_enabled**|**bit**|에이전트를 원격으로 활성화할 수 있음을 나타냅니다.<br /><br /> **0** 은 에이전트를 원격으로 활성화할 수 없음을 나타냅니다.<br /><br /> **1** 은 에이전트가 원격으로 활성화 되 고 offload_server 속성에 지정 된 원격 컴퓨터에서 활성화 되도록 지정 합니다.|  
|**offload_server**|**sysname**|원격 에이전트 활성화에 사용할 서버의 네트워크 이름을 지정합니다.|  
|**sid**|**varbinary(85)**|첫 번째 실행 시 배포 에이전트 또는 병합 에이전트의 SID(보안 ID)입니다.|  
|**subscriber_security_mode**|**smallint**|에이전트가 구독자에 연결할 때 사용하는 보안 모드로 다음 중 하나일 수 있습니다.<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증.<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 인증입니다.|  
|**subscriber_login**|**sysname**|구독자에 연결할 때 사용하는 로그인입니다.|  
|**subscriber_password**|**nvarchar (524)**|구독자에 연결할 때 사용하는 암호의 암호화된 값입니다.|  
|**publisher_security_mode**|**smallint**|에이전트가 게시자에 연결할 때 사용하는 보안 모드로 다음 중 하나일 수 있습니다.<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증.<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 인증입니다.|  
|**publisher_login**|**sysname**|게시자에 연결할 때 사용하는 로그인입니다.|  
|**publisher_password**|**nvarchar (524)**|게시자에 연결할 때 사용하는 암호의 암호화된 값입니다.|  
|**job_step_uid**|**uniqueidentifier**|에이전트가 시작되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 단계의 고유 ID입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
