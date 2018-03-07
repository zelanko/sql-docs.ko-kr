---
title: SETUSER (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a511e0337201c9b4501b5274fa8270fbebf7da50
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="setuser-transact-sql"></a>SETUSER(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  멤버 수는 **sysadmin** 고정 서버 역할 또는 다른 사용자를 가장 하는 데이터베이스의 소유자입니다.  
  
> [!IMPORTANT]  
>  SETUSER는 이전 버전과의 호환성을 위해 포함되었습니다. SETUSER는 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 릴리스에서 지원되지 않을 수 있으므로 사용 하는 것이 좋습니다 [EXECUTE AS](../../t-sql/statements/execute-as-transact-sql.md) 대신 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
SETUSER [ 'username' [ WITH NORESET ] ]   
```  
  
## <a name="arguments"></a>인수  
 **'** *username* **'**  
 가장된 현재 데이터베이스 내의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Windows 사용자 이름입니다. 때 *username* 를 지정 하지 않으면 시스템 관리자 또는 사용자를 가장 하는 데이터베이스 소유자의 원래 id를 다시 설정 합니다.  
  
 WITH NORESET  
 다음 SETUSER 문이 (지정 하지 않은 *username*) 사용자 id 시스템 관리자나 데이터베이스 소유자를 다시 설정 해야 합니다.  
  
## <a name="remarks"></a>주의  
 SETUSER의 멤버에서 사용할 수는 **sysadmin** 고정 서버 역할 또는 다른 사용자의 사용 권한을 테스트 하려면 다른 사용자의 id를 채택 하는 데이터베이스의 소유자입니다. Db_owner 고정 데이터베이스 역할의에서 멤버 자격이 충분 하지 않습니다.  
  
 SETUSER는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자에만 사용하세요. Windows 사용자에는 SETUSER가 지원되지 않습니다. 다른 사용자의 ID를 가장하기 위해 SETUSER를 사용할 때 가장한 사용자가 만든 개체는 가장된 사용자가 소유합니다. 예를 들어, 데이터베이스 소유자 사용자의 id를 가장할 **Margaret** 라는 테이블을 만들고 **orders**, **orders** 테이블을 소유 **Margaret** , 시스템 관리자가 아닙니다.  
  
 SETUSER는 다른 SETUSER 문을 지정할 때까지 또는 현재 데이터베이스가 USE 문을 통해 변경될 때까지 유효합니다.  
  
> [!NOTE]  
>  SETUSER WITH NORESET을 사용한 경우, 데이터베이스 소유자 또는 시스템 관리자는 로그오프한 후 다시 로그인해야 원래의 권한을 다시 얻을 수 있습니다.  
  
## <a name="permissions"></a>Permissions  
 멤버 자격이 필요는 **sysadmin** 고정 서버 역할 또는 데이터베이스의 소유자 여야 합니다. 멤버 자격이 **db_owner** 고정된 데이터베이스 역할이 충분 한지 않습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 데이터베이스 소유자가 다른 소유자 ID로 가장하는 방법을 보여 줍니다. 사용자 `mary`가 `computer_types`라는 테이블을 만듭니다. 데이터베이스 소유자는 SETUSER를 사용하여 `mary`로 가장한 다음 사용자 `joe`에게 `computer_types` 테이블에 대한 액세스 권한을 부여하고 다시 원래 ID로 돌아옵니다.  
  
```  
SETUSER 'mary';  
GO  
GRANT SELECT ON computer_types TO joe;  
GO  
--To revert to the original user  
SETUSER;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [DENY&#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [GRANT&#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE&#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [USE&#40;Transact-SQL&#41;](../../t-sql/language-elements/use-transact-sql.md)  
  
  
