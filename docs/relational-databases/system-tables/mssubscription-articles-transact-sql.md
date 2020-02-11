---
title: MSsubscription_articles (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsubscription_articles
- MSsubscription_articles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscription_articles system table
ms.assetid: dbc1737f-261e-4017-b9cd-703b9fc4ac78
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8518c787f876152787ee30a20b9f25f936b9fa86
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68139782"
---
# <a name="mssubscription_articles-transact-sql"></a>MSsubscription_articles(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSsubscription_articles** 테이블에는 대기 중인 구독의 아티클에 대 한 정보가 포함 되어 있습니다. 이 테이블은 지연 업데이트와 장애 조치로 지연 업데이트를 사용하는 즉시 업데이트의 복제 유형에 대해서만 채워집니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|이 아티클을 서비스하는 에이전트의 ID입니다.|  
|**artid**|**int**|**Sysarticles** 테이블의 문서 ID입니다.|  
|**자료**|**sysname**|**Sysarticles** 테이블의 아티클 이름입니다.|  
|**dest_table**|**sysname**|**Sysarticles** 테이블에서 대상 테이블의 이름입니다.|  
|**소유자도**|**sysname**|구독의 소유자입니다.|  
|**cft_table**|**sysname**|지연 업데이트 복제 유형의 경우 이 아티클에 대한 충돌 테이블의 이름입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
