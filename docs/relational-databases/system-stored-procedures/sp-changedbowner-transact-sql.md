---
title: sp_changedbowner (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_changedbowner
- sp_changedbowner_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_changedbowner
ms.assetid: 516ef311-e83b-45c9-b9cd-0e0641774c04
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 1a38be84e5f1980b680d674e1c04c2ba95d1a537
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47794301"
---
# <a name="spchangedbowner-transact-sql"></a>sp_changedbowner(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 데이터베이스의 소유자를 변경합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 사용 하 여 [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md) 대신 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_changedbowner [ @loginame = ] 'login'  
     [ , [ @map = ] remap_alias_flag ]  
```  
  
## <a name="arguments"></a>인수  
 [ @loginame=] '*로그인*'  
 현재 데이터베이스의 새 소유자의 로그인 ID입니다. *로그인* 됩니다 **sysname**, 기본값은 없습니다. *로그인* 이미 존재 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 또는 Windows 사용자입니다. *로그인* 이미 데이터베이스 내의 기존 사용자 보안 계정을 통해 데이터베이스에 액세스할 수 있는 경우 현재 데이터베이스의 소유자가 될 수 없습니다. 이 문제를 방지하려면 먼저 현재 데이터베이스에서 사용자를 삭제해야 합니다.  
  
 [ @map=] *remap_alias_flag*  
 합니다 *remap_alias_flag* 에서 로그인 별칭이 제거 되었으므로 매개 변수는 사용 되지 않습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 사용 하 여 *remap_alias_flag* 매개 변수는 오류가 발생 하지 않습니다 하지만 아무 효과가 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>Remarks  
 sp_changedbowner를 실행하면 새 소유자가 데이터베이스 내에서 dbo 사용자로 알려집니다. dbo는 기본적으로 데이터베이스에서 모든 작업을 수행할 수 있는 권한을 갖습니다.  
  
 master, model 또는 tempdb 시스템 데이터베이스의 소유자는 변경할 수 없습니다.  
  
 유효한 목록에 표시할 *로그인* sp_helplogins 저장 프로시저를 실행 하는 값입니다.  
  
 만 사용 하 여 sp_changedbowner를 실행 합니다 *로그인* 매개 변수 데이터베이스 소유권이 *로그인*합니다.  
  
 ALTER AUTHORIZATION 문을 사용하여 보안 개체의 소유자를 변경할 수 있습니다. 자세한 내용은 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)을 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스에 대한 TAKE OWNERSHIP 권한이 필요합니다. 새 소유자에 상응하는 사용자가 데이터베이스에 있으면 로그인에 대한 IMPERSONATE 권한이 필요하고, 그렇지 않으면 서버에 대한 CONTROL SERVER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Albert` 로그인을 현재 데이터베이스의 소유자로 만듭니다.  
  
```  
EXEC sp_changedbowner 'Albert';  
```  
  
## <a name="see-also"></a>관련 항목  
 [Security Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [sp_dropalias &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropalias-transact-sql.md)   
 [sp_dropuser&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [sp_helpdb &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdb-transact-sql.md)   
 [sp_helplogins &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helplogins-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
