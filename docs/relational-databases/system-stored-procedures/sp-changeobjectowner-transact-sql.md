---
title: sp_changeobjectowner (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_changeobjectowner_TSQL
- sp_changeobjectowner
dev_langs:
- TSQL
helpviewer_keywords:
- sp_changeobjectowner
ms.assetid: 45b3dc1c-1cde-45b7-a248-5195c12973e9
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 6f00b788ecf6b6e4c02d4b8343ba14fa2c345e6b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68056583"
---
# <a name="sp_changeobjectowner-transact-sql"></a>sp_changeobjectowner(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 데이터베이스에 있는 개체의 소유자를 변경합니다.  
  
> [!IMPORTANT]
>  이 저장 프로시저는에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]사용할 수 있는 개체에만 적용 됩니다. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]대신 [ALTER SCHEMA](../../t-sql/statements/alter-schema-transact-sql.md) 또는 [alter authorization](../../t-sql/statements/alter-authorization-transact-sql.md) 을 사용 하십시오. **sp_changeobjectowner** 스키마와 소유자를 모두 변경 합니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 호환성을 유지하기 위해 이 저장 프로시저는 현재 소유자와 새 소유자가 모두 데이터베이스 사용자 이름과 동일한 이름의 스키마를 갖고 있을 경우에만 개체 소유자를 변경합니다.  
> 
> [!IMPORTANT]
>  새로운 사용 권한 요구 사항이 이 저장 프로시저에 추가되었습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_changeobjectowner [ @objname = ] 'object' , [ @newowner = ] 'owner'  
```  
  
## <a name="arguments"></a>인수  
`[ @objname = ] 'object'`현재 데이터베이스에 있는 기존 테이블, 뷰, 사용자 정의 함수 또는 저장 프로시저의 이름입니다. *object* 는 **nvarchar (776)** 이며 기본값은 없습니다. *개체* 는 기존 개체의 소유자를 사용 하 여 _existing_owner_형식으로 정규화 될 수 있습니다 **.** 스키마와 해당 소유자의 이름이 같은 경우 _개체_ 입니다.  
  
`[ @newowner = ] 'owner_ '`개체의 새 소유자가 될 보안 계정의 이름입니다. *owner* 는 **sysname**이며 기본값은 없습니다. *owner* 는 현재 데이터베이스에 대 한 액세스 권한이 있는 유효한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 데이터베이스 사용자, 서버 역할, windows 로그인 또는 windows 그룹 이어야 합니다. 새 소유자가 해당하는 데이터베이스 수준의 보안 주체가 없는 Windows 사용자 또는 Windows 그룹이면 데이터베이스 사용자가 생성됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
 **sp_changeobjectowner** 는 개체에서 기존 사용 권한을 모두 제거 합니다. **Sp_changeobjectowner**를 실행 한 후에도 유지 하려는 사용 권한을 다시 적용 해야 합니다. 따라서 **sp_changeobjectowner**을 실행 하기 전에 기존 권한을 스크립팅 하는 것이 좋습니다. 개체의 소유권이 변경된 후 스크립트를 사용하여 사용 권한을 다시 적용할 수 있습니다. 실행 전에 사용 권한 스크립트 내의 개체 소유자를 변경해야 합니다.  
  
 보안 개체의 소유자를 변경하려면 ALTER AUTHORIZATION을 사용하십시오. 스키마를 변경하려면 ALTER SCHEMA를 사용하십시오.  
  
## <a name="permissions"></a>사용 권한  
 **Db_owner** 고정 데이터베이스 역할의 멤버 자격 또는 **db_ddladmin** 고정 데이터베이스 역할과 **db_securityadmin** 고정 데이터베이스 역할의 멤버 자격과 개체에 대 한 CONTROL 권한도 필요 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `authors` 테이블의 소유자를로 `Corporate\GeorgeW`변경 합니다.  
  
```  
EXEC sp_changeobjectowner 'authors', 'Corporate\GeorgeW';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER SCHEMA &#40;Transact-sql&#41;](../../t-sql/statements/alter-schema-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL &#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-sql&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [Transact-sql&#41;sp_changedbowner &#40;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
