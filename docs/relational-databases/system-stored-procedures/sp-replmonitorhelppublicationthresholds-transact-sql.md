---
title: sp_replmonitorhelppublicationthresholds (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b69d1ae90224b94d5db5f9658942e1beed0b61d1
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58526933"
---
# <a name="spreplmonitorhelppublicationthresholds-transact-sql"></a>sp_replmonitorhelppublicationthresholds(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  모니터링할 게시의 임계값 메트릭 집합을 반환합니다. 복제 모니터링에 사용되는 이 저장 프로시저는 배포 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_replmonitorhelppublicationthresholds [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
    [ , [ @publication_type = ] publication_type ]   
    [ , [ @thresholdmetricname = ] 'thresholdmetricname'  
```  
  
## <a name="arguments"></a>인수  
`[ @publisher = ] 'publisher'` 게시자의 이름이입니다. *게시자* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @publisher_db = ] 'publisher_db'` 게시 데이터베이스의 이름이입니다. *publisher_db* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @publication = ] 'publication'` 게시의 이름이입니다. *게시* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @publication_type = ] publication_type` 경우 게시 유형입니다. *publication_type* 됩니다 **int**, 이며 다음이 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**0**|트랜잭션 게시|  
|**1**|스냅숏 게시|  
|**2**|병합 게시|  
|NULL(기본값)|복제가 게시 유형을 확인하려고 합니다.|  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**metric_id**|**int**|복제 성능 메트릭의 ID이며 다음 중 하나가 될 수 있습니다.<br /><br /> **1expiration** -트랜잭션 게시에 대 한 구독의 만료가 임박 했는지 모니터링 합니다.<br /><br /> **2latency** -트랜잭션 게시에 대 한 구독의 성능 모니터링 합니다.<br /><br /> **4mergeexpiration** -병합 게시에 대 한 구독의 만료가 임박 했는지 모니터링 합니다.<br /><br /> **5mergeslowrunduration** -저대역폭 (전화 접속) 연결을 통한 병합 동기화의 기간을 모니터링 합니다.<br /><br /> **6mergefastrunduration** -고대역폭 (LAN) 연결을 통한 병합 동기화의 기간을 모니터링 합니다.<br /><br /> **7mergefastrunspeed** -고대역폭 (LAN) 연결을 통한 병합 동기화의 동기화 속도 모니터링 합니다.<br /><br /> **8mergeslowrunspeed** -저대역폭 (전화 접속) 연결을 통한 병합 동기화의 동기화 속도 모니터링 합니다.|  
|**title**|**sysname**|복제 성능 메트릭의 이름입니다.|  
|**value**|**int**|복제 성능 메트릭의 임계값입니다.|  
|**shouldalert**|**bit**|메트릭이이 게시에 대해 정의 된 임계값을 초과할 때 경고가 생성 될 경우는 값이 **1** 경고를 발생 해야 하는지 나타냅니다.|  
|**isenabled**|**bit**|이 게시에 대해이 복제 성능 메트릭에 대해 모니터링이 활성화 하는 경우는 값이 **1** 모니터링이 활성화 되었음을 나타냅니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_replmonitorhelppublicationthresholds** 모든 유형의 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **db_owner** 또는 **replmonitor** 고정된 데이터베이스 역할의 배포 데이터베이스를 실행할 수 있습니다 **sp_replmonitorhelppublicationthresholds**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [프로그래밍 방식으로 복제 모니터링](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
