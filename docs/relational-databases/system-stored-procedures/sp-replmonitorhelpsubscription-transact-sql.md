---
title: sp_replmonitorhelpsubscription (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_replmonitorhelpsubscription_TSQL
- sp_replmonitorhelpsubscription
helpviewer_keywords: sp_replmonitorhelpsubscription
ms.assetid: a681b2db-c82d-4624-a10c-396afb0ac42f
caps.latest.revision: "32"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 24254591967a08df8a46446e485af1be5760c862
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="spreplmonitorhelpsubscription-transact-sql"></a>sp_replmonitorhelpsubscription(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  게시자에 있는 하나 이상의 게시에 속한 구독의 현재 상태 정보를 반환하고 반환된 각 구독당 한 개의 행을 반환합니다. 복제 모니터링에 사용되는 이 저장 프로시저는 배포 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_replmonitorhelpsubscription [ @publisher = ] 'publisher'  
    [ , [ @publisher_db = ] 'publisher_db' ]  
    [ , [ @publication = ] 'publication' ]  
    [ , [ @publication_type = ] publication_type ]   
    [ , [ @mode = ] mode ]  
    [ , [ @topnum = ] topnum ]   
    [ , [ @exclude_anonymous = ] exclude_anonymous ]   
    [ , [ @refreshpolicy = ] refreshpolicy ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@publisher**  =] **'***게시자***'**  
 상태를 모니터링할 게시자의 이름입니다. *게시자* 은 **sysname**, 기본값은 NULL입니다. 경우 **null**, 배포자를 사용 하는 모든 게시자에 대 한 정보가 반환 됩니다.  
  
 [  **@publisher_db**  =] **'***publisher_db***'**  
 게시된 데이터베이스의 이름입니다. *publisher_db* 은 **sysname**, 기본값은 NULL입니다. NULL인 경우 게시자에 게시된 모든 데이터베이스에 대한 정보가 반환됩니다.  
  
 [  **@publication**  =] **'***게시***'**  
 모니터링할 게시의 이름입니다. *게시* 은 **sysname**, 기본값은 NULL입니다.  
  
 [  **@publication_type**  =] *publication_type*  
 게시의 유형입니다. *publication_type* 은 **int**, 다음이 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**0**|트랜잭션 게시|  
|**1**|스냅숏 게시|  
|**2**|병합 게시|  
|NULL(기본값)|복제에서 게시 유형을 확인하려고 합니다.|  
  
 [  **@mode**  =] *모드*  
 구독 모니터링 정보를 반환할 때 사용하는 필터링 모드입니다. *모드* 은 **int**, 다음이 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**0** (기본값)|모든 구독을 반환합니다.|  
|**1**|오류가 있는 구독만 반환합니다.|  
|**2**|생성된 임계값 메트릭 경고가 있는 구독만 반환합니다.|  
|**3**|오류 또는 생성된 임계값 메트릭 경고가 있는 구독만 반환합니다.|  
|**4**|상위 25 개 실적이 최악 구독을 반환합니다.|  
|**5**|성능이 가장 낮은 50개의 구독을 반환합니다.|  
|**6**|현재 동기화 중인 구독만 반환합니다.|  
|**7**|현재 동기화 중이 아닌 구독만 반환합니다.|  
  
 [  **@topnum**  =] *topnum*  
 반환된 데이터의 가장 위에서부터 지정한 수의 구독으로 결과 집합을 제한합니다. *topnum* 은 **int**, 기본값은 없습니다.  
  
 [  **@exclude_anonymous**  =] *exclude_anonymous*  
 결과 집합에서 익명 끌어오기 구독을 제외할지 여부입니다. *exclude_anonymous* 은 **비트**, 기본값은 **0**; 값을 **1** 의미 익명 구독이 제외 되 고 값이  **0** 포함 되는 것을 의미 합니다.  
  
 [  **@refreshpolicy=** ] *refreshpolicy*  
 내부적으로만 사용됩니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**상태**|**int**|게시와 연결된 모든 복제 에이전트의 상태를 검사하고 다음 순서로 발견된 가장 높은 상태를 반환합니다.<br /><br /> **6** = 실패<br /><br /> **5** = 다시 시도 중<br /><br /> **2** = 중지<br /><br /> **4** = 유휴 상태<br /><br /> **3** = 진행 중<br /><br /> **1** = 시작|  
|**경고**|**int**|게시에 속한 구독에서 생성한 최대 임계값 경고로 다음 값 중 하나 이상의 논리 OR 결과일 수 있습니다.<br /><br /> **1** = expiration-트랜잭션 게시에 구독이 보존 기간 임계값 내에서 동기화 되지 않습니다.<br /><br /> **2** = latency-트랜잭션 게시자에서 구독자로 데이터를 복제 하는 데 걸린 시간 (초)가 임계값을 초과 합니다.<br /><br /> **4** = mergeexpiration-병합 게시에 구독이 보존 기간 임계값 내에서 동기화 되지 않습니다.<br /><br /> **8** = mergefastrunduration-병합 구독을 완전 동기화 하는 데 걸린 시간 (초)을 고속 네트워크 연결을 통해 임계값을 초과 합니다.<br /><br /> **16** = mergeslowrunduration-병합 구독을 완전 동기화 하는 데 걸린 시간 (초)을 저속 또는 전화 접속 네트워크 연결을 통해 임계값을 초과 합니다.<br /><br /> **32** =의 배달 속도가 mergefastrunspeed-고속 네트워크 연결을 통해 임계 속도, 초당 행 수를 유지 하지 못했습니다 병합 구독을 동기화 하는 동안 행에 대 한 합니다.<br /><br /> **64** = mergeslowrunspeed-의 배달 속도가 저속 또는 전화 접속 네트워크 연결을 통해 임계 속도, 초당 행 수를 유지 하지 못했습니다 병합 구독을 동기화 하는 동안 행에 대 한 합니다.|  
|**subscriber**|**sysname**|구독자의 이름입니다.|  
|**subscriber_db**|**sysname**|구독에 사용되는 데이터베이스의 이름입니다.|  
|**publisher_db**|**sysname**|게시 데이터베이스의 이름입니다.|  
|**게시**|**sysname**|게시의 이름입니다.|  
|**publication_type**|**int**|게시 유형이며 다음 값 중 하나일 수 있습니다.<br /><br /> **0** = 트랜잭션 게시<br /><br /> **1** = 스냅숏 게시<br /><br /> **2** = 병합 게시|  
|**하위 유형**|**int**|구독 유형이며 다음 값 중 하나일 수 있습니다.<br /><br /> **0** = 밀어넣기<br /><br /> **1** = 끌어오기<br /><br /> **2** = 익명|  
|**대기 시간**|**int**|트랜잭션 게시에 대해 로그 판독기 또는 배포 에이전트가 전파하는 데이터 변경에 대한 최대 대기 시간(초)입니다.|  
|**latencythreshold**|**int**|경고 발생의 기준이 되는 트랜잭션 게시에 대한 최대 대기 시간입니다.|  
|**agentnotrunning**|**int**|에이전트가 실행되지 않은 시간(시간)입니다.|  
|**agentnotrunningthreshold**|**int**|경고가 발생하기 전까지 에이전트가 실행되지 않은 시간(시간)입니다.|  
|**timetoexpiration**|**int**|구독이 동기화되지 않은 경우 만료되기 전까지의 시간(시간)입니다.|  
|**expirationthreshold**|**int**|경고가 발생한 구독이 만료되기 전까지의 시간(시간)입니다.|  
|**last_distsync**|**datetime**|배포 에이전트가 마지막으로 실행된 날짜/시간입니다.|  
|**distribution_agentname**|**sysname**|트랜잭션 게시 구독에 대한 배포 에이전트 작업의 이름입니다.|  
|**mergeagentname**|**sysname**|병합 게시 구독에 대한 병합 에이전트 작업의 이름입니다.|  
|**mergesubscriptionfriendlyname**|**sysname**|구독에 지정된 이름입니다.|  
|**mergeagentlocation**|**sysname**|병합 에이전트가 실행되는 서버의 이름입니다.|  
|**mergeconnectiontype**|**int**|구독과 병합 게시를 동기화할 때 사용하는 연결이며 다음 값 중 하나일 수 있습니다.<br /><br /> **1** = 로컬 영역 네트워크 (LAN)<br /><br /> **2** = 전화 접속 네트워크 연결<br /><br /> **3** = 웹 동기화 합니다.|  
|**mergePerformance**|**int**|구독에 대한 모든 동기화 성능과 비교한 최근 동기화의 성능입니다. 최근 동기화의 배달 속도를 이전의 모든 배달 속도 평균으로 나눈 값을 기반으로 합니다.|  
|**mergerunspeed**|**float**|구독에 대한 최근 동기화의 배달 속도입니다.|  
|**mergerunduration**|**int**|구독의 최근 동기화를 완료하는 데 걸린 시간입니다.|  
|**monitorranking**|**int**|결과 집합에서 구독을 정렬하는 데 사용하는 순위 값이며 다음 값 중 하나일 수 있습니다.<br /><br /> 트랜잭션 게시인 경우<br /><br /> **60** = 오류<br /><br /> **56** = 경고: 성능 심각<br /><br /> **52** = 경고: 곧 만료 됨 또는 만료<br /><br /> **50** = 경고: 구독이 초기화 되지 않음<br /><br /> **40** 명령 다시 시도 중 실패 =<br /><br /> **30** (성공) 실행 되 고 있지 =<br /><br /> **20** = 실행 중 (시작, 실행 중 또는 유휴 상태)<br /><br /> 병합 게시인 경우<br /><br /> **60** = 오류<br /><br /> **56** = 경고: 성능 심각<br /><br /> **54** = 경고: 장기 실행 트랜잭션 병합<br /><br /> **52** = 경고: 곧 만료 됨<br /><br /> **50** = 경고: 구독이 초기화 되지 않음<br /><br /> **40** 명령 다시 시도 중 실패 =<br /><br /> **30** = 실행 중 (시작, 실행 중 또는 유휴 상태)<br /><br /> **20** (성공) 실행 되 고 있지 =|  
|**distributionagentjobid**|**binary (16)**|트랜잭션 게시 구독에 대한 배포 에이전트 작업의 ID입니다.|  
|**mergeagentjobid**|**binary (16)**|병합 게시 구독에 대한 병합 에이전트 작업의 ID입니다.|  
|**distributionagentid**|**int**|구독에 대한 배포 에이전트 작업의 ID입니다.|  
|**distributionagentprofileid**|**int**|배포 에이전트에서 사용하는 에이전트 프로필의 ID입니다.|  
|**mergeagentid**|**int**|구독에 대한 병합 에이전트 작업의 ID입니다.|  
|**mergeagentprofileid**|**int**|병합 에이전트에서 사용하는 에이전트 프로필의 ID입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_replmonitorhelpsubscription** 모든 유형의 복제와 함께 사용 됩니다.  
  
 **sp_replmonitorhelpsubscription** 결과 집합의 값에 의해 결정 되는 구독 상태의 심각도에 따라 정렬 *monitorranking*합니다. 예를 들어 오류 상태에 있는 모든 구독에 대한 행은 경고 상태에 있는 구독에 대한 행보다 위에 정렬됩니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **db_owner** 또는 **replmonitor** 배포 데이터베이스의 고정된 데이터베이스 역할을 실행할 수 있는 **sp_replmonitorhelpsubscription**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [프로그래밍 방식으로 복제 모니터링](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
