---
title: sp_changereplicationserverpasswords (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changereplicationserverpasswords_TSQL
- sp_changereplicationserverpasswords
helpviewer_keywords:
- sp_changereplicationserverpasswords
ms.assetid: 9333da96-3a1c-4adb-9a74-5dac9ce596df
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: d3f992fefc04de89fcfa9e077d01641fa538ea40
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85771407"
---
# <a name="sp_changereplicationserverpasswords-transact-sql"></a>sp_changereplicationserverpasswords(Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  복제 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 토폴로지의 서버에 연결할 때 복제 에이전트에서 사용 하는 Windows 계정 또는 로그인에 저장 된 암호를 변경 합니다. 서버에서 실행 중인 모든 에이전트가 동일한 로그인 또는 계정을 사용하더라도 보통은 각 에이전트의 암호를 개별적으로 변경해야 합니다. 이 저장 프로시저를 사용하면 서버에서 실행 중인 모든 복제 에이전트에서 사용하는 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인이나 Windows 계정의 모든 인스턴스에 대한 암호를 변경할 수 있습니다. 이 저장 프로시저는 master 데이터베이스의 복제 토폴로지에 있는 모든 서버에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_changereplicationserverpasswords [ @login_type = ] login_type  
        , [ @login = ] 'login'   
        , [ @password = ] 'password'  
    [ , [ @server = ] 'server' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @login_type = ] login_type`제공 된 자격 증명에 대 한 인증 유형입니다. *login_type* 은 **tinyint**이며 기본값은 없습니다.  
  
 **1** = Windows 통합 인증  
  
 **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증  
  
`[ @login = ] 'login'`변경할 Windows 계정 또는 로그인의 이름입니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . *login* 은 **nvarchar (257)** 이며 기본값은 없습니다.  
  
`[ @password = ] 'password'`지정 된 *로그인*에 대해 저장할 새 암호입니다. *password* 는 **sysname**이며 기본값은 없습니다.  
  
> [!NOTE]  
>  복제 암호를 변경한 후 해당 암호를 사용하는 각 에이전트를 중지한 다음 다시 시작해야 에이전트에 변경 내용이 적용됩니다.  
  
`[ @server = ] 'server'`저장 된 암호를 변경할 서버 연결입니다. *서버* 는 **sysname**이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**총판**|배포자에 대한 모든 에이전트 연결입니다.|  
|**발행자**|게시자에 대한 모든 에이전트 연결입니다.|  
|**구독자**|구독자에 대한 모든 에이전트 연결입니다.|  
|**%** 기본|복제 토폴로지의 모든 서버에 대한 모든 에이전트 연결입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_changereplicationserverpasswords** 은 모든 유형의 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만 **sp_changereplicationserverpasswords**를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [복제 보안 설정 보기 및 수정](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)  
  
  
