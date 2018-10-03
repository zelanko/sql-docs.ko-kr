---
title: MSpublicationthresholds (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- mspublicationthresholds
- mspublicationthresholds_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpublicationthresholds system table
ms.assetid: 9da3879f-b1f4-4ab4-abd4-a9a8ac395eba
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 133bdbd53cf89b9ebf20260c867e22008b460aae
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47703091"
---
# <a name="mspublicationthresholds-transact-sql"></a>MSpublicationthresholds(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **MSpublicationthresholds** 테이블 모니터링 중인 각 임계값 값에 대해 하나의 행을 사용 하 여 게시에 대 한 복제 성능 메트릭을 추적을 사용 합니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**publication_id**|**int**|임계값이 설정된 게시를 식별합니다.|  
|**metric_id**|**int**|에 정의 된 대로 모니터링 되 고 복제 성능 메트릭을 식별 합니다 [MSreplmonthresholdmetrics](../../relational-databases/system-tables/msreplmonthresholdmetrics-transact-sql.md) 시스템 테이블입니다.|  
|**value**|**sql_variant**|모니터링되는 메트릭의 임계값입니다.|  
|**shouldalert**|**bit**|값이 **1** 메트릭이 정의 된 임계값을 초과할 때 경고를 생성할지를 나타냅니다.|  
|**isenabled**|**bit**|값이 **1** 이 복제 성능 메트릭에 대 한 모니터링이 활성화 되었음을 나타냅니다.|  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
