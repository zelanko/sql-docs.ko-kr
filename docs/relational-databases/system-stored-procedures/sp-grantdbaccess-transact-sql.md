---
title: sp_grantdbaccess (Transact-sql) | Microsoft Docs
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
ms.openlocfilehash: 85ab6ead295b4459890a61deccdac3dc2775033a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85646007"
---
# <a name="sp_grantdbaccess-transact-sql"></a>sp_grantdbaccess(Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  현재 데이터베이스에 데이터베이스 사용자를 추가합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]대신 [CREATE USER](../../t-sql/statements/create-user-transact-sql.md) 를 사용 해야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sp_grantdbaccess [ @loginame = ] 'login'  
    [ , [ @name_in_db = ] 'name_in_db' [ OUTPUT ] ]  
```  
  
## <a name="arguments"></a>인수  
`[ @loginame = ] 'login_ '`새 데이터베이스 사용자에 매핑할 Windows 그룹, Windows 로그인 또는 로그인의 이름입니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Windows 그룹 및 windows 로그인의 이름은 *도메인* \\ *로그인*(예: **: london\joeb)**)의 windows 도메인 이름으로 한정 되어야 합니다. 로그인은 데이터베이스의 사용자에 미리 매핑될 수 없습니다. *login* 은 **sysname**이며 기본값은 없습니다.  
  
``[ @name_in_db = ] 'name_in_db' [ OUTPUT]``새 데이터베이스 사용자의 이름입니다. *name_in_db* 는 **SYSNAME**데이터 형식의 OUTPUT 변수 이며 기본값은 NULL입니다. 지정 하지 않으면 *login* 이 사용 됩니다. 값이 NULL 인 OUTPUT 변수로 지정 된 경우 ** \@ name_in_db** 는 *login*으로 설정 됩니다. *name_in_db* 은 (는) 현재 데이터베이스에 없어야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
 **sp_grantdbaccess** 는 추가 옵션을 지 원하는 CREATE USER를 호출 합니다. 데이터베이스 사용자를 만드는 방법에 대 한 자세한 내용은 [CREATE USER &#40;transact-sql&#41;](../../t-sql/statements/create-user-transact-sql.md)를 참조 하세요. 데이터베이스에서 데이터베이스 사용자를 제거 하려면 [DROP user](../../t-sql/statements/drop-user-transact-sql.md)를 사용 합니다.  
  
 사용자 정의 트랜잭션 내에서는 **sp_grantdbaccess** 을 실행할 수 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 **Db_owner** 고정 데이터베이스 역할 또는 **db_accessadmin** 고정 데이터베이스 역할의 멤버 자격이 필요 합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `CREATE USER` 를 사용 하 여 Windows 로그인에 대 한 데이터베이스 사용자를 현재 데이터베이스에 추가 합니다 `Edmonds\LolanSo` . 새 사용자의 이름은 `Lolan`입니다. 데이터베이스 사용자를 만드는 경우 기본적으로 이 방법이 사용됩니다.  
  
```sql
CREATE USER Lolan FOR LOGIN [Edmonds\LolanSo];  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;보안 저장 프로시저](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;사용자 &#40;만들기](../../t-sql/statements/create-user-transact-sql.md)   
 [DROP USER &#40;Transact-sql&#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
