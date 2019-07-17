---
title: sp_changeqreader_agent (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changeqreader_agent_TSQL
- sp_changeqreader_agent
helpviewer_keywords:
- sp_changeqreader_agent
ms.assetid: d3fe79c5-31ef-4565-bf38-b476b5fb16f7
author: stevestein
ms.author: sstein
ms.openlocfilehash: b636eb929d74aec7b0f3555ce511372f6592c5b0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68099145"
---
# <a name="spchangeqreaderagent-transact-sql"></a>sp_changeqreader_agent(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  큐 판독기 에이전트의 보안 속성을 변경합니다. 이 저장 프로시저는 배포 데이터베이스의 배포자 또는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_changeqreader_agent [ [ @job_login = ] 'job_login' ]  
    [ , [ @job_password = ] 'job_password' ]  
    [ , [ @frompublisher = ] frompublisher   
```  
  
## <a name="arguments"></a>인수  
`[ @job_login = ] 'job_login'` 에 대 한 로그인을 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 에이전트가 실행 되는 Windows 계정입니다. *job_login* 됩니다 **nvarchar(257)** , 기본값은 NULL입니다.  
  
`[ @job_password = ] 'job_password'` 에이전트가 실행 되는 Windows 계정의 암호가입니다. *job_password* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
`[ @frompublisher = ] frompublisher` 프로시저를 실행 하는 경우 게시자입니다. *frompublisher* 는 bit 이며 기본값은 **0**합니다. 값이 **1** 프로시저가 게시 데이터베이스의 게시자에서 실행 될 것임을 의미 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_changeqreader_agent** 트랜잭션 복제에 사용 됩니다.  
  
 **sp_changeqreader_agent** 큐 판독기 에이전트가 실행 되는 Windows 계정을 변경 하는 데 사용 됩니다. 기존 Windows 로그인의 암호를 변경하거나 새 Windows 로그인과 암호를 제공할 수 있습니다.  
  
 에이전트 로그인 또는 암호를 변경한 후 에이전트를 중지하고 다시 시작해야 변경 내용이 적용됩니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할을 실행할 수 있습니다 **sp_changeqreader_agent**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [복제 보안 설정 보기 및 수정](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [sp_addqreader_agent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md)  
  
  
