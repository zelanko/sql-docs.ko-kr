---
title: syssubscriptions (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- syssubscriptions_TSQL
- syssubscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- syssubscriptions system table
ms.assetid: 106c1707-e0e0-49b4-ba50-25380c40fab2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b7375dff31cb9cd0f092315b9a53e57e2f0ecd1a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62632293"
---
# <a name="syssubscriptions-transact-sql"></a>syssubscriptions(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터베이스 내의 각 구독당 하나의 행을 포함합니다. 이 테이블은 게시 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|아티클의 고유한 ID입니다.|  
|**srvid**|**smallint**|구독자의 서버 ID입니다.|  
|**dest_db**|**sysname**|대상 데이터베이스의 이름입니다.|  
|**상태**|**tinyint**|구독 상태입니다.<br /><br /> **0** = 비활성입니다.<br /><br /> **1** = 구독 합니다.<br /><br /> **2** = 활성입니다.|  
|**sync_type**|**tinyint**|초기 동기화의 유형입니다.<br /><br /> **1** = Automatic.<br /><br /> **2** = 없음|  
|**login_name**|**sysname**|구독을 추가할 때 사용하는 로그인 이름입니다.|  
|**subscription_type**|**int**|구독 유형은 다음과 같습니다.<br /><br /> 0 = 밀어넣기 - 배포 에이전트가 배포자에서 실행됩니다.<br /><br /> 1 = 끌어오기 - 배포 에이전트가 구독자에서 실행됩니다.|  
|**distribution_jobid**|**binary(16)**|배포 에이전트의 작업 ID입니다.|  
|**timestamp**|**timestamp**|타임 스탬프입니다.|  
|**update_mode**|**tinyint**|업데이트 모드입니다.<br /><br /> **0** = 읽기 전용입니다.<br /><br /> **1** = 즉시 업데이트 합니다.|  
|**loopback_detection**|**bit**|양방향 트랜잭션 복제 토폴로지에 속한 구독에 적용됩니다. 루프백 검색은 배포 에이전트가 구독자에서 발생한 트랜잭션을 다시 구독자로 보낼지 여부를 결정합니다.<br /><br /> **0** = 다시 보냅니다.<br /><br /> **1** 않습니다 = 다시 보내지 않습니다.|  
|**queued_reinit**|**bit**|아티클을 초기화 또는 다시 초기화하도록 표시할지 여부를 지정합니다. 값이 **1** 구독된 아티클을 초기화 또는 다시 초기화 하도록 표시 되도록 지정 합니다.|  
|**nosync_type**|**tinyint**|구독 초기화의 유형입니다.<br /><br /> **0** = 자동 (스냅숏)<br /><br /> **1** = 복제 지원 전용<br /><br /> **2** = 백업 사용 하 여 초기화<br /><br /> **3** = LSN (로그 시퀀스 번호)에서 초기화<br /><br /> 자세한 내용은 참조는 **@sync_type** 의 매개 변수 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)합니다.|  
|**srvname**|**sysname**|구독자 이름입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
