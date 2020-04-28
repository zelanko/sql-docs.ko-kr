---
title: sp_revokelogin (Transact-sql) | Microsoft Docs
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
ms.openlocfilehash: 95598885a80b1f697f5e1287e22c1048e737ba6b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67944728"
---
# <a name="sp_revokelogin-transact-sql"></a>sp_revokelogin(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  CREATE LOGIN, **sp_grantlogin**또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **sp_denylogin**를 사용 하 여 만든 Windows 사용자 또는 그룹에 대 한 로그인 항목을 제거 합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]대신 [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md) 을 사용 해야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_revokelogin [ @loginame= ] 'login'  
```  
  
## <a name="arguments"></a>인수  
`[ @loginame = ] 'login'`Windows 사용자 또는 그룹의 이름입니다. *login* 은 **sysname**이며 기본값은 없습니다. *로그인* 은 *컴퓨터 이름*\\*사용자 또는 도메인*\\*사용자*형식의 모든 기존 Windows 사용자 이름 또는 그룹 일 수 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
 **sp_revokelogin** 는 *login* 매개 변수로 지정 된 계정을 사용 하 여 연결을 해제 합니다. 그러나 Windows 그룹의 멤버 자격을 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 액세스 권한이 부여된 Windows 사용자는 개별 액세스 권한이 취소된 후에도 그룹 멤버 자격으로 계속 연결할 수 있습니다. 마찬가지로, *로그인* 매개 변수가 Windows 그룹의 이름을 지정 하는 경우 인스턴스에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대 한 액세스 권한이 별도로 부여 된 해당 그룹의 멤버는 계속 연결할 수 있습니다.  
  
 예를 들어 Windows 사용자 **ADVWORKS\john** windows 그룹 **ADVWORKS\Admins**의 구성원이 고 **sp_revokelogin** 에서 액세스를 취소 하는 경우 `ADVWORKS\john`:  
  
```  
sp_revokelogin [ADVWORKS\john]  
```  
  
 **ADVWORKS\Admins** 에 게 인스턴스에 대 한 액세스 권한이 부여 된 경우에도 사용자 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **ADVWORKS\john** 연결 될 수 있습니다. 마찬가지로 Windows 그룹 **ADVWORKS\Admins** 에 대 한 액세스 권한이 해지 되었지만 **ADVWORKS\john** 에 액세스 권한이 부여 된 경우에도 **ADVWORKS\john** 는 계속 연결할 수 있습니다.  
  
 **Sp_denylogin** 를 사용 하 여 Windows 그룹 멤버 자격에 관계 없이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]사용자가 인스턴스에 연결 하지 못하도록 명시적으로 지정할 수 있습니다.  
  
 사용자 정의 트랜잭션 내에서는 **sp_revokelogin** 을 실행할 수 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 서버에 대한 ALTER ANY LOGIN 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 Windows 사용자 `Corporate\MollyA`에 대 한 로그인 항목을 제거 합니다.  
  
```  
EXEC sp_revokelogin 'Corporate\MollyA';  
```  
  
 또는  
  
```  
EXEC sp_revokelogin [Corporate\MollyA];  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;보안 저장 프로시저](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [DROP LOGIN &#40;Transact-sql&#41;](../../t-sql/statements/drop-login-transact-sql.md)   
 [Transact-sql&#41;sp_denylogin &#40;](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [Transact-sql&#41;sp_droplogin &#40;](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [Transact-sql&#41;sp_grantlogin &#40;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
