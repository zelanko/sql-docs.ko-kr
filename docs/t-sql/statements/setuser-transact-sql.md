---
title: SETUSER(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SETUSER_TSQL
- SETUSER
dev_langs:
- TSQL
helpviewer_keywords:
- delegation [SQL Server]
- impersonation [SQL Server]
- SETUSER statement
- user impersonation [SQL Server]
ms.assetid: 7acfac5c-9ad6-4226-b874-7add36c4ea43
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 78e081b5f684751e23efab27acac38e5413f9845
ms.sourcegitcommit: edba1c570d4d8832502135bef093aac07e156c95
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/20/2020
ms.locfileid: "86483902"
---
# <a name="setuser-transact-sql"></a>SETUSER(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **sysadmin** 고정 서버 역할 또는 데이터베이스 소유자가 다른 사용자로 가장할 수 있도록 합니다.  
  
> [!IMPORTANT]  
>  SETUSER는 이전 버전과의 호환성을 위해 포함되었습니다. SETUSER는 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 릴리스에서 지원되지 않을 수 있으므로 대신 [EXECUTE AS](../../t-sql/statements/execute-as-transact-sql.md)를 사용하는 것이 좋습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
  
SETUSER [ 'username' [ WITH NORESET ] ]   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 **'** *username* **'**  
 가장된 현재 데이터베이스 내의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Windows 사용자 이름입니다. *username*을 지정하지 않으면 사용자 ID를 시스템 관리자 또는 사용자를 가장한 데이터베이스 소유자의 원래 ID로 다시 설정합니다.  
  
 WITH NORESET  
 *username*을 지정하지 않은 이후의 SETUSER 문이 사용자 ID를 시스템 관리자 또는 데이터베이스 소유자로 다시 설정하지 않도록 지정합니다.  
  
## <a name="remarks"></a>설명  
 **sysadmin** 고정 서버 역할 또는 데이터베이스 소유자 고정 데이터베이스 역할의 멤버는 SETUSER를 사용하여 다른 사용자로 가장하고, 해당 사용자의 사용 권한을 테스트할 수 있습니다. db_owner 고정 데이터베이스 역할의 멤버 자격으로는 충분하지 않습니다.  
  
 SETUSER는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자에만 사용하세요. Windows 사용자에는 SETUSER가 지원되지 않습니다. 다른 사용자의 ID를 가장하기 위해 SETUSER를 사용할 때 가장한 사용자가 만든 개체는 가장된 사용자가 소유합니다. 예를 들어 데이터베이스 소유자가 **Margaret**라는 사용자로 가장하여 **orders**라는 테이블을 만들면 **orders** 테이블의 소유자는 데이터베이스 소유자가 아니라 **Margaret**가 됩니다.  
  
 SETUSER는 다른 SETUSER 문을 지정할 때까지 또는 현재 데이터베이스가 USE 문을 통해 변경될 때까지 유효합니다.  
  
> [!NOTE]  
>  SETUSER WITH NORESET을 사용한 경우, 데이터베이스 소유자 또는 시스템 관리자는 로그오프한 후 다시 로그인해야 원래의 권한을 다시 얻을 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 **sysadmin** 고정 서버 역할의 멤버이거나 데이터베이스의 소유자여야 합니다. **db_owner** 고정 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 데이터베이스 소유자가 다른 소유자 ID로 가장하는 방법을 보여 줍니다. 사용자 `mary`가 `computer_types`라는 테이블을 만듭니다. 데이터베이스 소유자는 SETUSER를 사용하여 `mary`로 가장한 다음 사용자 `joe`에게 `computer_types` 테이블에 대한 액세스 권한을 부여하고 다시 원래 ID로 돌아옵니다.  
  
```sql
SETUSER 'mary';  
GO  
GRANT SELECT ON computer_types TO joe;  
GO  
--To revert to the original user  
SETUSER;  
```  
  
## <a name="see-also"></a>참고 항목  
 [DENY&#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [GRANT&#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE&#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [USE&#40;Transact-SQL&#41;](../../t-sql/language-elements/use-transact-sql.md)  
  
  
