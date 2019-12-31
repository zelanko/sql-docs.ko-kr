---
title: sp_replmonitorchangepublicationthreshold (T-sql)
description: 게시에 대 한 모니터링 임계값 메트릭을 변경 하는 sp_replmonitorchangepublicationthreshold 저장 프로시저에 대해 설명 합니다.
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorchangepublicationthreshold_TSQL
- sp_replmonitorchangepublicationthreshold
helpviewer_keywords:
- sp_replmonitorchangepublicationthreshold
ms.assetid: 2c3615d8-4a1a-4162-b096-97aefe6ddc16
author: stevestein
ms.author: sstein
ms.openlocfilehash: fdcf5a9dcd462562886c7815b500c43145b749a3
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2019
ms.locfileid: "75322240"
---
# <a name="sp_replmonitorchangepublicationthreshold-transact-sql"></a>sp_replmonitorchangepublicationthreshold(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  게시에 대한 모니터링 임계값 메트릭을 변경합니다. 복제 모니터링에 사용되는 이 저장 프로시저는 배포 데이터베이스의 배포자에서 실행됩니다.  
  
 ![토픽 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-sql 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_replmonitorchangepublicationthreshold [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
    [ , [ @publication_type = ] publication_type ]   
    [ , [ @metric_id = ] metric_id ]   
    [ , [ @thresholdmetricname = ] 'thresholdmetricname'   
    [ , [ @value = ] value ]   
    [ , [ @shouldalert = ] shouldalert ]   
    [ , [ @mode = ] mode ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publisher = ] 'publisher'`게시자의 이름입니다. *publisher* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publisher_db = ] 'publisher_db'`게시 된 데이터베이스의 이름입니다. *publisher_db* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publication = ] 'publication'`모니터링 임계값 특성이 변경 되는 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publication_type = ] publication_type`게시의 유형입니다. *publication_type* 은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
|Value|설명|  
|-----------|-----------------|  
|**0**|트랜잭션 게시|  
|**1(sp1)**|스냅샷 게시|  
|**sr-2**|병합 게시|  
|NULL(기본값)|복제에서 게시 유형을 확인하려고 합니다.|  
  
`[ @metric_id = ] metric_id`변경 중인 게시 임계값 메트릭의 ID입니다. *metric_id* 은 **int**이며 기본값은 NULL이 고 다음 값 중 하나일 수 있습니다.  
  
|Value|메트릭 이름|  
|-----------|-----------------|  
|**1(sp1)**|**만료** -트랜잭션 게시에 대 한 구독의 만료가 임박 했는지 모니터링 합니다.|  
|**sr-2**|**latency** -트랜잭션 게시에 대 한 구독의 성능을 모니터링 합니다.|  
|**3-4**|**mergeexpiration** -병합 게시에 대 한 구독의 만료가 임박 했는지 모니터링 합니다.|  
|**5**|**mergeslowrunduration** -저대역폭 (전화 접속) 연결을 통한 병합 동기화의 기간을 모니터링 합니다.|  
|**6**|**mergefastrunduration** -고대역폭 lan (local area network) 연결을 통한 병합 동기화의 기간을 모니터링 합니다.|  
|**일**|**mergefastrunspeed** -고대역폭 (LAN) 연결을 통한 병합 동기화의 동기화 속도를 모니터링 합니다.|  
|**20cm(8**|**mergeslowrunspeed** -저대역폭 (전화 접속) 연결을 통한 병합 동기화의 동기화 속도를 모니터링 합니다.|  
  
 *Metric_id* 또는 *thresholdmetricname*중 하나를 지정 해야 합니다. *Thresholdmetricname* 를 지정 하는 경우 *metric_id* 은 NULL 이어야 합니다.  
  
`[ @thresholdmetricname = ] 'thresholdmetricname'`변경 중인 게시 임계값 메트릭의 이름입니다. *thresholdmetricname* 는 **sysname**이며 기본값은 NULL입니다. *Thresholdmetricname* 또는 *metric_id*중 하나를 지정 해야 합니다. *Metric_id* 지정 된 경우 *thresholdmetricname* 는 NULL 이어야 합니다.  
  
`[ @value = ] value`게시 임계값 메트릭의 새 값입니다. *값* 은 **int**이며 기본값은 NULL입니다. **Null**인 경우 메트릭 값은 업데이트 되지 않습니다.  
  
`[ @shouldalert = ] shouldalert`게시 임계값 메트릭에 도달 하면 경고가 생성 되는지 여부입니다. *shouldalert* 은 **bit**이며 기본값은 NULL입니다. 값이 **1** 이면 경고가 생성 되 고 값이 **0** 이면 경고가 생성 되지 않습니다.  
  
`[ @mode = ] mode`게시 임계값 메트릭이 활성화 되어 있는지 여부입니다. *mode* 는 **tinyint**이며 기본값은 **1**입니다. 값이 **1** 이면이 메트릭에 대 한 모니터링이 사용 하도록 설정 되 고 값이 **2** 이면이 메트릭에 대 한 모니터링이 사용 되지 않음을 의미 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_replmonitorchangepublicationthreshold** 은 모든 유형의 복제에 사용 됩니다.  
  
## <a name="permissions"></a>권한  
 배포 데이터베이스에서 **db_owner** 또는 **replmonitor** 고정 데이터베이스 역할의 멤버만 **sp_replmonitorchangepublicationthreshold**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [프로그래밍 방식으로 복제 모니터링](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
