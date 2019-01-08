---
title: MSreplication_subscriptions (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSreplication_subscriptions
- MSreplication_subscriptions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplication_subscriptions system table
ms.assetid: fd0c5843-4e9b-4448-8bfb-0a4067d1d8d1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0fa68012f419939c3f77980020795f23c4ca4672
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52794535"
---
# <a name="msreplicationsubscriptions-transact-sql"></a>MSreplication_subscriptions(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **MSreplication_subscriptions** 테이블의 각 배포 에이전트는 로컬 구독자 데이터베이스에 대 한 복제 정보가 하나의 행을 포함 합니다. 이 테이블은 구독 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|게시자의 이름입니다.|  
|**publisher_db**|**sysname**|게시자 데이터베이스의 이름입니다.|  
|**게시**|**sysname**|게시의 이름입니다.|  
|**independent_agent**|**bit**|이 게시에 대한 독립 실행형 배포 에이전트가 있는지 여부를 나타냅니다.|  
|**subscription_type**|**int**|구독 유형은 다음과 같습니다.<br /><br /> 0 = 밀어넣기<br /><br /> 1 = 끌어오기<br /><br /> 2 = 익명|  
|**distribution_agent**|**sysname**|배포 에이전트의 이름입니다.|  
|**Time**|**smalldatetime**|배포 에이전트가 마지막으로 업데이트한 시간입니다.|  
|**description**|**nvarchar(255)**|게시에 대한 설명입니다.|  
|**transaction_timestamp**|**varbinary(16)**|내부적으로만 사용됩니다.|  
|**update_mode**|**tinyint**|업데이트의 유형입니다.|  
|**agent_id**|**binary(16)**|에이전트의 ID입니다.|  
|**subscription_guid**|**binary(16)**|게시에 관한 구독 버전의 전역 식별자입니다.|  
|**subid**|**binary(16)**|익명 구독에 관한 전역 식별자입니다.|  
|**immediate_sync**|**bit**|스냅숏 에이전트가 실행될 때마다 동기화 파일을 만들거나 다시 만들지 여부를 나타냅니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_helpsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
