---
title: sp_dropuser (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dropuser
- sp_dropuser_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropuser
ms.assetid: e28f18f9-7ecf-4568-89f4-fe5c520df386
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a231ed2809f387f58ccedef9acb8555a6569e992
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85772203"
---
# <a name="sp_dropuser-transact-sql"></a>sp_dropuser(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  현재 데이터베이스에서 데이터베이스 사용자를 제거합니다. **sp_dropuser** 는 이전 버전의와의 호환성을 제공 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]대신 [DROP USER](../../t-sql/statements/drop-user-transact-sql.md) 를 사용 해야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_dropuser [ @name_in_db = ] 'user'  
```  
  
## <a name="arguments"></a>인수  
`[ @name_in_db = ] 'user'`제거할 사용자의 이름입니다. *사용자* 는 **sysname**이며 기본값은 없습니다. *사용자가* 현재 데이터베이스에 있어야 합니다. Windows 로그인을 지정하는 경우에는 데이터베이스에서 알 수 있는 로그인 이름을 사용합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
 **sp_dropuser** **sp_revokedbaccess** 를 실행 하 여 현재 데이터베이스에서 사용자를 제거 합니다.  
  
 **Sp_helpuser** 를 사용 하 여 현재 데이터베이스에서 제거할 수 있는 사용자 이름 목록을 표시 합니다.  
  
 데이터베이스 사용자가 제거되면 해당 사용자의 모든 별칭도 함께 제거됩니다. 사용자가 사용자와 동일한 이름의 빈 스키마를 소유하는 경우 해당 스키마는 삭제됩니다. 데이터베이스 내의 다른 보안 개체를 소유하는 사용자는 삭제되지 않습니다. 이러한 사용자를 삭제하려면 먼저 개체의 소유권을 다른 보안 주체로 이전해야 합니다. 자세한 내용은 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)을 참조하세요. 데이터베이스 사용자를 제거하면 사용자와 연관된 사용 권한이 자동으로 제거되며 이 사용자가 속해 있던 모든 데이터베이스 역할에서 해당 사용자가 제거됩니다.  
  
 **sp_dropuser** 은 **master** 또는 **tempdb** 데이터베이스에서**dbo**(데이터베이스 소유자) **INFORMATION_SCHEMA** 사용자 또는 **게스트** 사용자를 제거 하는 데 사용할 수 없습니다. 시스템을 사용 하지 않는 데이터베이스에서 `EXEC sp_dropuser 'guest'` 는 사용자 **게스트**의 CONNECT 권한을 취소 합니다. 그러나 사용자 자체는 삭제되지 않습니다.  
  
 사용자 정의 트랜잭션 내에서는 **sp_dropuser** 을 실행할 수 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스에 대한 ALTER ANY USER 권한이 필요합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 현재 데이터베이스에서 `Albert` 사용자를 제거합니다.  
  
```  
EXEC sp_dropuser 'Albert';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;보안 저장 프로시저](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;sp_grantdbaccess &#40;](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [DROP USER &#40;Transact-sql&#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [Transact-sql&#41;sp_revokedbaccess &#40;](../../relational-databases/system-stored-procedures/sp-revokedbaccess-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
