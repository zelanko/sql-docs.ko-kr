---
title: sp_setapprole (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_setapprole
- sp_setapprole_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_setapprole
ms.assetid: cf0901c0-5f90-42d4-9d5b-8772c904062d
caps.latest.revision: "42"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cc1376391dcf0fefd0fb621d73817b8257b95bf9
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2017
---
# <a name="spsetapprole-transact-sql"></a>sp_setapprole(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 데이터베이스의 응용 프로그램 역할과 연관된 사용 권한을 활성화합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_setapprole [ @rolename = ] 'role',  
    [ @password = ] { encrypt N'password' }   
      |  
        'password' [ , [ @encrypt = ] { 'none' | 'odbc' } ]  
        [ , [ @fCreateCookie = ] true | false ]  
    [ , [ @cookie = ] @cookie OUTPUT ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@rolename =** ] **'***역할***'**  
 현재 데이터베이스에 정의된 응용 프로그램 역할의 이름입니다. *역할* 은 **sysname**, 기본값은 없습니다. *역할* 현재 데이터베이스에 존재 해야 합니다.  
  
 [  **@password =** ] **{암호화 N'***암호***'을 (를)**  
 응용 프로그램 역할을 활성화하는 데 필요한 암호입니다. *암호* 은 **sysname**, 기본값은 없습니다. *암호* ODBC를 사용 하 여 난독 처리 될 **암호화** 함수입니다. 사용 하는 경우는 **암호화** 함수를 배치 하 여 암호를 유니코드 문자열로 변환 해야 **N** 첫 번째 따옴표 앞입니다.  
  
 암호화 옵션을 사용 하는 연결에서 지원 되지 않습니다 **SqlClient**합니다.  
  
> [!IMPORTANT]  
>  ODBC **암호화** 함수 암호화를 제공 하지 않습니다. 이 함수를 사용해서는 네트워크로 전송되는 암호를 보호할 수 없습니다. 이 정보가 네트워크를 통해 전송되는 경우 SSL이나 IPSec을 사용하십시오.  
  
 **@encrypt'없음' =**  
 난독 처리가 사용되지 않도록 지정합니다. 암호는 일반 텍스트로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 전달됩니다. 기본값입니다.  
  
 **@encrypt'odbc' =**  
 ODBC를 사용 하 여 암호 ODBC는 난독 처리를 지정 **암호화** 암호를 보내기 전에 함수는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]합니다. 이 값은 ODBC 클라이언트 또는 SQL Server용 OLE DB 공급자를 사용하는 경우에만 지정할 수 있습니다.  
  
 [  **@fCreateCookie =** ] **true** | **false**  
 쿠키를 만들지 여부를 지정합니다. **true** 1로 암시적으로 변환 됩니다. **false** 암시적으로 0으로 변환 됩니다.  
  
 [  **@cookie =** ]  **@cookie 출력**  
 쿠키를 포함할 출력 매개 변수를 지정합니다. 경우에 쿠키는 생성의 값  **@fCreateCookie**  은 **true**합니다. **varbinary (8000)**  
  
> [!NOTE]  
>  현재 **sp_setapprole** 에 대한 쿠키 **OUTPUT** 매개 변수는 정확한 최대 길이인 **varbinary(8000)** 로 정의되어 있습니다. 그러나 현재 구현은 **varbinary(50)**입니다. 응용 프로그램은 계속해서 **varbinary(8000)** 를 예약하여 후속 릴리스에서 쿠키 반환 크기가 늘어날 경우에도 응용 프로그램이 제대로 작동할 수 있도록 해야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 및 1(실패)  
  
## <a name="remarks"></a>주의  
 응용 프로그램 역할이 활성화에 사용 하 여 **sp_setapprole**를 활성 상태로 사용자는 서버에서 연결을 끊습니다 또는 실행 될 때까지 **sp_unsetapprole**합니다. **sp_setapprole** 직접만 실행할 수 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문. **sp_setapprole** 다른 저장 프로시저 또는 사용자 정의 트랜잭션 내에서 실행할 수 없습니다.  
  
 응용 프로그램 역할의 개요를 참조 하십시오. [응용 프로그램 역할](../../relational-databases/security/authentication-access/application-roles.md)합니다.  
  
> [!IMPORTANT]  
>  응용 프로그램 역할 암호가 네트워크를 통해 전송되는 경우 이 암호를 보호하려면 응용 프로그램 역할을 사용할 때 항상 암호화된 연결을 사용해야 합니다.  
>   
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] ODBC **암호화** 옵션에서 지원 하지 않는 **SqlClient**합니다. 자격 증명을 저장해야 할 경우에는 crypto API 함수를 사용하여 암호화합니다. 매개 변수 *암호* 는 단방향 해시로 저장 됩니다. 이전 버전과의 호환성을 유지 하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 암호 복잡성 정책에 의해 적용 되지 **sp_addapprole**합니다. 암호 복잡성 정책의 적용 하려면 사용 하 여 [CREATE APPLICATION ROLE](../../t-sql/statements/create-application-role-transact-sql.md)합니다.  
  
## <a name="permissions"></a>Permissions  
 멤버 자격이 필요 **공용** 및 역할에 대 한 암호를 알고 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-activating-an-application-role-without-the-encrypt-option"></a>1. 암호화 옵션을 사용하지 않고 응용 프로그램 역할 활성화  
 다음 예에서는 현재 사용자가 사용하는 응용 프로그램에 대해 특별히 지정한 사용 권한을 부여하도록 만든 일반 텍스트 암호인 `SalesAppRole`를 사용하여 `AsDeF00MbXX`이라는 응용 프로그램 역할을 활성화합니다.  
  
```  
EXEC sp_setapprole 'SalesApprole', 'AsDeF00MbXX';  
GO  
```  
  
### <a name="b-activating-an-application-role-with-a-cookie-and-then-reverting-to-the-original-context"></a>2. 쿠키를 사용하여 응용 프로그램 역할을 활성화한 다음 원래 컨텍스트로 되돌리기  
 다음 예에서는 `Sales11` 암호로 `fdsd896#gfdbfdkjgh700mM` 응용 프로그램 역할을 활성화하고 쿠키를 만듭니다. 다음 예에서는 현재 사용자의 이름을 반환한 다음 `sp_unsetapprole`을 실행하여 원래 컨텍스트로 되돌아갑니다.  
  
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
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [보안 저장 프로시저 &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [APPLICATION role&#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [DROP APPLICATION role&#40; Transact SQL &#41;](../../t-sql/statements/drop-application-role-transact-sql.md)   
 [sp_unsetapprole &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-unsetapprole-transact-sql.md)  
  
  
