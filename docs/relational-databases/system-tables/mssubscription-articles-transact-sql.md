---
title: MSsubscription_articles (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
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
- MSsubscription_articles
- MSsubscription_articles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscription_articles system table
ms.assetid: dbc1737f-261e-4017-b9cd-703b9fc4ac78
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: a5f1530091601cb241da7f1e4b1d48e02f699497
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="mssubscriptionarticles-transact-sql"></a>MSsubscription_articles(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSsubscription_articles** 테이블에는 지연된 구독에 있는 아티클에 대 한 정보가 들어 있습니다. 이 테이블은 지연 업데이트와 장애 조치로 지연 업데이트를 사용하는 즉시 업데이트의 복제 유형에 대해서만 채워집니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|이 아티클을 서비스하는 에이전트의 ID입니다.|  
|**artid**|**int**|문서 ID는 **sysarticles** 테이블입니다.|  
|**article**|**sysname**|아티클의 이름을 **sysarticles** 테이블입니다.|  
|**dest_table**|**sysname**|대상 테이블의 이름을 **sysarticles** 테이블입니다.|  
|**소유자**|**sysname**|구독의 소유자입니다.|  
|**cft_table**|**sysname**|지연 업데이트 복제 유형의 경우 이 아티클에 대한 충돌 테이블의 이름입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [복제 테이블 &#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
