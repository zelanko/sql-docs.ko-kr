---
title: xp_revokelogin (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_revokelogin
- xp_revokelogin_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_revokelogin
ms.assetid: b3fa7678-dba4-4537-be94-5ae63ca11f81
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: f4b5e0f04f893bd5f351857a5a1b655d52350c52
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67898345"
---
# <a name="xp_revokelogin-transact-sql"></a>xp_revokelogin(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Windows 그룹 또는 사용자의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 액세스 권한을 취소합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]대신 [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md) 을 사용 해야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
xp_revokelogin {[@loginame=] 'login'}  
```  
  
## <a name="arguments"></a>인수  
`[ @loginame = ] 'login'`액세스를 취소할 Windows 사용자 또는 그룹의 이름입니다. *로그인* 에는 도메인 이름 (예: **[ADVWKS\sylvester1])** 이 포함 되어야 합니다. *login* 은 **sysname**이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
 대신 DROP LOGIN을 사용해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 서버에 대한 ALTER ANY LOGIN 권한이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_denylogin &#40;](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [Transact-sql&#41;sp_grantlogin &#40;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [Transact-sql&#41;sp_revokelogin &#40;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [Transact-sql&#41;&#40;시스템 저장 프로시저](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;일반 확장 저장 프로시저 &#40;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;xp_loginconfig &#40;](../../relational-databases/system-stored-procedures/xp-loginconfig-transact-sql.md)   
 [Transact-sql&#41;xp_logininfo &#40;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)  
  
  
