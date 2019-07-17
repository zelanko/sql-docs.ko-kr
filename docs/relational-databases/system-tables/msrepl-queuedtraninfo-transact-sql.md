---
title: MSrepl_queuedtraninfo (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSrepl_queuedtraninfo_TSQL
- MSrepl_queuedtraninfo
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_queuedtraninfo system table
ms.assetid: af7a5baf-32ea-475f-b6b9-68c557b4980c
author: stevestein
ms.author: sstein
ms.openlocfilehash: a94163e2fe4a1ed5be77dd4ae99f43d03cc35121
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079172"
---
# <a name="msreplqueuedtraninfo-transact-sql"></a>MSrepl_queuedtraninfo(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **Msreplication_queue** 테이블은 복제 프로세스에서 모든 지연된 업데이트 구독에서 SQL 기반의 지연 업데이트를 사용 하는 발급 된 대기 중인된 명령에 대 한 정보를 저장 하는 데 사용 됩니다. 이 테이블은 구독 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|게시자의 이름입니다.|  
|**publisher_db**|**sysname**|게시 데이터베이스의 이름입니다.|  
|**publication**|**sysname**|게시의 이름입니다.|  
|**tranid**|**sysname**|대기 중인 명령이 실행된 트랜잭션 ID입니다.|  
|**maxorderkey**|**bigint**|내부적으로만 사용됩니다.|  
|**commandcount**|**bigint**|내부적으로만 사용됩니다.|  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
