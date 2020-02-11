---
title: sp_MSchange_merge_agent_properties (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_MSchange_merge_agent_properties_TSQL
- sp_MSchange_merge_agent_properties
helpviewer_keywords:
- sp_MSchange_merge_agent_properties
ms.assetid: f775fa0f-28c7-4863-89ce-7bcfa1ab8b5e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 84c517fe891052ff6e12ee6e92a2d16d912a140b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67905190"
---
# <a name="sp_mschange_merge_agent_properties-transact-sql"></a>sp_MSchange_merge_agent_properties(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전의 배포자에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 실행 되는 병합 에이전트 작업의 속성을 변경 합니다. 이 저장 프로시저는 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 인스턴스에서 게시자가 실행될 때 속성을 변경하는 데 사용됩니다. 이 저장 프로시저는 배포 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_MSchange_merge_agent_properties [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
        , [ @subscriber = ] 'subscriber'   
        , [ @subscriber_db = ] 'subscriber_db'   
        , [ @property = ] 'property'   
        , [ @value = ] 'value' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publisher = ] 'publisher'`게시자의 이름입니다. *publisher* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publisher_db = ] 'publisher_db'`게시 데이터베이스의 이름입니다. *publisher_db* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publication = ] 'publication'`게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @subscriber = ] 'subscriber'`구독자의 이름입니다. *구독자* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @subscriber_db = ] 'subscriber_db'`구독 데이터베이스의 이름입니다. *subscriber_db* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @property = ] 'property'`변경할 게시 속성입니다. *속성* 은 **sysname**이며 기본값은 없습니다.  
  
`[ @value = ] 'value'`새 속성 값입니다. *value* 는 **nvarchar (524)** 이며 기본값은 NULL입니다.  
  
 이 테이블에서는 변경할 수 있는 병합 에이전트 작업의 속성 및 해당 속성 값의 제한에 대해 설명합니다.  
  
|속성|값|Description|  
|--------------|-----------|-----------------|  
|**한**||구독에 대한 간단한 설명입니다.|  
|**merge_job_login**||에이전트가 실행되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 계정의 로그인입니다.|  
|**merge_job_password**||에이전트 작업 실행에 사용된 Windows 계정의 암호입니다.|  
|**publisher_login**||구독을 동기화하기 위해 게시자에 연결할 때 사용되는 로그인입니다.|  
|**publisher_password**||게시자 암호입니다.<br /><br /> [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]|  
|**publisher_security_mode**|**1**|Windows 인증<br /><br /> [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]|  
||**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인증은.|  
|**subscriber_login**||구독을 동기화하기 위해 구독자에 연결할 때 사용하는 로그인입니다.|  
|**subscriber_password**||구독자 암호입니다.<br /><br /> [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]|  
|**subscriber_security_mode**|**1**|Windows 인증<br /><br /> [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]|  
||**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인증은.|  
  
> [!NOTE]  
>  에이전트 로그인 또는 암호를 변경한 후 에이전트를 중지하고 다시 시작해야 변경 내용이 적용됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_MSchange_merge_agent_properties** 는 병합 복제에 사용 됩니다.  
  
 게시자가 이상 버전의 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 인스턴스에서 실행 되는 경우 [sp_changemergesubscription](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md) 를 사용 하 여 배포자에서 실행 되는 밀어넣기 구독을 동기화 하는 병합 에이전트 작업의 속성을 변경 해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 배포자에서 **sysadmin** 고정 서버 역할의 멤버만 **sp_MSchange_merge_agent_properties**를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_addmergepushsubscription_agent &#40;](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md)   
 [Transact-sql&#41;sp_addmergesubscription &#40;](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)  
  
  
