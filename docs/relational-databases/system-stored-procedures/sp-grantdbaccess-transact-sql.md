---
title: sp_grantdbaccess (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_grantdbaccess
- sp_grantdbaccess_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_grantdbaccess
ms.assetid: 3eb09513-03f1-42f8-9917-3a1f3a579bec
ms.author: vanto
author: VanMSFT
manager: craigg
ms.openlocfilehash: 285f1c5f2ab868bbf21db80e68ebbf5d71100f14
ms.sourcegitcommit: 96090bb369ca8aba364c2e7f60b37165e5af28fc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/10/2019
ms.locfileid: "66822616"
---
# <a name="spgrantdbaccess-transact-sql"></a>sp_grantdbaccess(Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 데이터베이스에 데이터베이스 사용자를 추가합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 사용 하 여 [CREATE USER](../../t-sql/statements/create-user-transact-sql.md) 대신 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sp_grantdbaccess [ @loginame = ] 'login'  
    [ , [ @name_in_db = ] 'name_in_db' [ OUTPUT ] ]  
```  
  
## <a name="arguments"></a>인수  
`[ @loginame = ] 'login_ '` Windows 그룹, Windows 로그인의 이름 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 새 데이터베이스 사용자에 매핑할 수에 로그인 합니다. Windows 그룹과 Windows 로그인의 이름은 형식의 Windows 도메인 이름으로 한 정해야 *도메인*\\*로그인*; 예를 들어 **LONDON\Joeb**합니다. 로그인은 데이터베이스의 사용자에 미리 매핑될 수 없습니다. *로그인* 되는 **sysname**, 기본값은 없습니다.  
  
``[ @name_in_db = ] 'name_in_db' [ OUTPUT]`` 새 데이터베이스 사용자에 대 한 이름이입니다. *name_in_db* 데이터 형식의 OUTPUT 변수는 **sysname**, 및 기본값은 NULL입니다. 지정 하지 않으면 *로그인* 사용 됩니다. 값이 NULL 인 OUTPUT 변수로 지정 된 경우 **@name_in_db** 로 설정 되어 *로그인*합니다. *name_in_db* 현재 데이터베이스에 존재 하지 해야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_grantdbaccess** 추가 옵션을 지 원하는 CREATE USER를 호출 합니다. 데이터베이스 사용자를 만드는 방법에 대 한 자세한 내용은 [사용자 만들기 &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)합니다. 사용 하 여 데이터베이스에서 데이터베이스 사용자를 제거할 [DROP USER](../../t-sql/statements/drop-user-transact-sql.md)합니다.  
  
 **sp_grantdbaccess** 사용자 정의 트랜잭션 내에서 실행할 수 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버 자격이 필요 합니다 **db_owner** 고정된 데이터베이스 역할 또는 **db_accessadmin** 고정된 데이터베이스 역할.  
  
## <a name="examples"></a>예  
 다음 예제에서는 `CREATE USER` Windows 로그인에 대 한 데이터베이스 사용자를 추가 하려면 `Edmonds\LolanSo` 현재 데이터베이스에 있습니다. 새 사용자의 이름은 `Lolan`입니다. 데이터베이스 사용자를 만드는 경우 기본적으로 이 방법이 사용됩니다.  
  
```sql
CREATE USER Lolan FOR LOGIN [Edmonds\LolanSo];  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [Security Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE USER&#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [DROP USER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
