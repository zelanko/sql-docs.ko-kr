---
title: sp_replmonitorhelpmergesession (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorhelpmergesession_TSQL
- sp_replmonitorhelpmergesession
helpviewer_keywords:
- sp_replmonitorhelpmergesession
ms.assetid: a0400ba8-9609-4901-917e-925e119103a1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 224d304a44c3e66eb8f2c18f4c581bf271f926f9
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58538505"
---
# <a name="spreplmonitorhelpmergesession-transact-sql"></a>sp_replmonitorhelpmergesession(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정된 복제 병합 에이전트의 이전 세션에 대한 정보를 필터링 조건에 일치하는 각 세션당 한 행씩 반환합니다. 병합 복제 모니터링에 사용되는 이 저장 프로시저는 배포 데이터베이스의 배포자 또는 구독 데이터베이스의 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_replmonitorhelpmergesession [ [ @agent_name = ] 'agent_name' ]  
    [ , [ @hours = ] hours ]  
    [ , [ @session_type = ] session_type ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]  
    [ , [ @publication = ] 'publication' ]   
```  
  
## <a name="arguments"></a>인수  
`[ @agent_name = ] 'agent_name'` 에이전트의 이름이입니다. *agent_name* 됩니다 **nvarchar(100)** 기본값은 없습니다.  
  
`[ @hours = ] hours` 기록 에이전트 세션 정보를 반환할 수 있는 시간에서 시간 범위가입니다. *시간* 됩니다 **int**, 다음 범위 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|< **0**|이전에 실행된 에이전트 세션에 대한 정보를 최대 100개까지 반환합니다.|  
|**0** (기본값)|이전에 실행된 모든 에이전트 세션에 대한 정보를 반환합니다.|  
|> **0**|정보를 반환 합니다 에이전트에서 발생 한 실행 지난에서 *시간* 시간입니다.|  
  
`[ @session_type = ] session_type` 세션 종료 결과에 따라 결과 집합을 필터링 합니다. *session_type* 됩니다 **int**, 이며 다음이 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1** (기본값)|다시 시도 또는 성공한 에이전트 세션입니다.|  
|**0**|실패한 에이전트 세션입니다.|  
  
`[ @publisher = ] 'publisher'` 게시자의 이름이입니다. *게시자* 됩니다 **sysname**, 기본값은 NULL입니다. 실행 하는 경우이 매개 변수는 **sp_replmonitorhelpmergesession** 구독자의 합니다.  
  
`[ @publisher_db = ] 'publisher_db'` 게시 데이터베이스의 이름이입니다. *publisher_db* 됩니다 **sysname**, 기본값은 NULL입니다. 실행 하는 경우이 매개 변수는 **sp_replmonitorhelpmergesession** 구독자의 합니다.  
  
`[ @publication = ] 'publication'` 게시의 이름이입니다. *게시* 됩니다 **sysname**, 기본값은 NULL입니다. 실행 하는 경우이 매개 변수는 **sp_replmonitorhelpmergesession** 구독자의 합니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**Session_id**|**int**|에이전트 작업 세션의 ID입니다.|  
|**상태**|**int**|에이전트 실행 상태입니다.<br /><br /> **1** = Start<br /><br /> **2** = 성공<br /><br /> **3** = 진행 중<br /><br /> **4** = 유휴 상태<br /><br /> **5** = Retry<br /><br /> **6** = Fail|  
|**StartTime**|**datetime**|에이전트 작업 세션이 시작된 시간입니다.|  
|**EndTime**|**datetime**|에이전트 작업 세션이 완료된 시간입니다.|  
|**기간**|**int**|해당 작업 세션에 소요된 총 시간(초)입니다.|  
|**UploadedCommands**|**int**|에이전트 세션 중에 업로드된 명령 수입니다.|  
|**DownloadedCommands**|**int**|에이전트 세션 중에 다운로드된 명령 수입니다.|  
|**ErrorMessages**|**int**|에이전트 세션 중에 생성된 오류 메시지 수입니다.|  
|**ErrorID**|**int**|발생한 오류의 ID입니다.|  
|**PercentageDone**|**decimal**|활성 세션에서 이미 전달된 전체 변경 내용의 예상 비율(%)입니다.|  
|**TimeRemaining**|**int**|활성 세션에서 남은 예상 시간(초)입니다.|  
|**CurrentPhase**|**int**|활성 세션의 현재 단계이며 다음 중 하나일 수 있습니다.<br /><br /> **1** = 업로드<br /><br /> **2** = 다운로드|  
|**LastMessage**|**nvarchar(500)**|세션 중에 병합 에이전트에서 기록한 마지막 메시지입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_replmonitorhelpmergesession** 병합 복제를 모니터링 하는 데 사용 됩니다.  
  
 구독자에서 실행 될 때 **sp_replmonitorhelpmergesession** 만 마지막 다섯 개 병합 에이전트 세션에 대 한 정보를 반환 합니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **db_owner** 또는 **replmonitor** 고정된 데이터베이스 역할 또는 구독자의 구독 데이터베이스의 배포자에서 배포 데이터베이스의 실행할 수 있습니다 **sp_ replmonitorhelpmergesession**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [프로그래밍 방식으로 복제 모니터링](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
