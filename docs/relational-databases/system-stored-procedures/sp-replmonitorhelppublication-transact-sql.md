---
title: sp_replmonitorhelppublication (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorhelppublication_TSQL
- sp_replmonitorhelppublication
helpviewer_keywords:
- sp_replmonitorhelppublication
ms.assetid: 7928c50c-617f-41c5-9e0f-4e42e8be55dc
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8dc952f03ea2538412c864e1a9e9b228bf3ca877
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68771208"
---
# <a name="sp_replmonitorhelppublication-transact-sql"></a>sp_replmonitorhelppublication(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  게시자에 있는 하나 이상의 게시에 대한 현재 상태 정보를 반환합니다. 복제 모니터링에 사용되는 이 저장 프로시저는 배포 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_replmonitorhelppublication [ @publisher = ] 'publisher'  
    [ , [ @publisher_db = ] 'publisher_db'   
    [ , [ @publication = ] 'publication'   
    [ , [ @publication_type = ] publication_type ]   
    [ , [ @refreshpolicy = ] refreshpolicy ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publisher = ] 'publisher'`상태를 모니터링 하는 게시자의 이름입니다. *publisher* 는 **sysname**이며 기본값은 NULL입니다. **Null**인 경우 배포자를 사용 하는 모든 게시자에 대해 정보가 반환 됩니다.  
  
`[ @publisher_db = ] 'publisher_db'`게시 된 데이터베이스의 이름입니다. *publisher_db* 는 **sysname**이며 기본값은 NULL입니다. NULL인 경우 게시자에 게시된 모든 데이터베이스에 대한 정보가 반환됩니다.  
  
`[ @publication = ] 'publication'`모니터링 되는 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @publication_type = ] publication_type`게시의 유형입니다. *publication_type* 은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**0**|트랜잭션 게시|  
|**1**|스냅샷 게시|  
|**2**|병합 게시|  
|NULL(기본값)|복제에서 게시 유형을 확인하려고 합니다.|  
  
`[ @refreshpolicy = ] refreshpolicy`내부용 으로만 사용 됩니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**publisher_db**|**sysname**|게시자의 이름입니다.|  
|**게시물**|**sysname**|게시의 이름입니다.|  
|**publication_type**|**int**|게시 유형이며 다음 값 중 하나일 수 있습니다.<br /><br /> **0** = 트랜잭션 게시<br /><br /> **1** = 스냅숏 게시<br /><br /> **2** = 병합 게시|  
|**status**|**int**|게시와 연관된 모든 복제 에이전트의 최대 상태로 다음 값 중 하나일 수 있습니다.<br /><br /> **1** = 시작 됨<br /><br /> **2** = 성공<br /><br /> **3** = 진행 중<br /><br /> **4** = 유휴 상태<br /><br /> **5** = 다시 시도 중<br /><br /> **6** = 실패|  
|**warning**|**int**|게시에 속한 구독에서 생성한 최대 임계값 경고로 다음 값 중 하나 이상의 논리 OR 결과일 수 있습니다.<br /><br /> **1** = 만료-트랜잭션 게시에 대 한 구독이 보존 기간 임계값 내에서 동기화 되지 않았습니다.<br /><br /> **2** = latency-트랜잭션 게시자에서 구독자로 데이터를 복제 하는 데 소요 된 시간이 임계값 (초)을 초과 합니다.<br /><br /> **4** = mergeexpiration-병합 게시에 대 한 구독이 보존 기간 임계값 내에서 동기화 되지 않았습니다.<br /><br /> **8** = mergefastrunduration-고속 네트워크 연결을 통해 병합 구독의 동기화를 완료 하는 데 소요 된 시간이 임계값 (초)을 초과 합니다.<br /><br /> **16** = mergeslowrunduration-저속 또는 전화 접속 네트워크 연결을 통해 병합 구독의 동기화를 완료 하는 데 소요 된 시간이 임계값 (초)을 초과 합니다.<br /><br /> **32** = mergefastrunspeed-고속 네트워크 연결을 통해 병합 구독을 동기화 하는 동안 행의 배달 속도가 임계값 속도 (초당 행 수)를 유지 하지 못했습니다.<br /><br /> **64** = mergeslowrunspeed-저속 또는 전화 접속 네트워크 연결을 통해 병합 구독을 동기화 하는 동안 행의 배달 속도가 임계값 속도 (초당 행 수)를 유지 하지 못했습니다.|  
|**worst_latency**|**int**|트랜잭션 게시에 대해 로그 판독기 또는 배포 에이전트가 전파하는 데이터 변경에 대한 최대 대기 시간(초)입니다.|  
|**best_latency**|**int**|트랜잭션 게시에 대해 로그 판독기 또는 배포 에이전트가 전파하는 데이터 변경에 대한 최소 대기 시간(초)입니다.|  
|**average_latency**|**int**|트랜잭션 게시에 대해 로그 판독기 또는 배포 에이전트가 전파하는 데이터 변경에 대한 평균 대기 시간(초)입니다.|  
|**last_distsync**|**datetime**|배포 에이전트를 실행한 마지막 날짜/시간입니다.|  
|**보존**|**int**|게시의 보존 기간입니다.|  
|**latencythreshold**|**int**|트랜잭션 게시에 대해 설정된 대기 시간 임계값입니다.|  
|**expirationthreshold**|**int**|병합 게시인 경우 게시에 대해 설정된 만료 임계값입니다.|  
|**agentnotrunningthreshold**|**int**|에이전트를 실행하지 않을 가장 긴 시간에 대해 설정된 임계값입니다.|  
|**subscriptioncount**|**int**|게시에 대한 구독 수입니다.|  
|**runningdistagentcount**|**int**|게시에 대해 실행되는 배포 에이전트 수입니다.|  
|**snapshot_agentname**|**sysname**|게시에 대한 스냅샷 에이전트 작업의 이름입니다.|  
|**logreader_agentname**|**sysname**|트랜잭션 게시에 대한 로그 판독기 에이전트 작업의 이름입니다.|  
|**qreader_agentname**|**sysname**|지연 업데이트를 지원하는 트랜잭션 게시에 대한 큐 판독기 에이전트 작업의 이름입니다.|  
|**worst_runspeedPerf**|**int**|병합 게시에 대한 가장 긴 동기화 시간입니다.|  
|**best_runspeedPerf**|**int**|병합 게시에 대한 가장 짧은 동기화 시간입니다.|  
|**average_runspeedPerf**|**int**|병합 게시에 대한 평균 동기화 시간입니다.|  
|**retention_period_unit**|**int**|*보존*을 표현 하는 데 사용 되는 단위입니다.|  
|**발행자**|**sysname**|게시를 수행 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_replmonitorhelppublication** 은 모든 유형의 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 배포 데이터베이스에서 **db_owner** 또는 **replmonitor** 고정 데이터베이스 역할의 멤버만 **sp_replmonitorhelppublication**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [프로그래밍 방식으로 복제 모니터링](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
