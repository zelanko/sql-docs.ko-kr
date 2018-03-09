---
title: sp_helpqreader_agent (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_helpqreader_agent_TSQL
- sp_helpqreader_agent
helpviewer_keywords:
- sp_helpqreader_agent
ms.assetid: 8e74e1aa-e95b-4183-8017-bf123439b08d
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 50492a76e742459e7b883f9887026d0ce63d1eb1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
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
 [  **@frompublisher=** ] *frompublisher*  
 저장 프로시저가 게시자에서 호출되는지 또는 배포자에서 호출되는지 여부를 지정합니다. *frompublisher* 는 bit 이며 기본값은 0입니다. **1** 저장된 프로시저가 게시자에서 호출 될 것을 의미 하 고 **0** 저장된 프로시저가 배포자에서 호출 될 것을 의미 합니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**id**|**int**|에이전트의 ID입니다.|  
|**name**|**nvarchar (100)**|에이전트의 이름입니다.|  
|**job_id**|**uniqueidentifier**|에이전트 작업의 고유한 ID입니다.|  
|**job_login**|**nvarchar(512)**|배포 에이전트가 실행 되는, 형식으로 반환 되는 Windows 계정이 며 *도메인*\\*username*합니다.|  
|**job_password**|**sysname**|보안상의 이유로 값  **\* \* \* \* \* \* \* \* \* \***  는 항상 반환 됩니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_helpqreader_agent** 트랜잭션 복제에 사용 됩니다.  
  
## <a name="permissions"></a>Permissions  
 때의 값 *frompublisher* 은 **1**의 구성원만는 **sysadmin** 고정된 서버 역할의 멤버나 게시자는 **db_owner**게시 데이터베이스의 고정된 데이터베이스 역할을 실행할 수 있는 **sp_helpqreader_agent**합니다. 그렇지 않은 경우의 구성원만는 **sysadmin** 고정된 서버 역할의 멤버나 배포자는 **db_owner** 배포 데이터베이스의 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_helpqreader_ 에이전트**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [트랜잭션 게시에 대해 업데이트할 수 있는 구독 설정](../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)  
  
  
