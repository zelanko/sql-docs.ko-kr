---
title: sp_link_publication (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_link_publication_TSQL
- sp_link_publication
helpviewer_keywords:
- sp_link_publication
ms.assetid: 1945ed24-f9f1-4af6-94ca-16d8e864706e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 976109aa0ef09575f818ff6daf82e742626dede7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85756645"
---
# <a name="sp_link_publication-transact-sql"></a>sp_link_publication(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  즉시 업데이트 구독의 동기화 트리거가 게시자에 연결할 때 사용하는 구성 및 보안 정보를 설정합니다. 이 저장 프로시저는 구독 데이터베이스의 구독자에서 실행됩니다.  
  
> [!IMPORTANT]
>  게시자를 원격 배포자로 구성할 경우 *job_login* 및 *job_password*를 비롯한 모든 매개 변수에 제공된 값이 일반 텍스트로 배포자에게 전송됩니다. 이 저장 프로시저를 실행하기 전에 게시자와 해당 원격 배포자 간 연결을 암호화해야 합니다. 자세한 내용은 [데이터베이스 엔진에 암호화 연결 사용&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)을 참조하세요.  
> 
> [!IMPORTANT]
>  특정 상황에서는 구독자가 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 서비스 팩 1 이상을 실행 하 고 게시자가 이전 버전을 실행 하는 경우이 저장 프로시저가 실패할 수 있습니다. 이 시나리오에서 저장 프로시저가 실패하면 게시자를 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 서비스 팩 1 이상으로 업그레이드합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_link_publication [ @publisher = ] 'publisher'   
        , [ @publisher_db = ] 'publisher_db'   
        , [ @publication = ] 'publication'   
        , [ @security_mode = ] security_mode  
    [ , [ @login = ] 'login' ]  
    [ , [ @password = ]'password' ]  
    [ , [ @distributor = ] 'distributor' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publisher = ] 'publisher'`연결할 게시자의 이름입니다. *publisher* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publisher_db = ] 'publisher_db'`연결할 게시자 데이터베이스의 이름입니다. *publisher_db* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publication = ] 'publication'`연결할 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @security_mode = ] security_mode`즉시 업데이트를 위해 구독자가 원격 게시자에 연결 하는 데 사용 하는 보안 모드입니다. *security_mode* 은 **int**이며 다음 값 중 하나일 수 있습니다. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
|값|Description|  
|-----------|-----------------|  
|**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서이 저장 프로시저에 지정 된 로그인과 *암호*를 *login* 사용 하 여 인증을 사용 합니다.<br /><br /> 참고: 이전 버전의에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이 옵션은 동적 RPC (원격 프로시저 호출)를 지정 하는 데 사용 되었습니다.|  
|**1**|구독자에서 변경하는 사용자의 보안 컨텍스트([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 또는 Windows 인증)를 사용합니다.<br /><br /> 참고:이 계정은 권한이 있는 게시자에도 있어야 합니다. Windows 인증을 사용할 때는 보안 계정 위임이 지원되어야 합니다.|  
|**2**|**Sp_link_publication**를 사용 하 여 만든 기존의 사용자 정의 연결 된 서버 로그인을 사용 합니다.|  
  
`[ @login = ] 'login'`로그인입니다. *login*은 **sysname**이며 기본값은 NULL입니다. *Security_mode* 가 **0**인 경우이 매개 변수를 지정 해야 합니다.  
  
`[ @password = ] 'password'`암호입니다. *password* 는 **sysname**이며 기본값은 NULL입니다. *Security_mode* 가 **0**인 경우이 매개 변수를 지정 해야 합니다.  
  
`[ @distributor = ] 'distributor'`배포자의 이름입니다. *배포자* 는 **sysname**이며 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_link_publication** 은 트랜잭션 복제에서 즉시 업데이트 구독에 사용 됩니다.  
  
 밀어넣기 및 끌어오기 구독 모두에 **sp_link_publication** 를 사용할 수 있습니다. 구독을 만들기 전이나 후에 호출할 수 있습니다. 항목이 [MSsubscription_properties &#40;transact-sql&#41;](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md) 시스템 테이블에 삽입 되거나 업데이트 됩니다.  
  
 밀어넣기 구독의 경우 [transact-sql&#41;&#40;sp_subscription_cleanup ](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md)여 항목을 정리할 수 있습니다. 끌어오기 구독의 경우 Transact-sql&#41;또는 [sp_subscription_cleanup &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md)을 [sp_droppullsubscription &#40;](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md) 항목을 정리할 수 있습니다. NULL 암호를 사용 하 여 **sp_link_publication** 를 호출 하 여 보안 문제에 대 한 [MSsubscription_properties &#40;transact-sql&#41;](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md) 시스템 테이블의 항목을 지울 수도 있습니다.  
  
 즉시 업데이트 구독자가 게시자에 연결할 때 사용하는 기본 모드에서는 Windows 인증을 사용한 연결을 사용할 수 없습니다. Windows 인증 모드로 연결하려면 연결된 서버가 게시자에 설정되어 있고 즉시 업데이트 구독자가 구독자를 업데이트할 때 이 연결을 사용해야 합니다. 이렇게 하려면 *security_mode*2를 사용 하 여 **sp_link_publication** 실행 해야 합니다  =  **2**. Windows 인증을 사용할 때는 보안 계정 위임이 지원되어야 합니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_addtranpullsubscriptionagent_failover](../../relational-databases/replication/codesnippet/tsql/sp-link-publication-tran_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만 **sp_link_publication**를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_droppullsubscription &#40;](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md)   
 [Transact-sql&#41;sp_helpsubscription_properties &#40;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)   
 [Transact-sql&#41;sp_subscription_cleanup &#40;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
