---
description: MSreplmonthresholdmetrics(Transact-SQL)
title: MSreplmonthresholdmetrics (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- msreplmonthresholdmetrics_TSQL
- msreplmonthresholdmetrics
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplmonthresholdmetrics system table
ms.assetid: 0cc9b40a-36ce-485b-9bc2-d4abd5aa6727
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c58ed139f1ff0b35b190593c14ca360e065061f7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88454612"
---
# <a name="msreplmonthresholdmetrics-transact-sql"></a>MSreplmonthresholdmetrics(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSreplmonthresholdmetrics** 테이블은 복제 모니터링을 위해 제공 되는 메트릭을 정의 합니다. 이 테이블은 **msdb** 데이터베이스에 저장 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**metric_id**|**int**|복제 성능 메트릭을 식별하며 다음 값 중 하나일 수 있습니다.<br /><br /> **1** = 만료<br /><br /> **2** = 대기 시간<br /><br /> **4** = mergeexpiration<br /><br /> **5** = mergeslowrunduration<br /><br /> **6** = mergefastrunduration<br /><br /> **7** = mergefastrunspeed<br /><br /> **8** = mergeslowrunspeed|  
|**title**|**sysname**|복제 성능 메트릭의 이름입니다.|  
|**warningbitstatus**|**int**|다음 메트릭 중 하나에 대한 임계값 위반 경고를 제공하는 데 사용되는 비트 단위 식별자입니다.<br /><br /> **1** = 만료-트랜잭션 게시에 대 한 구독이 허용 된 임계값 (보존 기간에 대 한 비율) 이상 보존 기간을 초과 했습니다.<br /><br /> **2** = latency-트랜잭션 게시자에서 구독자로 데이터를 복제 하는 데 소요 된 시간이 임계값 (초)을 초과 합니다.<br /><br /> **4** = mergeexpiration-병합 게시에 대 한 구독이 허용 된 임계값 (보존 기간에 대 한 비율) 이상 보존 기간을 초과 했습니다.<br /><br /> **8** = mergefastrunduration-고속 네트워크 연결을 통해 병합 구독의 동기화를 완료 하는 데 소요 된 시간이 임계값 (초)을 초과 합니다.<br /><br /> **16** = mergeslowrunduration-저속 또는 전화 접속 네트워크 연결을 통해 병합 구독의 동기화를 완료 하는 데 소요 된 시간이 임계값 (초)을 초과 합니다.<br /><br /> **32** = mergefastrunspeed-고속 네트워크 연결을 통해 병합 구독을 동기화 하는 동안 행의 배달 속도가 임계값 속도 (초당 행 수)를 유지 하지 못했습니다.<br /><br /> **64** = mergeslowrunspeed-저속 또는 전화 접속 네트워크 연결을 통해 병합 구독을 동기화 하는 동안 행의 배달 속도가 임계값 속도 (초당 행 수)를 유지 하지 못했습니다.|  
|**alertmessageid**|**int**|임계값 경고 조건이 발생할 때 표시되는 오류 메시지의 ID입니다.|  
|**description**|**nvarchar (3000)**|복제 성능 메트릭에 대한 설명입니다.|  
|**default_value**|**sql_variant**|복제 성능 메트릭에 대한 기본값입니다.|  
|**min_value**|**sql_variant**|바인딩된 복제 성능 메트릭에 대한 최소값입니다.|  
|**max_value**|**sql_variant**|바인딩된 복제 성능 메트릭에 대한 최대값입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블 ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
