---
title: sp_setapprole (거래 -SQL) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 10/12/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_setapprole
- sp_setapprole_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_setapprole
ms.assetid: cf0901c0-5f90-42d4-9d5b-8772c904062d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: b158c4571deadadeaee23ffa6e46eb48a8c8446e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299611"
---
# <a name="sp_setapprole-transact-sql"></a>sp_setapprole(Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  현재 데이터베이스의 애플리케이션 역할과 연관된 사용 권한을 활성화합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  

```sql
sp_setapprole [ @rolename = ] 'role',  
    [ @password = ] { encrypt N'password' }
      |  
        'password' [ , [ @encrypt = ] { 'none' | 'odbc' } ]  
        [ , [ @fCreateCookie = ] true | false ]  
    [ , [ @cookie = ] @cookie OUTPUT ]  
```

## <a name="arguments"></a>인수

`[ @rolename = ] 'role'`현재 데이터베이스에 정의된 응용 프로그램 역할의 이름입니다. *역할은* **sysname입니다.** *역할이* 현재 데이터베이스에 있어야 합니다.  
  
`[ @password = ] { encrypt N'password' }`응용 프로그램 역할을 활성화하는 데 필요한 암호입니다. *암호는* **sysname**, 기본값 없음입니다. *암호는* ODBC **암호화** 기능을 사용하여 난독 처리 될 수 있습니다. **암호화** 함수를 사용하는 경우 첫 번째 따옴표 앞에 **N을** 배치하여 암호를 유니코드 문자열로 변환해야 합니다.  
  
 암호화 옵션은 **SqlClient**를 사용하는 연결에서 지원되지 않습니다.  
  
> [!IMPORTANT]  
> ODBC **암호화** 함수는 암호화를 제공하지 않습니다. 이 함수를 사용해서는 네트워크로 전송되는 암호를 보호할 수 없습니다. 이 정보가 네트워크를 통해 전송되는 경우 TLS 또는 IPSec을 사용합니다.
  
 **@encrypt= '없음'**  
 난독 처리가 사용되지 않도록 지정합니다. 암호는 일반 텍스트로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 전달됩니다. 이것이 기본값입니다.  
  
 **@encrypt= 'odbc'**  
 에 암호를 보내기 전에 ODBC **암호화** 함수를 사용하여 암호를 난독 처리하도록 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]지정합니다. 이 값은 ODBC 클라이언트 또는 SQL Server용 OLE DB 공급자를 사용하는 경우에만 지정할 수 있습니다.  
  
`[ @fCreateCookie = ] true | false`쿠키를 만들지 여부를 지정합니다. **true는** 암시적으로 1로 변환됩니다. **false는** 암시적으로 0으로 변환됩니다.  
  
`[ @cookie = ] @cookie OUTPUT`쿠키를 포함하도록 출력 매개 변수를 지정합니다. 쿠키는 ** \@fCreateCookie의** 값이 **true인**경우에만 생성됩니다. **varbinary(8000)**  
  
> [!NOTE]  
> 현재 **sp_setapprole** 에 대한 쿠키 **OUTPUT** 매개 변수는 정확한 최대 길이인 **varbinary(8000)** 로 정의되어 있습니다. 그러나 현재 구현은 **varbinary(50)** 입니다. 애플리케이션은 계속해서 **varbinary(8000)** 를 예약하여 후속 릴리스에서 쿠키 반환 크기가 늘어날 경우에도 애플리케이션이 제대로 작동할 수 있도록 해야 합니다.
  
## <a name="return-code-values"></a>반환 코드 값

 0(성공) 및 1(실패)  
  
## <a name="remarks"></a>설명

 **sp_setapprole**사용하여 응용 프로그램 역할이 활성화된 후에는 사용자가 서버에서 연결을 끊거나 **sp_unsetapprole**실행할 때까지 역할이 활성 상태로 유지됩니다. **sp_setapprole** 직접 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문으로만 실행할 수 있습니다. **sp_setapprole** 다른 저장 프로시저 내에서 또는 사용자 정의 트랜잭션 내에서 실행할 수 없습니다.  
  
 응용 프로그램 역할에 대한 개요는 [응용 프로그램 역할을](../../relational-databases/security/authentication-access/application-roles.md)참조하십시오.  
  
> [!IMPORTANT]  
> 네트워크를 통해 전송될 때 응용 프로그램 역할 암호를 보호하려면 응용 프로그램 역할을 활성화할 때 항상 암호화된 연결을 사용해야 합니다.
> [!INCLUDE[msCoName](../../includes/msconame-md.md)] ODBC **암호화** 옵션은 **SqlClient**에서 지원되지 않습니다. 자격 증명을 저장해야 할 경우에는 crypto API 함수를 사용하여 암호화합니다. 매개 변수 *암호는* 단방향 해시로 저장됩니다. 이전 버전과의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]호환성을 유지하기 위해 sp_addapprole **.** 암호 복잡성 정책을 적용하려면 [응용 프로그램 역할 만들기를](../../t-sql/statements/create-application-role-transact-sql.md)사용합니다.  
  
## <a name="permissions"></a>사용 권한

역할에 대한 **공개** 멤버 자격 및 암호 에 대한 지식이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-activating-an-application-role-without-the-encrypt-option"></a>A. 암호화 옵션을 사용하지 않고 애플리케이션 역할 활성화

 다음 예에서는 현재 사용자가 사용하는 애플리케이션에 대해 특별히 지정한 사용 권한을 부여하도록 만든 일반 텍스트 암호인 `SalesAppRole`를 사용하여 `AsDeF00MbXX`이라는 애플리케이션 역할을 활성화합니다.

```sql
EXEC sys.sp_setapprole 'SalesApprole', 'AsDeF00MbXX';  
GO
```

### <a name="b-activating-an-application-role-with-a-cookie-and-then-reverting-to-the-original-context"></a>B. 쿠키를 사용하여 애플리케이션 역할을 활성화한 다음 원래 컨텍스트로 되돌리기

 다음 예에서는 `Sales11` 암호로 `fdsd896#gfdbfdkjgh700mM` 애플리케이션 역할을 활성화하고 쿠키를 만듭니다. 다음 예에서는 현재 사용자의 이름을 반환한 다음 `sp_unsetapprole`을 실행하여 원래 컨텍스트로 되돌아갑니다.  

```sql
DECLARE @cookie varbinary(8000);  
EXEC sys.sp_setapprole 'Sales11', 'fdsd896#gfdbfdkjgh700mM'  
    , @fCreateCookie = true, @cookie = @cookie OUTPUT;  
-- The application role is now active.  
SELECT USER_NAME();  
-- This will return the name of the application role, Sales11.  
EXEC sys.sp_unsetapprole @cookie;  
-- The application role is no longer active.  
-- The original context has now been restored.  
GO  
SELECT USER_NAME();  
-- This will return the name of the original user.
GO
```

## <a name="see-also"></a>참고 항목

 [시스템 저장 프로시저 &#40;거래 SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md) 보안 저장 [프로시저 &#40;거래 SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md) 응용 프로그램 역할 만들기 &#40;[트랜스액트 SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md) 드롭 응용 프로그램 역할 &#40;[거래-SQL&#41;sp_unsetapprole](../../t-sql/statements/drop-application-role-transact-sql.md) sp_unsetapprole &#40;[거래-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unsetapprole-transact-sql.md) sp_unsetapprole
