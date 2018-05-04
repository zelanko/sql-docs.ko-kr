---
title: syssubscriptions (시스템 뷰) (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- syssubscriptions_TSQL
- syssubscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- syssubscriptions view
ms.assetid: c9613858-9512-43a9-aa53-7ee8064f064c
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 38c7ef5c308f91e7b7e981785f199139702367b0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="syssubscriptions-system-view-transact-sql"></a>syssubscriptions(시스템 뷰)(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **syssubscriptions** 뷰는 구독 정보를 표시 합니다. 이 뷰는 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|구독한 아티클의 고유 ID입니다.|  
|**srvid**|**smallint**|구독자의 서버 ID입니다.|  
|**dest_db**|**sysname**|구독 데이터베이스의 이름입니다.|  
|**상태**|**tinyint**|구독 상태입니다.<br /><br /> **0** = 비활성입니다.<br /><br /> **1** = 구독 합니다.<br /><br /> **2** = 활성 합니다.|  
|**sync_type**|**tinyint**|초기 동기화의 유형입니다.<br /><br /> **1** = 자동입니다.<br /><br /> **2** = none입니다.|  
|**login_name**|**sysname**|구독을 추가하기 위해 구독자에 연결할 때 사용하는 로그인 이름입니다.|  
|**subscription_type**|**int**|구독 유형은 다음과 같습니다.<br /><br /> **0** = 밀어넣기-배포 에이전트가 배포자에서 실행 합니다.<br /><br /> **1** = 끌어오기-배포 에이전트가 구독자에서 실행 합니다.|  
|**distribution_jobid**|**binary(16)**|구독을 동기화하는 데 사용되는 배포 에이전트 작업을 식별합니다.|  
|**timestmap**|**timestamp**|구독을 만든 날짜와 시간입니다.|  
|**update_mode**|**tinyint**|업데이트 모드입니다.<br /><br /> **0** = 읽기 전용입니다.<br /><br /> **1** = 즉시 업데이트 합니다.|  
|**loopback_detection**|**bit**|양방향 트랜잭션 복제 토폴로지에 속한 구독에 적용됩니다. 루프백 검색은 배포 에이전트가 구독자에서 발생한 트랜잭션을 다시 구독자에게 보낼지 여부를 결정합니다.<br /><br /> **0** = 다시 보냅니다.<br /><br /> **1** = 다시 보내지 않았습니다.|  
|**queued_reinit**|**bit**|아티클을 초기화 또는 다시 초기화하도록 표시할지 여부를 지정합니다. 값이 **1** 구독 된 아티클을 초기화 또는 다시 초기화 하도록 표시 되도록 지정 합니다.|  
|**nosync_type**|**tinyint**|구독 초기화의 유형입니다.<br /><br /> **0** = 자동 (스냅숏)<br /><br /> **1** = 복제 지원 전용<br /><br /> **2** = 백업으로 초기화<br /><br /> **3** = 로그 시퀀스 번호 (LSN)에서 초기화<br /><br /> 자세한 내용은 참조는 **@sync_type** 의 매개 변수 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)합니다.<br /><br /> **3** = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**srvname**|**sysname**|구독자 이름입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [복제 테이블 &#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [syssubscriptions&#40;Transact-SQL&#41;](../../relational-databases/system-tables/syssubscriptions-transact-sql.md)  
  
  
