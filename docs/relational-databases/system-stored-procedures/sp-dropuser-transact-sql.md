---
title: sp_dropuser (TRANSACT-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d96004357962ee822df7458a30d740fc836de658
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62723884"
---
# <a name="spdropuser-transact-sql"></a>sp_dropuser(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 데이터베이스에서 데이터베이스 사용자를 제거합니다. **sp_dropuser** 이전 버전과의 호환성을 제공 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 사용 하 여 [DROP USER](../../t-sql/statements/drop-user-transact-sql.md) 대신 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_dropuser [ @name_in_db = ] 'user'  
```  
  
## <a name="arguments"></a>인수  
`[ @name_in_db = ] 'user'` 제거할 사용자의 이름이입니다. *사용자* 되는 **sysname**, 기본값은 없습니다. *사용자* 현재 데이터베이스에 존재 해야 합니다. Windows 로그인을 지정하는 경우에는 데이터베이스에서 알 수 있는 로그인 이름을 사용합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_dropuser** 실행 **sp_revokedbaccess** 현재 데이터베이스에서 사용자를 제거 합니다.  
  
 사용 하 여 **sp_helpuser** 현재 데이터베이스에서 제거할 수 있는 사용자 이름의 목록을 표시 합니다.  
  
 데이터베이스 사용자가 제거되면 해당 사용자의 모든 별칭도 함께 제거됩니다. 사용자가 사용자와 동일한 이름의 빈 스키마를 소유하는 경우 해당 스키마는 삭제됩니다. 데이터베이스 내의 다른 보안 개체를 소유하는 사용자는 삭제되지 않습니다. 이러한 사용자를 삭제하려면 먼저 개체의 소유권을 다른 보안 주체로 이전해야 합니다. 자세한 내용은 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)을 참조하세요. 데이터베이스 사용자를 제거하면 사용자와 연관된 사용 권한이 자동으로 제거되며 이 사용자가 속해 있던 모든 데이터베이스 역할에서 해당 사용자가 제거됩니다.  
  
 **sp_dropuser** 데이터베이스 소유자를 제거할 수 없습니다 (**dbo**) **INFORMATION_SCHEMA** 사용자와 **게스트** 에서 사용자는 **마스터**  나 **tempdb** 데이터베이스입니다. 시스템 데이터베이스가 아닌 데이터베이스를 `EXEC sp_dropuser 'guest'` 사용자의 CONNECT 권한이 취소 됩니다 **게스트**합니다. 그러나 사용자 자체는 삭제되지 않습니다.  
  
 **sp_dropuser** 사용자 정의 트랜잭션 내에서 실행할 수 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스에 대한 ALTER ANY USER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 현재 데이터베이스에서 `Albert` 사용자를 제거합니다.  
  
```  
EXEC sp_dropuser 'Albert';  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [Security Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_grantdbaccess&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [DROP USER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [sp_revokedbaccess&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokedbaccess-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
