---
title: MSreplication_monitordata (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSreplication_monitordata_TSQL
- MSreplication_monitordata
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplication_monitordata system table
ms.assetid: 843d3ffd-a1ef-4fd5-a744-c2252199793e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 886240176188fdcea0c104ca366ec5451528312a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68079139"
---
# <a name="msreplication_monitordata-transact-sql"></a>MSreplication_monitordata(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSreplication_monitordata** 테이블에는 복제 모니터에서 사용 하는 캐시 된 데이터와 모니터링 되는 각 구독에 대 한 행이 하나씩 포함 되어 있습니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**lastrefresh**|**datetime**|모니터 데이터를 새로 고친 날짜와 시간입니다.|  
|**computetime**|**int**|모니터 데이터를 계산하는 데 소요된 시간(초)입니다.|  
|**publication_id**|**int**|게시 ID입니다.|  
|**발행자**|**sysname**|게시자의 이름입니다.|  
|**publisher_srvid**|**int**|게시자의 서버 ID입니다.|  
|**publisher_db**|**sysname**|게시 데이터베이스의 이름입니다.|  
|**게시물**|**sysname**|게시의 이름입니다.|  
|**publication_type**|**int**|게시 유형으로 다음 값 중 하나일 수 있습니다.<br /><br /> **0** = 트랜잭션 게시<br /><br /> **1** = 스냅숏 게시<br /><br /> **2** = 병합 게시|  
|**agent_type**|**int**|복제 에이전트 유형으로 다음 값 중 하나일 수 있습니다.<br /><br /> **1** = 스냅숏 에이전트<br /><br /> **2** = 로그 판독기 에이전트<br /><br /> **3** = 배포 에이전트<br /><br /> **4** = 병합 에이전트<br /><br /> **9** = 큐 판독기 에이전트|  
|**agent_id**|**int**|복제 에이전트의 ID입니다.|  
|**agent_name**|**sysname**|복제 에이전트 작업의 이름입니다.|  
|**job_id**|**uniqueidentifier**|복제 에이전트 작업의 GUID입니다.|  
|**status**|**int**|복제 에이전트 상태로 다음 값 중 하나일 수 있습니다.<br /><br /> **1** = 시작 됨<br /><br /> **2** = 성공<br /><br /> **3** = 진행 중<br /><br /> **4** = 유휴 상태<br /><br /> **5** = 다시 시도 중<br /><br /> **6** = 실패|  
|**isagentrunningnow**|**bit**|에이전트 작업이 현재 실행 중인지 여부를 나타내는 플래그입니다. 값 **1** 은 작업이 실행 중임을 의미 합니다.|  
|**warning**|**int**|구독에서 생성한 임계값 경고로 다음 값 중 하나 이상의 논리 OR 결과일 수 있습니다.<br /><br /> **1** = 만료-트랜잭션 게시에 대 한 구독이 허용 된 임계값 (보존 기간에 대 한 비율) 이상 보존 기간을 초과 했습니다.<br /><br /> **2** = latency-트랜잭션 게시자에서 구독자로 데이터를 복제 하는 데 소요 된 시간이 임계값 (초)을 초과 합니다.<br /><br /> **4** = mergeexpiration-병합 게시에 대 한 구독이 허용 된 임계값 (보존 기간에 대 한 비율) 이상 보존 기간을 초과 했습니다. 8 = mergefastrunduration - 고속 네트워크 연결을 통해 병합 구독을 완전 동기화하는 데 소요된 시간이 임계값(초)을 초과합니다.<br /><br /> **16** = mergeslowrunduration-저속 또는 전화 접속 네트워크 연결을 통해 병합 구독의 동기화를 완료 하는 데 소요 된 시간이 임계값 (초)을 초과 합니다.<br /><br /> **32** = mergefastrunspeed-고속 네트워크 연결을 통해 병합 구독을 동기화 하는 동안 행의 배달 속도가 임계값 속도 (초당 행 수)를 유지 하지 못했습니다.<br /><br /> **64** = mergeslowrunspeed-저속 또는 전화 접속 네트워크 연결을 통해 병합 구독을 동기화 하는 동안 행의 배달 속도가 임계값 속도 (초당 행 수)를 유지 하지 못했습니다.|  
|**last_distsync**|**datetime**|배포 에이전트를 마지막으로 실행한 날짜와 시간입니다.|  
|**agentstoptime**|**datetime**|에이전트를 중지한 날짜와 시간입니다.|  
|**distdb**|**sysname**|구독에 대한 배포 데이터베이스의 이름입니다.|  
|**보존**|**int**|게시의 보존 기간입니다.|  
|**time_stamp**|**datetime**|내부적으로만 사용됩니다.|  
|**worst_latency**|**int**|트랜잭션 게시에 대해 로그 판독기 또는 배포 에이전트가 전파하는 데이터 변경에 대한 최대 대기 시간(초)입니다.|  
|**best_latency**|**int**|트랜잭션 게시에 대해 로그 판독기 또는 배포 에이전트가 전파하는 데이터 변경에 대한 최소 대기 시간(초)입니다.|  
|**avg_latency**|**int**|트랜잭션 게시에 대해 로그 판독기 또는 배포 에이전트가 전파하는 데이터 변경에 대한 평균 대기 시간(초)입니다.|  
|**cur_latency**|**int**|현재 실행하는 동안 로그 판독기 또는 배포 에이전트가 전파하는 데이터 변경에 대한 대기 시간(초)입니다.|  
|**worst_runspeedPerf**|**int**|병합 게시에 대한 가장 긴 동기화 시간입니다.|  
|**best_runspeedPerf**|**int**|병합 게시에 대한 가장 짧은 동기화 시간입니다.|  
|**average_runspeedPerf**|**int**|병합 게시에 대한 평균 동기화 시간입니다.|  
|**mergePerformance**|**int**|구독에 대한 모든 동기화 성능과 비교한 최근 동기화의 성능입니다. 최근 동기화의 배달 속도를 이전의 모든 배달 속도 평균으로 나눈 값을 기반으로 합니다.|  
|**mergelatestsessionrunduration**|**int**|가장 최근에 병합 에이전트를 실행한 기간입니다.|  
|**mergelatestsessionrunspeed**|**float (53)**|가장 최근에 실행한 병합 에이전트의 배달 속도입니다.|  
|**mergelatestsessionconnectiontype**|**int**|가장 최근에 병합 에이전트 세션에 사용한 연결로 다음 값 중 하나일 수 있습니다.<br /><br /> **1** = lan (local area network)<br /><br /> **2** = 전화 접속 네트워크 연결|  
|**retention_period_unit**|**tinyint**|보존 기간을 정의할 때 사용할 단위를 지정합니다. 다음 값 중 하나일 수 있습니다.<br /><br /> **1** = 주<br /><br /> **2** = 개월<br /><br /> **3** = 년|  
  
## <a name="see-also"></a>참고 항목  
 [프로그래밍 방식으로 복제 모니터링](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)   
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Transact-sql&#41;&#40;복제 뷰](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [Transact-sql&#41;sp_replmonitorhelpsubscription &#40;](../../relational-databases/system-stored-procedures/sp-replmonitorhelpsubscription-transact-sql.md)   
 [Transact-sql&#41;sp_replmonitorhelppublication &#40;](../../relational-databases/system-stored-procedures/sp-replmonitorhelppublication-transact-sql.md)   
 [Transact-sql&#41;sp_replmonitorhelppublisher &#40;](../../relational-databases/system-stored-procedures/sp-replmonitorhelppublisher-transact-sql.md)   
 [Transact-sql&#41;sp_replmonitorhelpmergesession &#40;](../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesession-transact-sql.md)   
 [Transact-sql&#41;sp_replmonitorhelppublicationthresholds &#40;](../../relational-databases/system-stored-procedures/sp-replmonitorhelppublicationthresholds-transact-sql.md)   
 [Transact-sql&#41;sp_replmonitorhelpmergesessiondetail &#40;](../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesessiondetail-transact-sql.md)  
  
  
