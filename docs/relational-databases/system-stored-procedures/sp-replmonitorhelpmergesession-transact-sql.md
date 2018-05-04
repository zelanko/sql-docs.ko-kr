---
title: sp_replmonitorhelpmergesession (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
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
- sp_replmonitorhelpmergesession_TSQL
- sp_replmonitorhelpmergesession
helpviewer_keywords:
- sp_replmonitorhelpmergesession
ms.assetid: a0400ba8-9609-4901-917e-925e119103a1
caps.latest.revision: 25
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: d1d59aba126e66d523e23c680c55f679cbbfa6ee
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
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
 [ **@agent_name** =] **'***agent_name***'**  
 에이전트의 이름입니다. *agent_name* 은 **nvarchar (100)** 이며 기본값은 없습니다.  
  
 [ **@hours** =] *시간*  
 기록 에이전트 세션 정보를 반환할 시간 범위(시간)입니다. *시간* 은 **int**, 다음 범위 중 하나일 수 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|< **0**|이전에 실행된 에이전트 세션에 대한 정보를 최대 100개까지 반환합니다.|  
|**0** (기본값)|이전에 실행된 모든 에이전트 세션에 대한 정보를 반환합니다.|  
|> **0**|에 정보를 반환 에이전트에서 발생 한 실행 마지막 *시간* 시간 수입니다.|  
  
 [ **@session_type** =] *session_type*  
 세션 종료 결과를 기준으로 결과 집합을 필터링합니다. *session_type* 은 **int**, 다음이 값 중 하나일 수 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**1** (기본값)|다시 시도 또는 성공한 에이전트 세션입니다.|  
|**0**|실패한 에이전트 세션입니다.|  
  
 [ **@publisher** = ] **'***publisher***'**  
 게시자의 이름입니다. *게시자* 은 **sysname**, 기본값은 NULL입니다. 실행할 때이 매개 변수는 **sp_replmonitorhelpmergesession** 구독자에 있습니다.  
  
 [ **@publisher_db** = ] **'***publisher_db***'**  
 게시 데이터베이스의 이름입니다. *publisher_db* 은 **sysname**, 기본값은 NULL입니다. 실행할 때이 매개 변수는 **sp_replmonitorhelpmergesession** 구독자에 있습니다.  
  
 [  **@publication=** ] **'***게시***'**  
 게시의 이름입니다. *게시* 은 **sysname**, 기본값은 NULL입니다. 실행할 때이 매개 변수는 **sp_replmonitorhelpmergesession** 구독자에 있습니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**세션 id**|**int**|에이전트 작업 세션의 ID입니다.|  
|**상태**|**int**|에이전트 실행 상태입니다.<br /><br /> **1** = 시작<br /><br /> **2** = 성공<br /><br /> **3** = 진행 중<br /><br /> **4** = 유휴 상태<br /><br /> **5** = 다시 시도<br /><br /> **6** = 실패|  
|**StartTime**|**datetime**|에이전트 작업 세션이 시작된 시간입니다.|  
|**EndTime**|**datetime**|에이전트 작업 세션이 완료된 시간입니다.|  
|**기간**|**int**|해당 작업 세션에 소요된 총 시간(초)입니다.|  
|**UploadedCommands**|**int**|에이전트 세션 중에 업로드된 명령 수입니다.|  
|**DownloadedCommands**|**int**|에이전트 세션 중에 다운로드된 명령 수입니다.|  
|**ErrorMessages**|**int**|에이전트 세션 중에 생성된 오류 메시지 수입니다.|  
|**오류 Id**|**int**|발생한 오류의 ID입니다.|  
|**PercentageDone**|**decimal**|활성 세션에서 이미 전달된 전체 변경 내용의 예상 비율(%)입니다.|  
|**TimeRemaining**|**int**|활성 세션에서 남은 예상 시간(초)입니다.|  
|**CurrentPhase**|**int**|활성 세션의 현재 단계이며 다음 중 하나일 수 있습니다.<br /><br /> **1** = 업로드<br /><br /> **2** = 다운로드|  
|**LastMessage**|**nvarchar(500)**|세션 중에 병합 에이전트에서 기록한 마지막 메시지입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_replmonitorhelpmergesession** 병합 복제를 모니터링 하는 데 사용 됩니다.  
  
 구독자에서 실행 될 때 **sp_replmonitorhelpmergesession** 마지막 다섯 개 병합 에이전트 세션에 정보만 반환 합니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **db_owner** 또는 **replmonitor** 고정된 데이터베이스 역할 또는 구독자에서 구독 데이터베이스 배포자에서 배포 데이터베이스에서 실행할 수 있습니다 **sp_ replmonitorhelpmergesession**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [프로그래밍 방식으로 복제 모니터링](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
