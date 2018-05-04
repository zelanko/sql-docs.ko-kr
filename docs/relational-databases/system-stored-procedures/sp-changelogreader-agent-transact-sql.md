---
title: sp_changelogreader_agent (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- sp_changelogreader_agent
- sp_changelogreader_agent_TSQL
helpviewer_keywords:
- sp_changelogreader_agent
ms.assetid: 929b2fa7-1267-41d0-8b69-e9ab26a62c0f
caps.latest.revision: 21
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 076e6706e4e6272b56d677692e1ae658ed76faf4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="spchangelogreaderagent-transact-sql"></a>sp_changelogreader_agent(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  로그 판독기 에이전트의 보안 속성을 변경합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
> [!IMPORTANT]  
>  게시자를 원격 배포자로 구성할 경우 *job_login* 및 *job_password*를 비롯한 모든 매개 변수에 제공된 값이 일반 텍스트로 배포자에게 전송됩니다. 이 저장 프로시저를 실행하기 전에 게시자와 해당 원격 배포자 간 연결을 암호화해야 합니다. 자세한 내용은 [데이터베이스 엔진에 암호화 연결 사용&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)을 참조하세요.  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_changelogreader_agent [ [ @job_login = ] 'job_login' ]  
    [ , [ @job_password = ] 'job_password' ]  
    [ , [ @publisher_security_mode = ] publisher_security_mode ]  
    [ , [ @publisher_login = ] 'publisher_login' ]  
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@job_login**=] **'***job_login***'**  
 에이전트 실행에 사용되는 Windows 계정의 로그인입니다. *job_login* 은 **nvarchar (257)**, 기본값은 NULL입니다. *이 이외에 대 한 변경할 수 없습니다* [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *게시자입니다.*  
  
 [ **@job_password**=] **'***job_password***'**  
 에이전트 실행에 사용되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 계정의 암호입니다. *job_password* 은 **sysname**, 기본값은 NULL입니다.  
  
> [!IMPORTANT]  
>  가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 스크립트 파일에 저장해야 하는 경우에는 파일에 무단으로 액세스하지 못하도록 보안을 설정해야 합니다.  
  
 [ **@publisher_security_mode**=] *publisher_security_mode*  
 게시자에 연결할 때 에이전트가 사용하는 보안 모드입니다. *publisher_security_mode* 은 **smallint**, 기본값은 NULL입니다. **0** 지정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 하 고 **1** Windows 인증을 지정 합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 [ **@publisher_login**=] **'***publisher_login***'**  
 게시자에 연결할 때 사용하는 로그인입니다. *publisher_login* 은 **sysname**, 기본값은 NULL입니다. *publisher_login* 지정 해야 *publisher_security_mode* 은 **0**합니다. 경우 *publisher_login* null 및 *publisher_security_mode* 은 **1**에 지정 된 Windows 계정이 *job_login* 될 때 사용 됩니다 게시자에 연결합니다.  
  
 [ **@publisher_password**=] **'***publisher_password***'**  
 게시자에 연결할 때 사용하는 암호입니다. *publisher_password* 은 **sysname**, 기본값은 NULL입니다.  
  
> [!IMPORTANT]  
>  빈 암호를 사용하지 마세요. 강력한 암호를 사용하세요. 가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 스크립트 파일에 저장해야 하는 경우에는 파일에 무단으로 액세스하지 못하도록 보안을 설정해야 합니다.  
  
 [ **@publisher**=] **'***게시자***'**  
 게시자의 이름입니다. *게시자* 은 **sysname**, 기본값은 NULL입니다. 이 매개 변수는 SQL Server 이외 게시자용으로만 지원됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_changelogreader_agent** 트랜잭션 복제에 사용 됩니다.  
  
 **sp_changelogreader_agent** 로그 판독기 에이전트가 실행 되는 Windows 계정을 변경 하는 데 사용 됩니다. 기존 Windows 로그인의 암호를 변경하거나 새 Windows 로그인과 암호를 제공할 수 있습니다.  
  
 에이전트 로그인 또는 암호를 변경한 후 에이전트를 중지하고 다시 시작해야 변경 내용이 적용됩니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_changelogreader_agent**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [복제 보안 설정 보기 및 수정](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [sp_helplogreader_agent &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md)   
 [sp_addlogreader_agent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)  
  
  
