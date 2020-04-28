---
title: sp_revoke_publication_access (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_revoke_publication_access_TSQL
- sp_revoke_publication_access
helpviewer_keywords:
- sp_revoke_publication_access
ms.assetid: 84ed9e77-991f-4fa5-a21f-7c6bfec1b3e3
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 2724a62f6bf55941edbaa206728f9352e8fce5c1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67941723"
---
# <a name="sp_revoke_publication_access-transact-sql"></a>sp_revoke_publication_access(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  게시 액세스 목록에서 로그인을 제거합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_revoke_publication_access [ @publication = ] 'publication' , [ @login = ] 'login'  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'`액세스할 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @login = ] 'login'`로그인 ID입니다. *login* 은 **sysname**이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_revoke_publication_access** 은 스냅숏, 트랜잭션 및 병합 복제에 사용 됩니다.  
  
 **sp_revoke_publication_access** 를 반복적으로 호출할 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_revoke_publication_access**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_grant_publication_access &#40;](../../relational-databases/system-stored-procedures/sp-grant-publication-access-transact-sql.md)   
 [Transact-sql&#41;sp_help_publication_access &#40;](../../relational-databases/system-stored-procedures/sp-help-publication-access-transact-sql.md)   
 [게시자 보안 설정](../../relational-databases/replication/security/secure-the-publisher.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
