---
description: sp_help_publication_access(Transact-SQL)
title: sp_help_publication_access (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_help_publication_access
- sp_help_publication_access_TSQL
helpviewer_keywords:
- sp_help_publication_access
ms.assetid: 9408fa13-54a0-4cb1-8fb0-845e5536ef50
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5a40f12ade4dcbb08609da6184fa0a96ca9926cd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88485986"
---
# <a name="sp_help_publication_access-transact-sql"></a>sp_help_publication_access(Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  게시에 대해 허가된 모든 로그인의 목록을 반환합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_publication_access [ @publication = ] 'publication'  
    [ , [ @return_granted = ] 'return_granted' ]   
    [ , [ @login = ] 'login' ]  
    [ , [ @initial_list = ] initial_list ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'` 액세스할 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @return_granted = ] 'return_granted'` 로그인 ID입니다. *return_granted* 은 **bit**이며 기본값은 1입니다. **0** 을 지정 하 고 인증을 사용 하는 경우 게시자에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 표시 되지만 배포자에는 표시 되지 않는 사용 가능한 로그인이 반환 됩니다. **0** 을 지정 하 고 Windows 인증을 사용 하는 경우 게시자 또는 배포자에서 특별히 액세스가 거부 되지 않은 로그인이 반환 됩니다.  
  
`[ @login = ] 'login'` 표준 보안 로그인 ID입니다. *login* 은 **sysname**이며 기본값은 **%** 입니다.  
  
`[ @initial_list = ] initial_list` 게시 액세스 권한이 있는 모든 멤버를 반환할지 아니면 새 멤버가 목록에 추가 되기 전에 액세스 권한이 있는 사용자만 반환할지를 지정 합니다. *initial_list* 은 bit 이며 기본값은 **0**입니다.  
  
 **1** 은 게시를 만들 때 사용 된 배포자에서 유효한 로그인과 함께 **sysadmin** 고정 서버 역할의 모든 멤버와 현재 로그인에 대 한 정보를 반환 합니다.  
  
 **0** 은 (는 **) sysadmin 고정** 서버 역할에 속하지 않는 게시 액세스 목록의 모든 사용자 뿐만 아니라 게시를 만들 때 사용 했던 배포자에서 유효한 로그인을 사용 하는 **sysadmin** 고정 서버 역할의 모든 멤버에 대 한 정보를 반환 합니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**Loginname**|**nvarchar(256)**|실제 로그인 이름입니다.|  
|**Isntname**|**int**|**0** = 로그인이 Windows 사용자가 아닙니다.<br /><br /> **1** = 로그인이 Windows 사용자입니다.|  
|**Isntgroup**|**int**|**0** = 로그인이 Windows 그룹이 아닙니다.<br /><br /> **1** = 로그인이 Windows 그룹입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_help_publication_access** 은 모든 유형의 복제에 사용 됩니다.  
  
 결과 집합에서 **Isntname** 및 **Isntgroup** 가 모두 **0**인 경우 로그인이 로그인 이라고 가정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_help_publication_access**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_grant_publication_access &#40;](../../relational-databases/system-stored-procedures/sp-grant-publication-access-transact-sql.md)   
 [Transact-sql&#41;sp_revoke_publication_access &#40;](../../relational-databases/system-stored-procedures/sp-revoke-publication-access-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
