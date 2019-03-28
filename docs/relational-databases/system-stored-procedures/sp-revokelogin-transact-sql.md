---
title: sp_revokelogin (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_revokelogin_TSQL
- sp_revokelogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_revokelogin
ms.assetid: cb1ab102-1ae0-4811-9144-9a8121ef2d7e
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 2763b573eff741575c1d496efb0e861472714823
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58533005"
---
# <a name="sprevokelogin-transact-sql"></a>sp_revokelogin(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  로그인 항목을 제거 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 사용자 또는 그룹 CREATE LOGIN을 사용 하 여 만든 **sp_grantlogin**, 또는 **sp_denylogin**합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 사용 하 여 [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md) 대신 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_revokelogin [ @loginame= ] 'login'  
```  
  
## <a name="arguments"></a>인수  
`[ @loginame = ] 'login'` Windows 사용자 또는 그룹의 이름이입니다. *로그인* 됩니다 **sysname**, 기본값은 없습니다. *로그인* 모든 기존 Windows 사용자 이름 또는 형식에서 그룹이 될 수 있습니다 *컴퓨터 이름*\\*사용자나 도메인*\\*사용자*합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_revokelogin** 지정 하는 계정을 사용 하 여 연결을 사용 하지 않도록 설정 합니다 *로그인* 매개 변수입니다. 그러나 Windows 그룹의 멤버 자격을 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 액세스 권한이 부여된 Windows 사용자는 개별 액세스 권한이 취소된 후에도 그룹 멤버 자격으로 계속 연결할 수 있습니다. 마찬가지로, 경우 합니다 *로그인* Windows 그룹의 이름을 지정 하는 매개 변수를 별도로 된 해당 그룹의 구성원의 인스턴스에 대 한 액세스를 부여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결할 수 있습니다.  
  
 예를 들어, 경우 Windows 사용자 **ADVWORKS\john** Windows 그룹의 멤버인 **ADVWORKS\Admins**, 및 **sp_revokelogin** 의 액세스 권한도 해지 `ADVWORKS\john`:  
  
```  
sp_revokelogin [ADVWORKS\john]  
```  
  
 사용자 **ADVWORKS\john** 경우에 연결할 수 있습니다 **ADVWORKS\Admins** 인스턴스에 대 한 액세스를 부여한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 마찬가지로, 경우 Windows 그룹 **ADVWORKS\Admins** 에 대 한 액세스를 취소 하지만 **ADVWORKS\john** 액세스 권한이 부여 됩니다 **ADVWORKS\john** 계속 연결할 수 있습니다.  
  
 사용 하 여 **sp_denylogin** 의 인스턴스에 연결 하는 것을 명시적으로 못하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]해당 Windows 그룹 멤버 자격에 관계 없이 합니다.  
  
 **sp_revokelogin** 사용자 정의 트랜잭션 내에서 실행할 수 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 서버에 대한 ALTER ANY LOGIN 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 Windows 사용자에 대 한 로그인 항목을 제거 `Corporate\MollyA`합니다.  
  
```  
EXEC sp_revokelogin 'Corporate\MollyA';  
```  
  
 또는  
  
```  
EXEC sp_revokelogin [Corporate\MollyA];  
```  
  
## <a name="see-also"></a>관련 항목  
 [Security Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [DROP LOGIN&#40;Transact-SQL&#41;](../../t-sql/statements/drop-login-transact-sql.md)   
 [sp_denylogin&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [sp_droplogin&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [sp_grantlogin&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
