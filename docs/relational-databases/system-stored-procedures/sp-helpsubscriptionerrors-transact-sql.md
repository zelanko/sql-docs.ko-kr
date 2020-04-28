---
title: sp_helpsubscriptionerrors (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpsubscriptionerrors_TSQL
- sp_helpsubscriptionerrors
helpviewer_keywords:
- sp_helpsubscriptionerrors
ms.assetid: 01c8bc21-939e-490d-8cc8-219c068be31e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2fe01c857d8a9e27de56538d0e595f3ad89f4d96
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68771518"
---
# <a name="sp_helpsubscriptionerrors-transact-sql"></a>sp_helpsubscriptionerrors(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  지정된 구독에 대한 모든 트랜잭션 복제 오류를 반환합니다. 이 저장 프로시저는 배포 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpsubscriptionerrors [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'   
        , [ @publication = ] 'publication'   
        , [ @subscriber = ] 'subscriber'   
        , [ @subscriber_db = ] 'subscriber_db'  
```  
  
## <a name="arguments"></a>인수  
`[ @publisher = ] 'publisher'`게시자의 이름입니다. *publisher* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publisher_db = ] 'publisher_db'`게시 데이터베이스의 이름입니다. *publisher_db* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publication = ] 'publication'`게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @subscriber = ] 'subscriber'`구독자의 이름입니다. *구독자* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @subscriber_db = ] 'subscriber_db'`구독 데이터베이스의 이름입니다. *subscriber_db* 는 **sysname**이며 기본값은 없습니다.  
  
## <a name="result-set"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|오류 ID입니다.|  
|**time**|**datetime**|오류가 발생한 시간입니다.|  
|**error_type_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**source_type_id**|**int**|오류 원본 유형 ID입니다.|  
|**source_name**|**nvarchar (100)**|오류 원본의 이름입니다.|  
|**error_code**|**sysname**|오류 코드|  
|**error_text**|**ntext**|오류 메시지입니다.|  
|**xact_seqno**|**varbinary(16)**|실패한 실행 일괄 처리의 시작 트랜잭션 로그 시퀀스 번호입니다. 배포 에이전트에 의해서만 사용되며 실패한 실행 일괄 처리에 있는 첫 번째 트랜잭션의 트랜잭션 로그 시퀀스 번호입니다.|  
|**command_id**|**int**|실패한 실행 일괄 처리의 명령 ID입니다. 배포 에이전트에 의해서만 사용되며 실패한 실행 일괄 처리에 있는 첫 번째 명령의 명령 ID입니다.|  
|**session_id**|**int**|오류가 발생한 에이전트 세션의 ID입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_helpsubscriptionerrors** 는 스냅숏 및 트랜잭션 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_helpsubscriptionerrors**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_helpsubscription &#40;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)   
 [sp_helpsubscription_properties&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
