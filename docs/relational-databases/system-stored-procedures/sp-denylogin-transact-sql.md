---
description: sp_denylogin(Transact-SQL)
title: sp_denylogin (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_denylogin_TSQL
- sp_denylogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_denylogin
ms.assetid: db80f152-e8af-4303-95b6-3a3a7b664374
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4a2ac84bae7f12509addc44ff8dabcdb0101cf2f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464359"
---
# <a name="sp_denylogin-transact-sql"></a>sp_denylogin(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Windows 사용자 또는 Windows 그룹이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결하는 것을 방지합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 대신 [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) 을 사용 해야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_denylogin [ @loginame = ] 'login'   
```  
  
## <a name="arguments"></a>인수  
`[ @loginame = ] 'login_ '` Windows 사용자 또는 그룹의 이름입니다. *login* 은 **sysname**이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
 **sp_denylogin** 는 지정 된 windows 사용자 또는 windows 그룹에 매핑된 서버 수준 보안 주체에 대 한 CONNECT SQL 권한을 거부 합니다. 서버 보안 주체가 없으면 새로 생성됩니다. 새 주 서버는 [server_principals &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) 카탈로그 뷰에 표시 됩니다.  
  
 사용자 정의 트랜잭션 내에서는 **sp_denylogin** 을 실행할 수 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 **sp_denylogin** 를 사용 하 여 Windows 사용자가 `CORPORATE\GeorgeV` 서버에 연결 하지 못하도록 하는 방법을 보여 줍니다.  
  
```  
EXEC sp_denylogin 'CORPORATE\GeorgeV';  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_grantlogin &#40;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [Transact-sql&#41;&#40;보안 저장 프로시저 ](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
