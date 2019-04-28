---
title: sp_grantlogin (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_grantlogin_TSQL
- sp_grantlogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_grantlogin
ms.assetid: 0c873d99-c3bf-4eb1-948b-a46cb235ccd4
ms.author: vanto
manager: craigg
ms.openlocfilehash: def5041286ade754020a5c84e8d2ac91fc79afa3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62796573"
---
# <a name="spgrantlogin-transact-sql"></a>sp_grantlogin(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 만듭니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 사용 하 여 [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md) 대신 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_grantlogin [@loginame=] 'login'  
```  
  
## <a name="arguments"></a>인수  
`[ @loginame = ] 'login'` Windows 사용자 또는 그룹의 이름이입니다. Windows 사용자 또는 그룹을 폼에 있는 Windows 도메인 이름으로 한정 되어야 합니다 *도메인*\\*사용자*; 예를 들어 **London\Joeb**합니다. *로그인* 됩니다 **sysname**, 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_grantlogin** 추가 옵션을 지 원하는 CREATE LOGIN을 호출 합니다. SQL Server 로그인을 만드는 방법에 대 한 정보를 참조 하세요 [CREATE LOGIN &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)  
  
 **sp_grantlogin** 사용자 정의 트랜잭션 내에서 실행할 수 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 서버에 대한 ALTER ANY LOGIN 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 `CREATE LOGIN` 만들려면를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 사용자에 대 한 로그인 `Corporate\BobJ.` 이 것이 좋습니다.  
  
```  
CREATE LOGIN [Corporate\BobJ] FROM WINDOWS;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [Security Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
