---
title: MSreplication_subscriptions (Transact-sql) | Microsoft Docs
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
ms.openlocfilehash: a7164afe24d15abf195ebff96e4e96a82877deae
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68079988"
---
# <a name="msreplication_subscriptions-transact-sql"></a>MSreplication_subscriptions(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSreplication_subscriptions** 테이블에는 로컬 구독자 데이터베이스를 제공 하는 각 배포 에이전트에 대 한 복제 정보 행이 하나씩 포함 되어 있습니다. 이 테이블은 구독 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**발행자**|**sysname**|게시자의 이름입니다.|  
|**publisher_db**|**sysname**|게시자 데이터베이스의 이름입니다.|  
|**게시물**|**sysname**|게시의 이름입니다.|  
|**independent_agent**|**bit**|이 게시에 대한 독립 실행형 배포 에이전트가 있는지 여부를 나타냅니다.|  
|**subscription_type**|**int**|구독 유형은 다음과 같습니다.<br /><br /> 0 = 밀어넣기<br /><br /> 1 = 끌어오기<br /><br /> 2 = 익명|  
|**distribution_agent**|**sysname**|배포 에이전트의 이름입니다.|  
|**런타임**|**smalldatetime**|배포 에이전트가 마지막으로 업데이트한 시간입니다.|  
|**한**|**nvarchar(255)**|게시에 대한 설명입니다.|  
|**transaction_timestamp**|**varbinary(16)**|내부적으로만 사용됩니다.|  
|**update_mode**|**tinyint**|업데이트의 유형입니다.|  
|**agent_id**|**binary(16)**|에이전트의 ID입니다.|  
|**subscription_guid**|**binary(16)**|게시에 관한 구독 버전의 전역 식별자입니다.|  
|**subid**|**binary(16)**|익명 구독에 관한 전역 식별자입니다.|  
|**immediate_sync**|**bit**|스냅샷 에이전트가 실행될 때마다 동기화 파일을 만들거나 다시 만들지 여부를 나타냅니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Transact-sql&#41;&#40;복제 뷰](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [Transact-sql&#41;sp_helpsubscription &#40;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
