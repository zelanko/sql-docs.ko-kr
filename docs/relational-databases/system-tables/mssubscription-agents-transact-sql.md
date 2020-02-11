---
title: MSsubscription_agents (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsubscription_agents
- MSsubscription_agents_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscription_agents system table
ms.assetid: 86ad5891-0bef-4963-9381-7d5b45245a0c
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3354f69f92cbbbaa9d60ae8ed6352a0b3be6ab52
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68139794"
---
# <a name="mssubscription_agents-transact-sql"></a>MSsubscription_agents(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSsubscription_agents** 테이블은 구독 속성을 추적 하기 위해 업데이트 가능한 구독의 배포 에이전트 및 트리거에서 사용 됩니다. 이 테이블은 구독 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**a-id**|**int**|행의 ID입니다.|  
|**발행자**|**sysname**|게시자의 이름입니다.|  
|**publisher_db**|**sysname**|게시 데이터베이스의 이름입니다.|  
|**게시물**|**sysname**|게시의 이름입니다.|  
|**subscription_type**|**int**|구독 유형입니다.<br /><br /> 0 = 밀어넣기<br /><br /> 1 = 끌어오기<br /><br /> 2 = 익명 끌어오기|  
|**queue_id**|**sysname**|게시자에 있는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 메시지 큐의 ID입니다. SQL 기반 지연 업데이트에 대 한 *Queue_id* **sql** 로 설정 됩니다.|  
|**update_mode**|**tinyint**|업데이트의 유형입니다.<br /><br /> **0** = 읽기 전용입니다.<br /><br /> **1** = 즉시 업데이트<br /><br /> **2** = 메시지 큐를 사용 하는 지연 업데이트<br /><br /> **3** = 메시지 큐를 사용 하 여 장애 조치 (failover)로 지연 업데이트를 사용 하는 즉시 업데이트<br /><br /> **4** = SQL Server 큐를 사용 하는 지연 업데이트<br /><br /> **5** = SQL Server 큐를 사용 하는 지연 업데이트 장애 조치 (failover)를 사용 하는 즉시 업데이트|  
|**failover_mode**|**bit**|업데이트의 장애 조치 유형이 선택된 경우 장애 조치 유형은 다음과 같습니다.<br /><br /> **0** = 즉시 업데이트를 사용 하 고 있습니다. 장애 조치를 사용하지 않습니다.<br /><br /> **1** = 지연 업데이트를 사용 하 고 있습니다. 장애 조치를 사용합니다. 장애 조치 (failover)에 사용 되는 큐는 *update_mode* 값에 지정 됩니다.|  
|**spid**|**int**|현재 실행 중이거나 방금 실행된 배포 에이전트가 사용하는 연결에 대한 시스템 프로세스 ID입니다.|  
|**login_time**|**datetime**|현재 실행 중이거나 방금 실행된 배포 에이전트 연결의 날짜 및 시간입니다.|  
|**allow_subscription_copy**|**bit**|구독 데이터베이스 복사 기능의 허용 여부를 지정합니다.|  
|**attach_state**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**attach_version**|**binary (16)**|연결된 구독의 버전을 나타내는 고유한 식별자입니다.|  
|**last_sync_status**|**int**|현재 실행 중이거나 방금 실행된 배포 에이전트의 마지막 실행 상태입니다. 상태는 다음과 같을 수 있습니다.<br /><br /> **1** = 시작 됨<br /><br /> **2** = 성공<br /><br /> **3** = 진행 중<br /><br /> **4** = 유휴 상태입니다.<br /><br /> **5** = 다시 시도<br /><br /> **6** = 실패|  
|**last_sync_summary**|**sysname**|현재 실행 중이거나 방금 실행된 배포 에이전트의 마지막 메시지입니다. 상태는 다음과 같을 수 있습니다.<br /><br /> **했어야.**<br /><br /> **열었습니다.**<br /><br /> **진행 중입니다.**<br /><br /> **유휴.**<br /><br /> **Retry.**<br /><br /> **통과.**|  
|**last_sync_time**|**datetime**|*Last_sync_summary* 및 *last_sync_status* 열이 업데이트 된 날짜 및 시간입니다. SqlServer 에이전트 서비스 작업으로 실행되는 끌어오기 또는 익명 배포 에이전트는 이러한 열을 업데이트하지 않습니다. 이 경우에는 대신 기록 정보가 작업 기록 테이블에 기록됩니다.|  
|**queue_server**|**sysname**|내부적으로만 사용됩니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Transact-sql&#41;&#40;복제 뷰](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [Transact-sql&#41;sp_helppullsubscription &#40;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)  
  
  
