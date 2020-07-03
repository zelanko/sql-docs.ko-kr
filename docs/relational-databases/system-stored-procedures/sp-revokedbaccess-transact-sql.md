---
title: sp_revokedbaccess (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_revokedbaccess_TSQL
- sp_revokedbaccess
dev_langs:
- TSQL
helpviewer_keywords:
- sp_revokedbaccess
ms.assetid: c997cfa1-539d-485c-a664-9c6f76bfe0c2
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: cec7eb26b749328d5bbf0f95f74a0de3b0f30a07
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85901355"
---
# <a name="sp_revokedbaccess-transact-sql"></a>sp_revokedbaccess(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  현재 데이터베이스에서 데이터베이스 사용자를 제거합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]대신 [DROP USER](../../t-sql/statements/drop-user-transact-sql.md) 를 사용 해야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_revokedbaccess [ @name_in_db = ] 'name'  
```  
  
## <a name="arguments"></a>인수  
`[ @name_in_db = ] 'name'`제거할 데이터베이스 사용자의 이름입니다. *name* 은 **sysname** 이며 기본값은 없습니다. *이름은* 서버 로그인, windows 로그인 또는 windows 그룹의 이름일 수 있으며 현재 데이터베이스에 있어야 합니다. Windows 로그인 또는 Windows 그룹을 지정하는 경우 데이터베이스를 식별할 이름을 지정합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
 데이터베이스 사용자가 제거되면 해당 사용자에 종속된 사용 권한 및 별칭도 제거됩니다.  
  
 현재 데이터베이스에서 데이터베이스 사용자만 제거할 수 **sp_revokedbaccess** . 현재 데이터베이스의 개체를 소유하는 데이터베이스를 제거하기 전에 개체 소유권을 전송하거나 개체를 데이터베이스에서 삭제해야 합니다. 자세한 내용은 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)을 참조하세요.  
  
 사용자 정의 트랜잭션 내에서는 **sp_revokedbaccess** 을 실행할 수 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스에 대한 ALTER ANY USER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 현재 데이터베이스에서로 매핑된 데이터베이스 사용자를 제거 합니다 `Edmonds\LolanSo` .  
  
```  
EXEC sp_revokedbaccess 'Edmonds\LolanSo';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;보안 저장 프로시저](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;&#40;시스템 저장 프로시저](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [DROP USER &#40;Transact-sql&#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [ALTER AUTHORIZATION&#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)  
  
  
