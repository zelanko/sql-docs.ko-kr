---
title: sp_unsetapprole (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_unsetapprole_TSQL
- sp_unsetapprole
dev_langs:
- TSQL
helpviewer_keywords:
- sp_unsetapprole
ms.assetid: 4c4033d3-1a34-4dfb-835d-e3293d1a442d
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: ad1bc32a3d1eb6b42ccd7c709217427d2926bac6
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="spunsetapprole-transact-sql"></a>sp_unsetapprole(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  응용 프로그램 역할을 비활성화하고 이전의 보안 컨텍스트로 되돌립니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_unsetapprole @cookie   
```  
  
## <a name="arguments"></a>인수  
 **@cookie**  
 응용 프로그램 역할을 활성화할 때 생성된 쿠키를 지정합니다. 쿠키 만들어집니다 [sp_setapprole &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)합니다. **varbinary (8000)** 합니다.  
  
> [!NOTE]  
>  현재 **sp_setapprole** 에 대한 쿠키 **OUTPUT** 매개 변수는 정확한 최대 길이인 **varbinary(8000)** 로 정의되어 있습니다. 그러나 현재 구현은 **varbinary(50)** 입니다. 응용 프로그램은 계속해서 **varbinary(8000)** 를 예약하여 후속 릴리스에서 쿠키 반환 크기가 늘어날 경우에도 응용 프로그램이 제대로 작동할 수 있도록 해야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 및 1(실패)  
  
## <a name="remarks"></a>주의  
 응용 프로그램 역할이 활성화에 사용 하 여 **sp_setapprole**를 활성 상태로 사용자는 서버에서 연결을 끊습니다 또는 실행 될 때까지 **sp_unsetapprole**합니다.  
  
 응용 프로그램 역할의 개요를 참조 하십시오. [응용 프로그램 역할](../../relational-databases/security/authentication-access/application-roles.md)합니다.  
  
## <a name="permissions"></a>Permissions  
 멤버 자격이 필요 **공용** 및 응용 프로그램 역할을 활성화할 때 저장 된 쿠키를 알아야 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="activating-an-application-role-with-a-cookie-then-reverting-to-the-previous-context"></a>쿠키를 사용하여 응용 프로그램 역할을 활성화한 다음 이전 컨텍스트로 되돌리기  
 다음 예에서는 `Sales11` 암호로 `fdsd896#gfdbfdkjgh700mM` 응용 프로그램 역할을 활성화하고 쿠키를 만듭니다. 이 예제에서는 현재 사용자의 이름을 반환 하 고 다음을 실행 하 여 원래 컨텍스트로 되돌아갑니다 **sp_unsetapprole**합니다.  
  
```  
DECLARE @cookie varbinary(8000);  
EXEC sp_setapprole 'Sales11', 'fdsd896#gfdbfdkjgh700mM'  
    , @fCreateCookie = true, @cookie = @cookie OUTPUT;  
-- The application role is now active.  
SELECT USER_NAME();  
-- This will return the name of the application role, Sales11.  
EXEC sp_unsetapprole @cookie;  
-- The application role is no longer active.  
-- The original context has now been restored.  
GO  
SELECT USER_NAME();  
-- This will return the name of the original user.   
GO   
```  
  
## <a name="see-also"></a>관련 항목:  
 [sp_setapprole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Security Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [DROP APPLICATION ROLE&#40;Transact-SQL&#41;](../../t-sql/statements/drop-application-role-transact-sql.md)  
  
  
