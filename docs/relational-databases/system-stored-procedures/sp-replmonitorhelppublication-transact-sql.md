---
title: sp_replmonitorhelppublication (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
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
- sp_replmonitorhelppublication_TSQL
- sp_replmonitorhelppublication
helpviewer_keywords:
- sp_replmonitorhelppublication
ms.assetid: 7928c50c-617f-41c5-9e0f-4e42e8be55dc
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 1067d01bf7b4d510e81ac85f3e88b121b0f645e9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33002800"
---
# <a name="spreplmonitorhelppublication-transact-sql"></a>sp_replmonitorhelppublication(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  게시자에 있는 하나 이상의 게시에 대한 현재 상태 정보를 반환합니다. 복제 모니터링에 사용되는 이 저장 프로시저는 배포 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_replmonitorhelppublication [ @publisher = ] 'publisher'  
    [ , [ @publisher_db = ] 'publisher_db'   
    [ , [ @publication = ] 'publication'   
    [ , [ @publication_type = ] publication_type ]   
    [ , [ @refreshpolicy = ] refreshpolicy ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@publisher** = ] **'***publisher***'**  
 상태를 모니터링할 게시자의 이름입니다. *게시자* 은 **sysname**, 기본값은 NULL입니다. 경우 **null**, 배포자를 사용 하는 모든 게시자에 대 한 정보가 반환 됩니다.  
  
 [ **@publisher_db** = ] **'***publisher_db***'**  
 게시된 데이터베이스의 이름입니다. *publisher_db* 은 **sysname**, 기본값은 NULL입니다. NULL인 경우 게시자에 게시된 모든 데이터베이스에 대한 정보가 반환됩니다.  
  
 [ **@publication** =] **'***게시***'**  
 모니터링할 게시의 이름입니다. *게시* 은 **sysname**, 기본값은 NULL입니다.  
  
 [ **@publication_type** =] *publication_type*  
 게시의 유형입니다. *publication_type* 은 **int**, 다음이 값 중 하나일 수 있습니다.  
  
|Value|설명|  
|-----------|-----------------|  
|**0**|트랜잭션 게시|  
|**1**|스냅숏 게시|  
|**2**|병합 게시|  
|NULL(기본값)|복제에서 게시 유형을 확인하려고 합니다.|  
  
 [  **@refreshpolicy=** ] *refreshpolicy*  
 내부적으로만 사용됩니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**publisher_db**|**sysname**|게시자의 이름입니다.|  
|**게시**|**sysname**|게시의 이름입니다.|  
|**publication_type**|**int**|게시 유형이며 다음 값 중 하나일 수 있습니다.<br /><br /> **0** = 트랜잭션 게시<br /><br /> **1** = 스냅숏 게시<br /><br /> **2** = 병합 게시|  
|**상태**|**int**|게시와 연관된 모든 복제 에이전트의 최대 상태로 다음 값 중 하나일 수 있습니다.<br /><br /> **1** = 시작<br /><br /> **2** = 성공<br /><br /> **3** = 진행 중<br /><br /> **4** = 유휴 상태<br /><br /> **5** = 다시 시도 중<br /><br /> **6** = 실패|  
|**경고**|**int**|게시에 속한 구독에서 생성한 최대 임계값 경고로 다음 값 중 하나 이상의 논리 OR 결과일 수 있습니다.<br /><br /> **1** = expiration-트랜잭션 게시에 구독이 보존 기간 임계값 내에서 동기화 되지 않습니다.<br /><br /> **2** = latency-트랜잭션 게시자에서 구독자로 데이터를 복제 하는 데 걸린 시간 (초)가 임계값을 초과 합니다.<br /><br /> **4** = mergeexpiration-병합 게시에 구독이 보존 기간 임계값 내에서 동기화 되지 않습니다.<br /><br /> **8** = mergefastrunduration-병합 구독을 완전 동기화 하는 데 걸린 시간 (초)을 고속 네트워크 연결을 통해 임계값을 초과 합니다.<br /><br /> **16** = mergeslowrunduration-병합 구독을 완전 동기화 하는 데 걸린 시간 (초)을 저속 또는 전화 접속 네트워크 연결을 통해 임계값을 초과 합니다.<br /><br /> **32** =의 배달 속도가 mergefastrunspeed-고속 네트워크 연결을 통해 임계 속도, 초당 행 수를 유지 하지 못했습니다 병합 구독을 동기화 하는 동안 행에 대 한 합니다.<br /><br /> **64** = mergeslowrunspeed-의 배달 속도가 저속 또는 전화 접속 네트워크 연결을 통해 임계 속도, 초당 행 수를 유지 하지 못했습니다 병합 구독을 동기화 하는 동안 행에 대 한 합니다.|  
|**worst_latency**|**int**|트랜잭션 게시에 대해 로그 판독기 또는 배포 에이전트가 전파하는 데이터 변경에 대한 최대 대기 시간(초)입니다.|  
|**best_latency**|**int**|트랜잭션 게시에 대해 로그 판독기 또는 배포 에이전트가 전파하는 데이터 변경에 대한 최소 대기 시간(초)입니다.|  
|**average_latency**|**int**|트랜잭션 게시에 대해 로그 판독기 또는 배포 에이전트가 전파하는 데이터 변경에 대한 평균 대기 시간(초)입니다.|  
|**last_distsync**|**datetime**|배포 에이전트를 실행한 마지막 날짜/시간입니다.|  
|**retention**|**int**|게시의 보존 기간입니다.|  
|**latencythreshold**|**int**|트랜잭션 게시에 대해 설정된 대기 시간 임계값입니다.|  
|**expirationthreshold**|**int**|병합 게시인 경우 게시에 대해 설정된 만료 임계값입니다.|  
|**agentnotrunningthreshold**|**int**|에이전트를 실행하지 않을 가장 긴 시간에 대해 설정된 임계값입니다.|  
|**subscriptioncount**|**int**|게시에 대한 구독 수입니다.|  
|**runningdistagentcount**|**int**|게시에 대해 실행되는 배포 에이전트 수입니다.|  
|**snapshot_agentname**|**sysname**|게시에 대한 스냅숏 에이전트 작업의 이름입니다.|  
|**logreader_agentname**|**sysname**|트랜잭션 게시에 대한 로그 판독기 에이전트 작업의 이름입니다.|  
|**qreader_agentname**|**sysname**|지연 업데이트를 지원하는 트랜잭션 게시에 대한 큐 판독기 에이전트 작업의 이름입니다.|  
|**worst_runspeedPerf**|**int**|병합 게시에 대한 가장 긴 동기화 시간입니다.|  
|**best_runspeedPerf**|**int**|병합 게시에 대한 가장 짧은 동기화 시간입니다.|  
|**average_runspeedPerf**|**int**|병합 게시에 대한 평균 동기화 시간입니다.|  
|**retention_period_unit**|**int**|나타내는 데 사용 되는 단위는 *보존*합니다.|  
|**publisher**|**sysname**|게시를 수행 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_replmonitorhelppublication** 모든 유형의 복제와 함께 사용 됩니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **db_owner** 또는 **replmonitor** 배포 데이터베이스의 고정된 데이터베이스 역할을 실행할 수 있는 **sp_replmonitorhelppublication**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [프로그래밍 방식으로 복제 모니터링](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
