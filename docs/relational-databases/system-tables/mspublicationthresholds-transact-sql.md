---
title: MSpublicationthresholds (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
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
- mspublicationthresholds
- mspublicationthresholds_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpublicationthresholds system table
ms.assetid: 9da3879f-b1f4-4ab4-abd4-a9a8ac395eba
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: cda79bde63b4f9ca7b33348374cd00e92d79c1a2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="mspublicationthresholds-transact-sql"></a>MSpublicationthresholds(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSpublicationthresholds** 테이블은 모니터링 되는 각 임계값에 대 한 행이 하나씩 있는 게시에 대 한 복제 성능 메트릭을 추적 하는 데 사용 됩니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**publication_id**|**int**|임계값이 설정된 게시를 식별합니다.|  
|**metric_id**|**int**|에 정의 되어 있는 모니터링 되는 복제 성능 메트릭을 식별 된 [MSreplmonthresholdmetrics](../../relational-databases/system-tables/msreplmonthresholdmetrics-transact-sql.md) 시스템 테이블입니다.|  
|**value**|**sql_variant**|모니터링되는 메트릭의 임계값입니다.|  
|**shouldalert**|**bit**|값이 **1** 메트릭을 정의 된 임계값을 초과 하는 경우 경고를 생성할지를 나타냅니다.|  
|**isenabled**|**bit**|값이 **1** 이 복제 성능 메트릭에 대해 모니터링이 활성화 되었음을 나타냅니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [복제 테이블 &#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
