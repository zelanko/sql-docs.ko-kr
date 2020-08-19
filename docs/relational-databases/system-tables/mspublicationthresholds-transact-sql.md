---
description: MSpublicationthresholds(Transact-SQL)
title: MSpublicationthresholds (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- mspublicationthresholds
- mspublicationthresholds_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpublicationthresholds system table
ms.assetid: 9da3879f-b1f4-4ab4-abd4-a9a8ac395eba
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 799c068d066fdab518a355552ead5ed5a9fde8af
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88427655"
---
# <a name="mspublicationthresholds-transact-sql"></a>MSpublicationthresholds(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSpublicationthresholds** 테이블은 게시에 대 한 복제 성능 메트릭을 추적 하는 데 사용 되며 모니터링 되는 각 임계값에 대해 하나의 행을 포함 합니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**publication_id**|**int**|임계값이 설정된 게시를 식별합니다.|  
|**metric_id**|**int**|[MSreplmonthresholdmetrics](../../relational-databases/system-tables/msreplmonthresholdmetrics-transact-sql.md) 시스템 테이블에 정의 된 대로 모니터링 되는 복제 성능 메트릭을 식별 합니다.|  
|**value**|**sql_variant**|모니터링되는 메트릭의 임계값입니다.|  
|**shouldalert**|**bit**|값 **1** 은 메트릭이 정의 된 임계값을 초과할 때 경고를 생성 해야 함을 나타냅니다.|  
|**isenabled**|**bit**|값 **1** 은이 복제 성능 메트릭에 대해 모니터링이 사용 하도록 설정 되어 있음을 나타냅니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블 ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
