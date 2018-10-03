---
title: MSreplmonthresholdmetrics (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- msreplmonthresholdmetrics_TSQL
- msreplmonthresholdmetrics
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplmonthresholdmetrics system table
ms.assetid: 0cc9b40a-36ce-485b-9bc2-d4abd5aa6727
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 90d750d05af52b051bfcba4778f4aba7c911753e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47777261"
---
# <a name="msreplmonthresholdmetrics-transact-sql"></a>MSreplmonthresholdmetrics(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **MSreplmonthresholdmetrics** 테이블 복제 모니터링에 대 한 제공 된 메트릭을 정의 합니다. 이 테이블에 저장 되는 **msdb** 데이터베이스입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**metric_id**|**int**|복제 성능 메트릭을 식별하며 다음 값 중 하나일 수 있습니다.<br /><br /> **1** = expiration-<br /><br /> **2** 대기 시간 =<br /><br /> **4** mergeexpiration =<br /><br /> **5** = mergeslowrunduration<br /><br /> **6** = mergefastrunduration<br /><br /> **7** = mergefastrunspeed<br /><br /> **8** mergeslowrunspeed =|  
|**title**|**sysname**|복제 성능 메트릭의 이름입니다.|  
|**warningbitstatus**|**int**|다음 메트릭 중 하나에 대한 임계값 위반 경고를 제공하는 데 사용되는 비트 단위 식별자입니다.<br /><br /> **1** = expiration-트랜잭션 게시에 구독 보존 기간의 백분율 허용 된 임계값 이상 보존 기간을 초과 했습니다.<br /><br /> **2** = latency – 트랜잭션 게시자에서 구독자로 데이터를 복제 하는 데 걸린 시간 (초)에서의 임계값을 초과 합니다.<br /><br /> **4** = mergeexpiration-병합 게시에 대 한 구독 보존 기간의 백분율 허용 된 임계값 이상 보존 기간을 초과 했습니다.<br /><br /> **8** = mergefastrunduration – 병합 구독을 완전 동기화 하는 데 걸린 시간 (초), 고속 네트워크 연결을 통해, 임계값을 초과 합니다.<br /><br /> **16** = mergeslowrunduration – 병합 구독을 완전 동기화 하는 데 걸린 시간 (초), 저속 또는 전화 접속 네트워크 연결을 통해, 임계값을 초과 합니다.<br /><br /> **32** = mergefastrunspeed-의 배달 속도가 임계 속도 초당 행 고속 네트워크 연결을 통해 유지 관리 못했습니다 병합 구독을 동기화 하는 동안 행.<br /><br /> **64** = mergeslowrunspeed-의 배달 속도가 병합 구독을 동기화 하는 동안 행에 저속 또는 전화 접속 네트워크 연결을 통해 초당 행에서 임계 속도 유지 하지 못했습니다.|  
|**alertmessageid**|**int**|임계값 경고 조건이 발생할 때 표시되는 오류 메시지의 ID입니다.|  
|**description**|**nvarchar(3000)**|복제 성능 메트릭에 대한 설명입니다.|  
|**default_value**|**sql_variant**|복제 성능 메트릭에 대한 기본값입니다.|  
|**min_value**|**sql_variant**|바인딩된 복제 성능 메트릭에 대한 최소값입니다.|  
|**max_value**|**sql_variant**|바인딩된 복제 성능 메트릭에 대한 최대값입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
