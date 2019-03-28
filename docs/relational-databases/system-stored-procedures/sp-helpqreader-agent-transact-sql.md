---
title: sp_helpqreader_agent (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpqreader_agent_TSQL
- sp_helpqreader_agent
helpviewer_keywords:
- sp_helpqreader_agent
ms.assetid: 8e74e1aa-e95b-4183-8017-bf123439b08d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f40856b20a76abdb7a3788f2564c02fe2e090619
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58529345"
---
# <a name="sphelpqreaderagent-transact-sql"></a>sp_helpqreader_agent(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  큐 판독기 에이전트의 속성을 반환합니다. 이 저장 프로시저는 배포 데이터베이스의 배포자 또는 모든 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpqreader_agent [ [ @frompublisher = ] frompublisher ]  
```  
  
## <a name="arguments"></a>인수  
`[ @frompublisher = ] frompublisher` 저장된 프로시저는 게시자 또는 배포자에서 호출 되는지 여부를 지정 합니다. *frompublisher* 는 bit 이며 기본값은 0입니다. **1** 은 저장된 프로시저가 게시자에서 호출 됨 및 **0** 저장된 프로시저가 배포자에서 호출 되는 것을 의미 합니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|에이전트의 ID입니다.|  
|**name**|**nvarchar(100)**|에이전트의 이름입니다.|  
|**job_id**|**uniqueidentifier**|에이전트 작업의 고유한 ID입니다.|  
|**job_login**|**nvarchar(512)**|배포 에이전트를 실행 하는 형식으로 반환 되는 Windows 계정입니다 *도메인*\\*username*합니다.|  
|**job_password**|**sysname**|값이 보안상의 이유로 **\* \* \* \* \* \* \* \* \* \*** 항상 반환 됩니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_helpqreader_agent** 트랜잭션 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 때 값 *frompublisher* 는 **1**의 구성원만 합니다 **sysadmin** 고정된 서버 역할의 멤버나 게시자는 **db_owner**게시 데이터베이스의 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_helpqreader_agent**합니다. 이 고, 그렇지의 멤버만 합니다 **sysadmin** 고정된 서버 역할의 멤버나 배포자 합니다 **db_owner** 고정된 데이터베이스 역할의 배포 데이터베이스를 실행할 수 있습니다 **sp_helpqreader_ 에이전트**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [트랜잭션 게시에 대해 업데이트할 수 있는 구독 설정](../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)  
  
  
