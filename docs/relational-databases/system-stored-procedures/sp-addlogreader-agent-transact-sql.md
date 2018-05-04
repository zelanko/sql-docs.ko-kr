---
title: sp_addlogreader_agent (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- sp_addlogreader_agent
- sp_addlogreader_agent_TSQL
helpviewer_keywords:
- sp_addlogreader_agent
ms.assetid: d83096b9-96ee-4789-bde0-940d4765b9ed
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 96954747e39c2b5740af743d2d55c8bf02d2f66b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="spaddlogreaderagent-transact-sql"></a>sp_addlogreader_agent(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정된 데이터베이스에 대해 로그 판독기 에이전트를 추가합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
> [!IMPORTANT]  
>  게시자를 원격 배포자로 구성할 경우 *job_login* 및 *job_password*를 비롯한 모든 매개 변수에 제공된 값이 일반 텍스트로 배포자에게 전송됩니다. 이 저장 프로시저를 실행하기 전에 게시자와 해당 원격 배포자 간 연결을 암호화해야 합니다. 자세한 내용은 [데이터베이스 엔진에 암호화 연결 사용&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_addlogreader_agent [ @job_login = ] 'job_login'  
        , [ @job_password = ] 'job_password'  
    [ , [ @job_name = ] 'job_name' ]  
    [ , [ @publisher_security_mode = ] publisher_security_mode ]  
    [ , [ @publisher_login = ] 'publisher_login' ]  
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@job_login**=] **'***job_login***'**  
 에이전트 실행에 사용되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 계정의 로그인입니다. *job_login* 은 **nvarchar (257)**, 기본값은 NULL입니다. 이 Windows 계정은 에이전트가 배포자에 연결할 때 항상 사용됩니다.  
  
> [!NOTE]  
>  에 대 한 비-[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자의 경우에 지정 된 동일한 로그인 이어야 합니다. [sp_adddistpublisher &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)합니다.  
  
 [ **@job_password**=] **'***job_password***'**  
 에이전트 실행에 사용되는 Windows 계정의 암호입니다. *job_password* 은 **sysname**, 기본값은 NULL입니다.  
  
> [!IMPORTANT]  
>  스크립트 파일에 인증 정보를 저장하지 않도록 합니다. 최상의 보안을 위해 런타임에 로그인 이름과 암호를 제공해야 합니다.  
  
 [ **@job_name**=] **'***job_name***'**  
 기존 에이전트 작업의 이름입니다. *job_name* 은 **sysname**, 기본값은 NULL입니다. 이 매개 변수는 에이전트가 새로 만든 작업(기본값) 대신 기존 작업을 사용하여 시작된 경우에만 지정됩니다.  
  
 [ **@publisher_security_mode**=] *publisher_security_mode*  
 게시자에 연결할 때 에이전트가 사용하는 보안 모드입니다. *publisher_security_mode* 은 **smallint**, 기본값은 **1**합니다. **0** 지정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 하 고 **1** Windows 인증을 지정 합니다. 값이 **0** 지정 해야 이외[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다.  
  
 [ **@publisher_login**=] **'***publisher_login***'**  
 게시자에 연결할 때 사용하는 로그인입니다. *publisher_login* 은 **sysname**, 기본값은 NULL입니다. *publisher_login* 지정 해야 *publisher_security_mode* 은 **0**합니다. 경우 *publisher_login* null 및 *publisher_security_mode* 은 **1**에 지정 된 Windows 계정이 *job_login* 사용 됩니다 게시자에 연결 합니다.  
  
 [ **@publisher_password**=] **'***publisher_password***'**  
 게시자에 연결할 때 사용하는 암호입니다. *publisher_password* 은 **sysname**, 기본값은 NULL입니다.  
  
> [!IMPORTANT]  
>  스크립트 파일에 인증 정보를 저장하지 않도록 합니다. 최상의 보안을 위해 런타임에 로그인 이름과 암호를 제공해야 합니다.  
  
 [ **@publisher**=] **'***게시자***'**  
 비의 이름인[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다. *게시자* 은 **sysname**, 기본값은 NULL입니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자에 이 매개 변수를 지정하지 않습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_addlogreader_agent** 트랜잭션 복제에 사용 됩니다.  
  
 실행 해야 **sp_addlogreader_agent** 이 버전의에 대 한 복제 설정 된 데이터베이스를 업그레이드 한 경우 로그 판독기 에이전트를 추가 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 전에 데이터베이스를 사용 하는 게시가 생성 합니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_addlogreader_agent**합니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_AddTranPub](../../relational-databases/replication/codesnippet/tsql/sp-addlogreader-agent-tr_1.sql)]  
  
## <a name="see-also"></a>관련 항목:  
 [게시 만들기](../../relational-databases/replication/publish/create-a-publication.md)   
 [sp_addpublication &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changelogreader_agent &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
