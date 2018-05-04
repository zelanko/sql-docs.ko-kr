---
title: sp_replmonitorhelppublicationthresholds (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_replmonitorhelppublicationthresholds
- sp_replmonitorhelppublicationthresholds_TSQL
helpviewer_keywords:
- sp_replmonitorhelppublicationthresholds
ms.assetid: d6b1aa4b-3369-4255-a892-c0e5cc9cb693
caps.latest.revision: 21
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 79e46e7b3dbed1537d5d61aea5def13dba36d5e7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
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
 [ **@publisher**=] **'***게시자***'**  
 게시자의 이름입니다. *게시자* 은 **sysname**, 기본값은 없습니다.  
  
 [ **@publisher_db**=] **'***publisher_db***'**  
 게시된 데이터베이스의 이름입니다. *publisher_db* 은 **sysname**, 기본값은 없습니다.  
  
 [ **@publication**=] **'***게시***'**  
 게시의 이름입니다. *게시* 은 **sysname**, 기본값은 없습니다.  
  
 [ **@publication_type**=] *publication_type*  
 게시의 유형입니다. *publication_type* 은 **int**, 다음이 값 중 하나일 수 있습니다.  
  
|Value|설명|  
|-----------|-----------------|  
|**0**|트랜잭션 게시|  
|**1**|스냅숏 게시|  
|**2**|병합 게시|  
|NULL(기본값)|복제에서 게시 유형을 확인하려고 합니다.|  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**metric_id**|**int**|복제 성능 메트릭의 ID이며 다음 중 하나가 될 수 있습니다.<br /><br /> **1expiration** -트랜잭션 게시에 대 한 구독의 만료가 임박 했는지 모니터링 합니다.<br /><br /> **2latency** -한 트랜잭션 게시에 대 한 구독의 성능 모니터링 합니다.<br /><br /> **4mergeexpiration** -병합 게시에 대 한 구독의 만료가 임박 했는지 모니터링 합니다.<br /><br /> **5mergeslowrunduration** -저대역폭 (전화 접속) 연결을 통한 병합 동기화의 기간을 모니터링 합니다.<br /><br /> **6mergefastrunduration** -고대역폭 (LAN) 연결을 통한 병합 동기화의 기간을 모니터링 합니다.<br /><br /> **7mergefastrunspeed** -고대역폭 (LAN) 연결을 통한 병합 동기화의 동기화 속도 모니터링 합니다.<br /><br /> **8mergeslowrunspeed** -저대역폭 (전화 접속) 연결을 통한 병합 동기화의 동기화 속도 모니터링 합니다.|  
|**title**|**sysname**|복제 성능 메트릭의 이름입니다.|  
|**value**|**int**|복제 성능 메트릭의 임계값입니다.|  
|**shouldalert**|**bit**|에 대 한 메트릭을;이 게시에 대해 정의 된 임계값을 초과 하는 경우 경고를 생성할지 여부는 값이 **1** 경고는 발생 수를 나타냅니다.|  
|**isenabled**|**bit**|이 게시에 대 한 해당 복제 성능 메트릭에 대해 모니터링이 활성화 하는 경우에 값이 **1** 모니터링이 활성화 되었음을 나타냅니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_replmonitorhelppublicationthresholds** 모든 유형의 복제와 함께 사용 됩니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **db_owner** 또는 **replmonitor** 배포 데이터베이스의 고정된 데이터베이스 역할을 실행할 수 있는 **sp_replmonitorhelppublicationthresholds**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [프로그래밍 방식으로 복제 모니터링](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
