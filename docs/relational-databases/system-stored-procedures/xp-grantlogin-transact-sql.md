---
title: xp_grantlogin (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_grantlogin
- xp_grantlogin_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_grantlogin
ms.assetid: c851c1ab-3b29-4b99-9902-78c2665a844b
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 957bbdc43c0f0adf3a545fee76e9f69df130d8f9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68116668"
---
# <a name="xp_grantlogin-transact-sql"></a>xp_grantlogin(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Windows 그룹 또는 사용자에게 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 액세스 권한을 부여합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]대신 [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md) 을 사용 해야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
xp_grantlogin {[@loginame = ] 'login'} [,[@logintype = ] 'logintype']  
```  
  
## <a name="arguments"></a>인수  
`[ @loginame = ] 'login'`추가할 Windows 사용자 또는 그룹의 이름입니다. Windows 사용자 또는 그룹은 *도메인*\\*사용자*형식의 windows 도메인 이름으로 한정 되어야 합니다. *login* 은 **sysname**이며 기본값은 없습니다.  
  
`[ @logintype = ] 'logintype'`액세스 권한을 부여 받은 로그인의 보안 수준입니다. *logintype* 은 **varchar (5)** 이며 기본값은 NULL입니다. **관리자** 만 지정할 수 있습니다. **Admin** 이 지정 된 경우 *로그인* 에 대 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]한 액세스 권한이 부여 되 고 **sysadmin** 고정 서버 역할의 멤버로 추가 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
 이제 **xp_grantlogin** 는 확장 저장 프로시저가 아닌 시스템 저장 프로시저입니다. **xp_grantlogin** 는 **sp_grantlogin** 및 **sp_addsrvrolemember**를 호출 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Securityadmin** 고정 서버 역할의 멤버 자격이 필요 합니다. *Logintype*를 변경 하는 경우에는 **sysadmin** 고정 서버 역할의 멤버 자격이 필요 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_denylogin &#40;](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [Transact-sql&#41;sp_grantlogin &#40;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [Transact-sql&#41;&#40;시스템 저장 프로시저](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;일반 확장 저장 프로시저 &#40;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;xp_enumgroups &#40;](../../relational-databases/system-stored-procedures/xp-enumgroups-transact-sql.md)   
 [Transact-sql&#41;xp_loginconfig &#40;](../../relational-databases/system-stored-procedures/xp-loginconfig-transact-sql.md)   
 [Transact-sql&#41;xp_logininfo &#40;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)   
 [sp_revokelogin&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)  
  
  
