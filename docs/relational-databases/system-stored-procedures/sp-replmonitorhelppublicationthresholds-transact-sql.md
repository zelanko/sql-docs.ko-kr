---
title: sp_replmonitorhelppublicationthresholds (T-sql)
description: 모니터링 되는 게시에 대해 설정 된 임계값 메트릭을 반환 하는 sp_replmonitorhelppublicationthresholds 저장 프로시저에 대해 설명 합니다.
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorhelppublicationthresholds
- sp_replmonitorhelppublicationthresholds_TSQL
helpviewer_keywords:
- sp_replmonitorhelppublicationthresholds
ms.assetid: d6b1aa4b-3369-4255-a892-c0e5cc9cb693
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a41b93878178bd47574acc7ae11da69e11c76016
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543130"
---
# <a name="sp_replmonitorhelppublicationthresholds-transact-sql"></a>sp_replmonitorhelppublicationthresholds(Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  모니터링할 게시의 임계값 메트릭 집합을 반환합니다. 복제 모니터링에 사용되는 이 저장 프로시저는 배포 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_replmonitorhelppublicationthresholds [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
    [ , [ @publication_type = ] publication_type ]   
    [ , [ @thresholdmetricname = ] 'thresholdmetricname'  
```  
  
## <a name="arguments"></a>인수  
`[ @publisher = ] 'publisher'` 게시자의 이름입니다. *publisher* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publisher_db = ] 'publisher_db'` 게시 된 데이터베이스의 이름입니다. *publisher_db* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publication = ] 'publication'` 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publication_type = ] publication_type` 게시의 유형입니다. *publication_type* 은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**0**|트랜잭션 게시|  
|**1**|스냅샷 게시|  
|**2**|병합 게시|  
|NULL(기본값)|복제가 게시 유형을 확인하려고 합니다.|  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**metric_id**|**int**|복제 성능 메트릭의 ID이며 다음 중 하나가 될 수 있습니다.<br /><br /> **1 만료** -트랜잭션 게시에 대 한 구독의 만료가 임박 했는지 모니터링 합니다.<br /><br /> **2 대기 시간** -트랜잭션 게시에 대 한 구독의 성능을 모니터링 합니다.<br /><br /> **4mergeexpiration** -병합 게시에 대 한 구독의 만료가 임박 했는지 모니터링 합니다.<br /><br /> **5mergeslowrunduration** -저대역폭 (전화 접속) 연결을 통한 병합 동기화의 기간을 모니터링 합니다.<br /><br /> **6mergefastrunduration** -고대역폭 (LAN) 연결을 통한 병합 동기화의 기간을 모니터링 합니다.<br /><br /> **7mergefastrunspeed** -고대역폭 (LAN) 연결을 통한 병합 동기화의 동기화 속도를 모니터링 합니다.<br /><br /> **8mergeslowrunspeed** -저대역폭 (전화 접속) 연결을 통한 병합 동기화의 동기화 속도를 모니터링 합니다.|  
|**title**|**sysname**|복제 성능 메트릭의 이름입니다.|  
|**value**|**int**|복제 성능 메트릭의 임계값입니다.|  
|**shouldalert**|**bit**|메트릭이이 게시에 대해 정의 된 임계값을 초과할 때 경고를 생성 해야 하는지 여부입니다. 값 **1** 은 경고가 발생 해야 함을 나타냅니다.|  
|**isenabled**|**bit**|이 게시에 대 한이 복제 성능 메트릭에 대해 모니터링을 사용할 수 있는지 여부입니다. 값이 **1** 이면 모니터링이 사용 하도록 설정 되어 있음을 나타냅니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_replmonitorhelppublicationthresholds** 은 모든 유형의 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 배포 데이터베이스에서 **db_owner** 또는 **replmonitor** 고정 데이터베이스 역할의 멤버만 **sp_replmonitorhelppublicationthresholds**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [프로그래밍 방식으로 복제 모니터링](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
