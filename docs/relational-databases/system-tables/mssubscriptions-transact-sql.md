---
title: MSsubscriptions (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsubscriptions_TSQL
- MSsubscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscriptions system table
ms.assetid: b7e8301d-d115-41f6-8d4f-e0d25f453b25
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 210329f301790b9a977e356d883c13a8a246a9c3
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85889322"
---
# <a name="mssubscriptions-transact-sql"></a>MSsubscriptions(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **Mssubscriptions** 테이블에는 로컬 배포자가 서비스 하는 구독에 게시 된 각 아티클에 대 한 행이 하나씩 포함 되어 있습니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**publisher_database_id**|**int**|게시자 데이터베이스의 ID입니다.|  
|**publisher_id**|**smallint**|게시자의 ID입니다.|  
|**publisher_db**|**sysname**|게시자 데이터베이스의 이름입니다.|  
|**publication_id**|**int**|게시의 ID입니다.|  
|**article_id**|**int**|아티클의 ID입니다.|  
|**subscriber_id**|**smallint**|구독자의 ID입니다.|  
|**subscriber_db**|**sysname**|구독 데이터베이스의 이름입니다.|  
|**subscription_type**|**int**|구독 유형은 다음과 같습니다.<br /><br /> **0** = 푸시합니다.<br /><br /> **1** = 끌어오기<br /><br /> **2** = 익명.|  
|**sync_type**|**tinyint**|동기화 유형입니다.<br /><br /> **1** = 자동<br /><br /> **2** = 동기화 하지 않습니다.|  
|**status**|**tinyint**|구독 상태입니다.<br /><br /> **0** = 비활성<br /><br /> **1** = 구독 됨<br /><br /> **2** = 활성|  
|**subscription_seqno**|**varbinary(16)**|스냅샷 트랜잭션 시퀀스 번호입니다.|  
|**snapshot_seqno_flag**|**bit**|스냅숏 트랜잭션 시퀀스 번호의 원본을 나타냅니다. 여기서 값 **1** 은 **subscription_seqno** 이 스냅숏 시퀀스 번호 임을 의미 합니다.|  
|**independent_agent**|**bit**|이 게시에 대한 독립 실행형 배포 에이전트가 있는지 여부를 나타냅니다.|  
|**subscription_time**|**datetime**|내부적으로만 사용됩니다.|  
|**loopback_detection**|**bit**|양방향 트랜잭션 복제 토폴로지에 속한 구독에 적용됩니다. 루프백 검색은 배포 에이전트가 구독자에서 발생한 트랜잭션을 다시 구독자로 보낼지 여부를 결정합니다.<br /><br /> **1** = 다시 보내지 않습니다.<br /><br /> **0** = 다시 보냅니다.<br /><br />|  
|**agent_id**|**int**|에이전트의 ID입니다.|  
|**update_mode**|**tinyint**|업데이트의 유형입니다.|  
|**publisher_seqno**|**varbinary(16)**|이 구독에 대한 게시자에서의 트랜잭션 시퀀스 번호입니다.|  
|**ss_cplt_seqno**|**varbinary(16)**|동시 스냅샷 처리의 완료를 표시하는 데 사용되는 시퀀스 번호입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Transact-sql&#41;&#40;복제 뷰](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [Transact-sql&#41;sp_helpsubscription &#40;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
