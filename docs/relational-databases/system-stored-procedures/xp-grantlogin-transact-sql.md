---
title: xp_grantlogin (TRANSACT-SQL) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: a6b08e90fafccca3c64b13132b9cf9e248fdee7e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47663779"
---
# <a name="xpgrantlogin-transact-sql"></a>xp_grantlogin(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Windows 그룹 또는 사용자에게 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 액세스 권한을 부여합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 사용 하 여 [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md) 대신 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
xp_grantlogin {[@loginame = ] 'login'} [,[@logintype = ] 'logintype']  
```  
  
## <a name="arguments"></a>인수  
 [ **@loginame =** ] **'***login***'**  
 추가할 Windows 사용자 또는 그룹의 이름입니다. Windows 사용자 또는 그룹을 폼에 있는 Windows 도메인 이름으로 한정 되어야 합니다 *도메인*\\*사용자*합니다. *로그인* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [  **@logintype =** ] **'***logintype***'**  
 액세스를 부여할 로그인의 보안 수준입니다. *logintype* 됩니다 **varchar(5)**, 기본값은 NULL입니다. 만 **관리자** 지정할 수 있습니다. 경우 **관리자** 지정 된 경우 *로그인* 에 대 한 액세스 권한이 부여 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 구성원으로 추가 합니다 **sysadmin** 고정된 서버 역할입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>Remarks  
 **xp_grantlogin** 시스템 저장 프로시저는 확장된 저장된 프로시저 대신 되었습니다. **xp_grantlogin** 호출 **sp_grantlogin** 하 고 **sp_addsrvrolemember**합니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버 자격이 필요 합니다 **securityadmin** 고정된 서버 역할입니다. 변경 하는 경우는 *logintype*의 멤버 자격이 필요 합니다 **sysadmin** 고정된 서버 역할입니다.  
  
## <a name="see-also"></a>관련 항목  
 [sp_denylogin&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [sp_grantlogin&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [일반 확장 저장된 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_enumgroups &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/xp-enumgroups-transact-sql.md)   
 [xp_loginconfig &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/xp-loginconfig-transact-sql.md)   
 [xp_logininfo &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)   
 [sp_revokelogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)  
  
  
