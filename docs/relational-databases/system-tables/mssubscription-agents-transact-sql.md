---
title: MSsubscription_agents (Transact SQL) | Microsoft Docs
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
- MSsubscription_agents
- MSsubscription_agents_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscription_agents system table
ms.assetid: 86ad5891-0bef-4963-9381-7d5b45245a0c
caps.latest.revision: 25
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6918d4e2c1f835cb9a2ac2ac5fb15dee188916a5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="mssubscriptionagents-transact-sql"></a>MSsubscription_agents(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSsubscription_agents** 테이블 배포 에이전트 및 업데이트할 수 있는 구독의 트리거가 구독 속성 추적을 사용 합니다. 이 테이블은 구독 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|행의 ID입니다.|  
|**publisher**|**sysname**|게시자의 이름입니다.|  
|**publisher_db**|**sysname**|게시 데이터베이스의 이름입니다.|  
|**게시**|**sysname**|게시의 이름입니다.|  
|**subscription_type**|**int**|구독 유형입니다.<br /><br /> 0 = 밀어넣기<br /><br /> 1 = 끌어오기<br /><br /> 2 = 익명 끌어오기|  
|**queue_id**|**sysname**|ID는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 메시지 게시자에서 큐입니다. *queue_id* 로 설정 된 **SQL** 에 대 한 SQL 기반의 지연 업데이트 합니다.|  
|**update_mode**|**tinyint**|업데이트의 유형입니다.<br /><br /> **0** = 읽기 전용입니다.<br /><br /> **1** = 즉시 업데이트 합니다.<br /><br /> **2** = 메시지 큐를 사용 하는 지연 업데이트 합니다.<br /><br /> **3** = 즉시 메시지 큐를 사용 하 여 장애 조치로 지연된 업데이트를 업데이트 합니다.<br /><br /> **4** = SQL Server 큐를 사용 하는 지연 업데이트 합니다.<br /><br /> **5** = SQL Server 큐를 사용 하 여 지연된 업데이트 장애 조치를 사용 하는 즉시 업데이트 합니다.|  
|**failover_mode**|**bit**|업데이트의 장애 조치 유형이 선택된 경우 장애 조치 유형은 다음과 같습니다.<br /><br /> **0** = 즉시 업데이트를 사용 합니다. 장애 조치를 사용하지 않습니다.<br /><br /> **1** = 대기 중 업데이트를 사용 합니다. 장애 조치를 사용합니다. 장애 조치에 사용 되는 큐에 지정 된 *update_mode* 값입니다.|  
|**spid**|**int**|현재 실행 중이거나 방금 실행된 배포 에이전트가 사용하는 연결에 대한 시스템 프로세스 ID입니다.|  
|**login_time**|**datetime**|현재 실행 중이거나 방금 실행된 배포 에이전트 연결의 날짜 및 시간입니다.|  
|**allow_subscription_copy**|**bit**|구독 데이터베이스 복사 기능의 허용 여부를 지정합니다.|  
|**attach_state**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**attach_version**|**binary(16)**|연결된 구독의 버전을 나타내는 고유한 식별자입니다.|  
|**last_sync_status**|**int**|현재 실행 중이거나 방금 실행된 배포 에이전트의 마지막 실행 상태입니다. 상태는 다음과 같을 수 있습니다.<br /><br /> **1** = 시작 합니다.<br /><br /> **2** = 성공 합니다.<br /><br /> **3** = 진행 중입니다.<br /><br /> **4** = 유휴 상태입니다.<br /><br /> **5** = 다시 시도 합니다.<br /><br /> **6** = 실패.|  
|**last_sync_summary**|**sysname**|현재 실행 중이거나 방금 실행된 배포 에이전트의 마지막 메시지입니다. 상태는 다음과 같을 수 있습니다.<br /><br /> **시작 되었습니다.**<br /><br /> **성공 했습니다.**<br /><br /> **진행 중입니다.**<br /><br /> **유휴입니다.**<br /><br /> **다시 시도 하십시오.**<br /><br /> **실패 합니다.**|  
|**last_sync_time**|**datetime**|날짜 및 시간을 *last_sync_summary* 및 *last_sync_status* 업데이트 된 열입니다. SqlServer 에이전트 서비스 작업으로 실행되는 끌어오기 또는 익명 배포 에이전트는 이러한 열을 업데이트하지 않습니다. 이 경우에는 대신 기록 정보가 작업 기록 테이블에 기록됩니다.|  
|**queue_server**|**sysname**|내부적으로만 사용됩니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [복제 테이블 &#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_helppullsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)  
  
  
