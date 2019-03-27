---
title: sp_addapprole (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addapprole_TSQL
- sp_addapprole
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addapprole
ms.assetid: 24200295-9a54-4cab-9922-fb2e88632721
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 11d0115c1f8bea82385d7c69365489a93351a5c5
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58493135"
---
# <a name="spaddapprole-transact-sql"></a>sp_addapprole(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 데이터베이스에 응용 프로그램 역할을 추가합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 사용 하 여 [CREATE APPLICATION ROLE](../../t-sql/statements/create-application-role-transact-sql.md) 대신 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_addapprole [ @rolename = ] 'role' , [ @password = ] 'password'  
```  
  
## <a name="arguments"></a>인수  
`[ @rolename = ] 'role'` 새 응용 프로그램 역할의 이름이입니다. *역할* 됩니다 **sysname**, 기본값은 없습니다. *역할* 유효한 식별자 여야 하며 현재 데이터베이스에 이미 존재할 수 없습니다.  
  
 응용 프로그램 역할 이름은 문자, 기호 및 숫자를 비롯하여 1자에서 128자까지의 문자를 포함할 수 있습니다. 역할 이름은 백슬래시를 포함할 수 없습니다 (\\) NULL 또는 빈 문자열 (")도 있습니다.  
  
`[ @password = ] 'password'` 응용 프로그램 역할을 활성화 하는 데 필요한 암호가입니다. *암호* 됩니다 **sysname**, 기본값은 없습니다. *암호* NULL 일 수 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>Remarks  
 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용자 및 역할은 스키마와 완전히 구분되지 않았습니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]부터 스키마는 역할과 완전히 구분됩니다. 이 새 아키텍처는 CREATE APPLICATION ROLE의 동작에 반영되었습니다. 이 문은 대체 **sp_addapprole**합니다.  
  
 이전 버전의 이전 버전과 호환성을 유지 하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], **sp_addapprole** 다음을 수행 합니다.  
  
-   응용 프로그램 역할과 이름이 같은 스키마가 아직 없으면 해당 스키마가 생성됩니다. 새 스키마는 응용 프로그램 역할이 소유하고 응용 프로그램 역할의 기본 스키마가 됩니다.  
  
-   응용 프로그램 역할과 이름이 같은 스키마가 이미 있으면 프로시저가 실패합니다.  
  
-   암호 복잡성을 확인 하지 않습니다 **sp_addapprole**합니다. CREATE APPLICATION ROLE에서 검사합니다.  
  
 매개 변수 *암호* 단방향 해시로 저장 됩니다.  
  
 합니다 **sp_addapprole** 사용자 정의 트랜잭션 내에서 저장된 프로시저를 실행할 수 없습니다.  
  
> [!IMPORTANT]  
>  Microsoft ODBC **암호화할** 옵션에서 지원 되지 않습니다 **SqlClient**합니다. 가능한 경우 런타임 시 사용자에게 응용 프로그램 역할 자격 증명을 입력하라는 메시지를 표시할 수도 있습니다. 자격 증명은 파일에 저장하지 않는 것이 좋습니다. 자격 증명을 유지해야 할 경우에는 CryptoAPI 함수를 사용하여 암호화합니다.  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스에 대한 ALTER ANY APPLICATION ROLE 권한이 필요합니다. 새 역할과 이름 및 소유자가 같은 스키마가 아직 없으면 데이터베이스에 대한 CREATE SCHEMA 권한도 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 새 응용 프로그램 역할 추가 `SalesApp` 암호로 `x97898jLJfcooFUYLKm387gf3` 현재 데이터베이스에 있습니다.  
  
```  
EXEC sp_addapprole 'SalesApp', 'x97898jLJfcooFUYLKm387gf3' ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md)  
  
  
