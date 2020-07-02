---
title: sp_unsetapprole (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_unsetapprole_TSQL
- sp_unsetapprole
dev_langs:
- TSQL
helpviewer_keywords:
- sp_unsetapprole
ms.assetid: 4c4033d3-1a34-4dfb-835d-e3293d1a442d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 700bab92fde35f26ba1ce6ca956fabd72f130e31
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85762741"
---
# <a name="sp_unsetapprole-transact-sql"></a>sp_unsetapprole(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  애플리케이션 역할을 비활성화하고 이전의 보안 컨텍스트로 되돌립니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_unsetapprole @cookie   
```  
  
## <a name="arguments"></a>인수  
 **\@쿠키가**  
 애플리케이션 역할을 활성화할 때 생성된 쿠키를 지정합니다. 쿠키는 [transact-sql&#41;&#40;sp_setapprole ](../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)에 의해 만들어집니다. **varbinary (8000)**.  
  
> [!NOTE]  
>  현재 **sp_setapprole** 에 대한 쿠키 **OUTPUT** 매개 변수는 정확한 최대 길이인 **varbinary(8000)** 로 정의되어 있습니다. 그러나 현재 구현은 **varbinary(50)** 입니다. 애플리케이션은 계속해서 **varbinary(8000)** 를 예약하여 후속 릴리스에서 쿠키 반환 크기가 늘어날 경우에도 애플리케이션이 제대로 작동할 수 있도록 해야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 및 1(실패)  
  
## <a name="remarks"></a>설명  
 **Sp_setapprole**를 사용 하 여 응용 프로그램 역할을 활성화 한 후에는 사용자가 서버에서 연결을 끊거나 **sp_unsetapprole**를 실행할 때까지 역할은 활성 상태로 유지 됩니다.  
  
 응용 프로그램 역할에 대 한 개요는 [응용 프로그램 역할](../../relational-databases/security/authentication-access/application-roles.md)을 참조 하세요.  
  
## <a name="permissions"></a>사용 권한  
 **Public** 의 멤버 자격이 필요 하 고 응용 프로그램 역할이 활성화 되었을 때 저장 된 쿠키에 대 한 지식이 필요 합니다.  
  
## <a name="examples"></a>예제  
  
### <a name="activating-an-application-role-with-a-cookie-then-reverting-to-the-previous-context"></a>쿠키를 사용하여 애플리케이션 역할을 활성화한 다음 이전 컨텍스트로 되돌리기  
 다음 예에서는 `Sales11` 암호로 `fdsd896#gfdbfdkjgh700mM` 애플리케이션 역할을 활성화하고 쿠키를 만듭니다. 이 예에서는 현재 사용자의 이름을 반환 하 고 **sp_unsetapprole**를 실행 하 여 원래 컨텍스트로 되돌립니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_setapprole &#40;](../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)   
 [Transact-sql&#41;&#40;시스템 저장 프로시저](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;&#40;보안 저장 프로시저](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;&#40;응용 프로그램 역할 만들기](../../t-sql/statements/create-application-role-transact-sql.md)   
 [DROP APPLICATION ROLE&#40;Transact-SQL&#41;](../../t-sql/statements/drop-application-role-transact-sql.md)  
  
  
