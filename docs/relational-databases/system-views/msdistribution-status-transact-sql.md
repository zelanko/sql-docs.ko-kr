---
title: MSdistribution_status (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- MSdistribution_status_TSQL
- MSdistribution_status
dev_langs:
- TSQL
helpviewer_keywords:
- MSdistribution_status view
ms.assetid: 90d447de-3a4a-4f3e-aeab-e8fff6348361
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d497a85e82e35658c14be59734f0c1ab05e1914a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47826641"
---
# <a name="msdistributionstatus-transact-sql"></a>MSdistribution_status(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **MSdistribution_status** 뷰는 배포 데이터베이스에 상태 명령에 대 한 추가 정보를 표시 합니다. 이 뷰는 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**article_id**|**int**|아티클을 식별합니다.|  
|**agent_id**|**int**|복제 에이전트를 식별합니다.|  
|**UndelivCmdsInDistDB**|**int**|구독자에 대한 배달을 보류 중인 명령 수입니다.|  
|**DelivCmdsInDistDB**|**int**|구독자로 배달된 명령 수입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
