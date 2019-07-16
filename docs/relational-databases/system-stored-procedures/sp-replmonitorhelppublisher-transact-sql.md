---
title: sp_replmonitorhelppublisher (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorhelppublisher_TSQL
- sp_replmonitorhelppublisher
helpviewer_keywords:
- sp_replmonitorhelppublisher
ms.assetid: 171501fe-4b74-4647-96c3-7691c777e01b
author: stevestein
ms.author: sstein
ms.openlocfilehash: ba2c2a15efda0ca096d0f3d50acf60407b5dc86a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67950555"
---
# <a name="spreplmonitorhelppublisher-transact-sql"></a>sp_replmonitorhelppublisher(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  배포자와 연결된 하나 이상의 게시에 대한 현재 상태 정보를 반환합니다. 복제 모니터링에 사용되는 이 저장 프로시저는 배포 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_replmonitorhelppublisher [ [ @publisher = ] 'publisher' ]  
    [ , [ @refreshpolicy = ] refreshpolicy ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publisher = ] 'publisher'` 상태를 모니터링 하는 게시자의 이름이입니다. *게시자* 됩니다 **sysname**, 기본값은 NULL입니다. NULL인 경우 배포자를 사용하는 모든 게시자에 대해 정보가 반환됩니다.  
  
`[ @refreshpolicy = ] refreshpolicy` 내부 전용입니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|게시자의 이름입니다.|  
|**distribution_db**|**sysname**|지정된 게시자에서 사용하는 배포 데이터베이스의 이름입니다.|  
|**상태**|**int**|이 게시자의 게시와 연결된 모든 복제 에이전트의 최대 상태로 다음 값 중 하나일 수 있습니다.<br /><br /> **1** = 시작<br /><br /> **2** = 성공<br /><br /> **3** = 진행 중<br /><br /> **4** = 유휴 상태<br /><br /> **5** = 다시 시도 중<br /><br /> **6** = 실패|  
|**warning**|**int**|이 게시자의 게시에 속한 구독에서 생성한 최대 임계값 경고로 다음 값 중 하나 이상을 논리적 OR 연산한 결과일 수 있습니다.<br /><br /> **1** = expiration-보존 기간 임계값 내에 트랜잭션 게시에 구독 동기화 되지 않습니다.<br /><br /> **2** = latency-트랜잭션 게시자에서 구독자로 데이터를 복제 하는 데 걸린 시간 (초)에서의 임계값을 초과 합니다.<br /><br /> **4** = mergeexpiration-보존 기간 임계값 내에 병합 게시에 구독 동기화 되지 않습니다.<br /><br /> **8** = mergefastrunduration-병합 구독을 완전 동기화 하는 데 걸린 시간 (초), 고속 네트워크 연결을 통해, 임계값을 초과 합니다.<br /><br /> **16** = mergeslowrunduration-병합 구독을 완전 동기화 하는 데 걸린 시간 (초), 저속 또는 전화 접속 네트워크 연결을 통해, 임계값을 초과 합니다.<br /><br /> **32** = mergefastrunspeed-의 배달 속도가 임계 속도 초당 행 고속 네트워크 연결을 통해 유지 관리 못했습니다 병합 구독을 동기화 하는 동안 행.<br /><br /> **64** = mergeslowrunspeed-배달 속도 저속 또는 전화 접속 네트워크 연결을 통해 초당 행에서 임계 속도 유지 하기 위해 병합 구독을 동기화 하는 동안 행 실패 했습니다.|  
|**publicationcount**|**int**|게시자에 속한 게시의 수입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_replmonitorhelppublisher** 모든 유형의 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 구성원만 합니다 **sysadmin** 고정된 서버 역할의 멤버나 배포자 합니다 **db_owner** 또는 **replmonitor** 배포 데이터베이스의 고정된 데이터베이스 역할 수 실행할 **sp_replmonitorhelppublisher**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [프로그래밍 방식으로 복제 모니터링](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
