---
title: sp_help_publication_access (TRANSACT-SQL) | Microsoft Docs
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
- sp_help_publication_access
- sp_help_publication_access_TSQL
helpviewer_keywords:
- sp_help_publication_access
ms.assetid: 9408fa13-54a0-4cb1-8fb0-845e5536ef50
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 803b5d26fa2294a9e53d3afb597a232384dfd38d
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43036188"
---
# <a name="sphelppublicationaccess-transact-sql"></a>sp_help_publication_access(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  게시에 대해 허가된 모든 로그인의 목록을 반환합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_publication_access [ @publication = ] 'publication'  
    [ , [ @return_granted = ] 'return_granted' ]   
    [ , [ @login = ] 'login' ]  
    [ , [ @initial_list = ] initial_list ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@publication=**] **'***publication***'**  
 액세스할 게시의 이름입니다. *게시* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [  **@return_granted=**] **'***return_granted***'**  
 로그인 ID입니다. *return_granted* 됩니다 **비트**, 기본값은 1입니다. 하는 경우 **0** 지정 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증이 사용 되는 게시자 나 배포자에 없습니다 표시 되는 사용 가능한 로그인 반환 됩니다. 하는 경우 **0** 지정 및 Windows 인증이 사용 되는, 명시적으로 거부 로그인 액세스에서 게시자 또는 배포자가 반환 됩니다.  
  
 [  **@login=**] **'***로그인***'**  
 표준 보안 로그인 ID입니다. *로그인* 됩니다 **sysname**, 기본값은 **%** 합니다.  
  
 [  **@initial_list =**] *initial_list*  
 게시 액세스 권한이 있는 모든 멤버를 반환할지 또는 목록에 새 멤버가 추가되기 전에 액세스 권한을 가졌던 멤버만 반환할지 지정합니다. *initial_list* 는 bit 이며 기본값은 **0**합니다.  
  
 **1** 의 모든 멤버에 대 한 정보를 반환 합니다 **sysadmin** 현재 로그인 뿐만 아니라 게시를 만들 때 존재 하는 배포자에서 유효한 로그인을 사용 하 여 고정된 서버 역할입니다.  
  
 **0** 의 모든 멤버에 대 한 정보를 반환 합니다 **sysadmin** 하지 게시를 만들 때도 모든 사용자가 게시 액세스 목록에 존재 하는 배포자에서 유효한 로그인을 사용 하 여 고정된 서버 역할 에 속해야 합니다 **sysadmin** 고정된 서버 역할입니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**Loginname**|**nvarchar(256)**|실제 로그인 이름입니다.|  
|**isntname**|**int**|**0** = 로그인이 Windows 사용자입니다.<br /><br /> **1** = 로그인이 Windows 사용자입니다.|  
|**isntgroup**|**int**|**0** = 로그인이 Windows 그룹입니다.<br /><br /> **1** = 로그인이 Windows 그룹입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_help_publication_access** 모든 유형의 복제에 사용 됩니다.  
  
 때 둘 다 **Isntname** 및 **Isntgroup** 집합에 결과 **0**, 로그인 임을 가정를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 합니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_help_publication_access**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [sp_grant_publication_access &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-publication-access-transact-sql.md)   
 [sp_revoke_publication_access &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revoke-publication-access-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
