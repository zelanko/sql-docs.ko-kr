---
description: sp_replmonitorhelppublisher(Transact-SQL)
title: sp_replmonitorhelppublisher (Transact-sql) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a2a37168d22bd931faa6f8033c847620b9606b11
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473875"
---
# <a name="sp_replmonitorhelppublisher-transact-sql"></a>sp_replmonitorhelppublisher(Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  배포자와 연결된 하나 이상의 게시에 대한 현재 상태 정보를 반환합니다. 복제 모니터링에 사용되는 이 저장 프로시저는 배포 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_replmonitorhelppublisher [ [ @publisher = ] 'publisher' ]  
    [ , [ @refreshpolicy = ] refreshpolicy ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publisher = ] 'publisher'` 상태를 모니터링 하는 게시자의 이름입니다. *publisher* 는 **sysname**이며 기본값은 NULL입니다. NULL인 경우 배포자를 사용하는 모든 게시자에 대해 정보가 반환됩니다.  
  
`[ @refreshpolicy = ] refreshpolicy` 내부용 으로만 사용 됩니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**발행자**|**sysname**|게시자의 이름입니다.|  
|**distribution_db**|**sysname**|지정된 게시자에서 사용하는 배포 데이터베이스의 이름입니다.|  
|**status**|**int**|이 게시자의 게시와 연결된 모든 복제 에이전트의 최대 상태로 다음 값 중 하나일 수 있습니다.<br /><br /> **1** = 시작 됨<br /><br /> **2** = 성공<br /><br /> **3** = 진행 중<br /><br /> **4** = 유휴 상태<br /><br /> **5** = 다시 시도 중<br /><br /> **6** = 실패|  
|**warning**|**int**|이 게시자의 게시에 속한 구독에서 생성한 최대 임계값 경고로 다음 값 중 하나 이상을 논리적 OR 연산한 결과일 수 있습니다.<br /><br /> **1** = 만료-트랜잭션 게시에 대 한 구독이 보존 기간 임계값 내에서 동기화 되지 않았습니다.<br /><br /> **2** = latency-트랜잭션 게시자에서 구독자로 데이터를 복제 하는 데 소요 된 시간이 임계값 (초)을 초과 합니다.<br /><br /> **4** = mergeexpiration-병합 게시에 대 한 구독이 보존 기간 임계값 내에서 동기화 되지 않았습니다.<br /><br /> **8** = mergefastrunduration-고속 네트워크 연결을 통해 병합 구독의 동기화를 완료 하는 데 소요 된 시간이 임계값 (초)을 초과 합니다.<br /><br /> **16** = mergeslowrunduration-저속 또는 전화 접속 네트워크 연결을 통해 병합 구독의 동기화를 완료 하는 데 소요 된 시간이 임계값 (초)을 초과 합니다.<br /><br /> **32** = mergefastrunspeed-고속 네트워크 연결을 통해 병합 구독을 동기화 하는 동안 행의 배달 속도가 임계값 속도 (초당 행 수)를 유지 하지 못했습니다.<br /><br /> **64** = mergeslowrunspeed-저속 또는 전화 접속 네트워크 연결을 통해 병합 구독을 동기화 하는 동안 행의 배달 속도가 임계값 속도 (초당 행 수)를 유지 하지 못했습니다.|  
|**publicationcount**|**int**|게시자에 속한 게시의 수입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_replmonitorhelppublisher** 은 모든 유형의 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 배포자에서 **sysadmin** 고정 서버 역할의 멤버 또는 배포 데이터베이스의 **db_owner** 또는 **replmonitor** 고정 데이터베이스 역할의 멤버만 **sp_replmonitorhelppublisher**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [프로그래밍 방식으로 복제 모니터링](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
