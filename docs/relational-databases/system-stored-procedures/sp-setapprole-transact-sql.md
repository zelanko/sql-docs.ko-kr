---
title: sp_setapprole (Transact-sql) | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
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

`[ @rolename = ] 'role'`현재 데이터베이스에 정의 된 응용 프로그램 역할의 이름입니다. *role* 은 **sysname**이며 기본값은 없습니다. 현재 데이터베이스에 *역할이* 있어야 합니다.  
  
`[ @password = ] { encrypt N'password' }`응용 프로그램 역할을 활성화 하는 데 필요한 암호입니다. *password* 는 **sysname**이며 기본값은 없습니다. ODBC **encrypt** 함수를 사용 하 여 *암호* 를 난독 처리 할 수 있습니다. **Encrypt** 함수를 사용 하는 경우 첫 번째 따옴표 앞에 **N** 을 추가 하 여 암호를 유니코드 문자열로 변환 해야 합니다.  
  
 **SqlClient**를 사용 하는 연결에서는 encrypt 옵션이 지원 되지 않습니다.  
  
> [!IMPORTANT]  
> ODBC **encrypt** 함수는 암호화를 제공 하지 않습니다. 이 함수를 사용해서는 네트워크로 전송되는 암호를 보호할 수 없습니다. 이 정보가 네트워크를 통해 전송 되는 경우 TLS 또는 IPSec을 사용 합니다.
  
 **@encrypt= ' 없음 '**  
 난독 처리가 사용되지 않도록 지정합니다. 암호는 일반 텍스트로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 전달됩니다. 기본값입니다.  
  
 **@encrypt= ' odbc '**  
 Odbc **암호화** 기능을 사용 하 여에 암호를 보내기 전에 odbc에서 암호를 난독 처리 하도록 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]지정 합니다. 이 값은 ODBC 클라이언트 또는 SQL Server용 OLE DB 공급자를 사용하는 경우에만 지정할 수 있습니다.  
  
`[ @fCreateCookie = ] true | false`쿠키를 만들지 여부를 지정 합니다. **true** 는 암시적으로 1로 변환 됩니다. **false** 는 암시적으로 0으로 변환 됩니다.  
  
`[ @cookie = ] @cookie OUTPUT`쿠키를 포함 하는 출력 매개 변수를 지정 합니다. 쿠키는 ** \@fCreateCookie** 의 값이 **true**인 경우에만 생성 됩니다. **varbinary(8000)**  
  
> [!NOTE]  
> 현재 **sp_setapprole** 에 대한 쿠키 **OUTPUT** 매개 변수는 정확한 최대 길이인 **varbinary(8000)** 로 정의되어 있습니다. 그러나 현재 구현은 **varbinary(50)** 입니다. 애플리케이션은 계속해서 **varbinary(8000)** 를 예약하여 후속 릴리스에서 쿠키 반환 크기가 늘어날 경우에도 애플리케이션이 제대로 작동할 수 있도록 해야 합니다.
  
## <a name="return-code-values"></a>반환 코드 값

 0(성공) 및 1(실패)  
  
## <a name="remarks"></a>설명

 **Sp_setapprole**를 사용 하 여 응용 프로그램 역할을 활성화 한 후에는 사용자가 서버에서 연결을 끊거나 **sp_unsetapprole**를 실행할 때까지 역할은 활성 상태로 유지 됩니다. **sp_setapprole** 는 직접 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문으로만 실행할 수 있습니다. **sp_setapprole** 는 다른 저장 프로시저 또는 사용자 정의 트랜잭션 내에서 실행할 수 없습니다.  
  
 응용 프로그램 역할에 대 한 개요는 [응용 프로그램 역할](../../relational-databases/security/authentication-access/application-roles.md)을 참조 하세요.  
  
> [!IMPORTANT]  
> 네트워크를 통해 전송 될 때 응용 프로그램 역할 암호를 보호 하려면 응용 프로그램 역할을 사용 하도록 설정할 때 항상 암호화 된 연결을 사용 해야 합니다.
> [!INCLUDE[msCoName](../../includes/msconame-md.md)] ODBC **Encrypt** 옵션은 **SqlClient**에서 지원 되지 않습니다. 자격 증명을 저장해야 할 경우에는 crypto API 함수를 사용하여 암호화합니다. 매개 변수 *암호* 는 단방향 해시로 저장 됩니다. 이전 버전의와의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]호환성을 유지 하기 위해 암호 복잡성 정책은 **sp_addapprole**에 의해 적용 되지 않습니다. 암호 복잡성 정책을 적용 하려면 [CREATE APPLICATION ROLE](../../t-sql/statements/create-application-role-transact-sql.md)을 사용 합니다.  
  
## <a name="permissions"></a>사용 권한

**Public** 의 멤버 자격이 필요 하 고 역할에 대 한 암호를 알고 있어야 합니다.  
  
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

 [Transact-sql&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md) [보안 저장 프로시저 &#40;transact-sql&#41;&#40;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md) transact-sql &#40;응용 프로그램 역할을 [만듭니다](../../t-sql/statements/create-application-role-transact-sql.md) . transact-sql&#41;[DROP 응용 프로그램 역할](../../t-sql/statements/drop-application-role-transact-sql.md) &#40;transact-sql [&#41;sp_unsetapprole &#40;](../../relational-databases/system-stored-procedures/sp-unsetapprole-transact-sql.md)&#41;
