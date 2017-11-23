---
title: IHextendedSubscriptionView (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- IHextendedSubscriptionView_TSQL
- IHextendedSubscriptionView
dev_langs: TSQL
helpviewer_keywords: IHextendedSubscriptionView view
ms.assetid: 124756a4-463a-4a81-bf5b-de7e8ffc7a62
caps.latest.revision: "11"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b7aa47e213552b5351c1dc1c7fc685ec96cd4a45
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="ihextendedsubscriptionview-transact-sql"></a>IHextendedSubscriptionView(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHextendedSubscriptionView** 뷰는 구독 SQL Server 이외 게시에 대 한 정보를 표시 합니다. 이 보기에 저장 되는 **배포** 데이터베이스입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**article_id**|**int**|아티클에 대한 고유 식별자입니다.|  
|**dest_db**|**sysname**|대상 데이터베이스의 이름입니다.|  
|**srvid**|**smallint**|구독자에 대한 고유 식별자입니다.|  
|**login_name**|**sysname**|구독자에 연결할 때 사용하는 로그인입니다.|  
|**distribution_jobid**|**binary**|배포 에이전트 작업을 식별합니다.|  
|**publisher_database_id**|**int**|게시 데이터베이스를 식별합니다.|  
|**subscription_type**|**int**|구독 유형은 다음과 같습니다.<br /><br /> **0** = 밀어넣기-배포 에이전트가 구독자에서 실행 합니다.<br /><br /> **1** = 끌어오기-배포 에이전트가 배포자에서 실행 합니다.|  
|**sync_type**|**tinyint**|초기 동기화의 유형입니다.<br /><br /> **1** = 자동<br /><br /> **2** = 없음|  
|**상태**|**tinyint**|구독 상태입니다.<br /><br /> **0** = 비활성<br /><br /> **1** = 구독<br /><br /> **2** = 활성|  
|**snapshot_seqno_flag**|**bit**|스냅숏 시퀀스 번호가 사용되었는지 여부를 나타냅니다.|  
|**독립 에이전트**|**bit**|해당 게시에 독립 실행형 배포 에이전트가 있는지 여부를 지정합니다.<br /><br /> **0** = 게시는 공유 배포 에이전트를 사용 하며 각 게시자 데이터베이스/구독자 데이터베이스 쌍에는 공유 에이전트가 있습니다.<br /><br /> **1** =이 게시에 대 한 독립 실행형 배포 에이전트가 있습니다.|  
|**subscription_time**|**datetime**|내부적으로만 사용됩니다.|  
|**loopback_detection**|**bit**|양방향 트랜잭션 복제 토폴로지에 속한 구독에 적용됩니다. 루프백 검색은 배포 에이전트가 구독자에서 발생한 트랜잭션을 다시 구독자에게 보낼지 여부를 결정합니다.<br /><br /> **1** = 다시 보내지 않았습니다.<br /><br /> **0** = 다시 보냅니다.|  
|**agent_id**|**int**|배포 에이전트의 고유 식별자입니다.|  
|**update_mode**|**tinyint**|업데이트 모드의 유형을 나타내며 다음 중 하나일 수 있습니다.<br /><br /> **0** = 읽기 전용입니다.<br /><br /> **1** = 즉시 업데이트 합니다.<br /><br /> **2** = 메시지 큐를 사용 하는 지연 업데이트 합니다.<br /><br /> **3** = 즉시 메시지 큐를 사용 하 여 장애 조치로 지연된 업데이트를 업데이트 합니다.<br /><br /> **4** = SQL Server 큐를 사용 하는 지연 업데이트 합니다.<br /><br /> **5** = SQL Server 큐를 사용 하 여 지연된 업데이트 장애 조치를 사용 하는 즉시 업데이트 합니다.|  
|**publisher_seqno**|**varbinary (16)**|이 구독에 대한 게시자에서의 트랜잭션 시퀀스 번호입니다.|  
|**ss_cplt_seqno**|**varbinary (16)**|동시 스냅숏 처리의 완료를 표시하는 데 사용되는 시퀀스 번호입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [다른 유형의 데이터베이스 복제](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [복제 테이블 &#40; Transact SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
