---
title: LOGINPROPERTY (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- BadPasswordCount_TSQL
- BadPasswordTime_TSQL
- IsLockedIsMustChange
- PasswordLastSetTime
- LOGINPROPERTY_TSQL
- LockoutTime
- BadPasswordCount
- PasswordHash
- HistoryLengthIsExpired
- LockoutTime_TSQL
- PasswordHash_TSQL
- HistoryLengthIsExpired_TSQL
- PasswordLastSetTime_TSQL
- BadPasswordTime
- IsLockedIsMustChange_TSQL
- LOGINPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- default database
- LOGINPROPERTY function
ms.assetid: b34df777-79b0-49a5-88db-b99998479a5d
caps.latest.revision: 42
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 31cbf502614fb348f35474237009f444ed294384
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="loginproperty-transact-sql"></a>LOGINPROPERTY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  로그인 정책 설정에 대한 정보를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
LOGINPROPERTY ( 'login_name' , 'property_name' )  
```  
  
## <a name="arguments"></a>인수  
 *login_name*  
 로그인 속성 상태가 반환되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 이름입니다.  
  
 *propertyname*  
 반환될 로그인 속성 정보가 포함된 식입니다. *propertyname* 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**BadPasswordCount**|잘못된 암호를 사용하여 연속해서 로그인을 시도한 횟수를 반환합니다.|  
|**BadPasswordTime**|잘못된 암호를 사용하여 마지막으로 로그인을 시도한 시간을 반환합니다.|  
|**DaysUntilExpiration**|암호 만료일까지 남은 일 수를 반환합니다.|  
|**DefaultDatabase**|반환 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 기본 데이터베이스를 메타 데이터에 저장 또는 **마스터** 데이터베이스가 지정 되지 않은 경우. NULL을 반환 이외[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자 (예를 들어 Windows 인증 사용자)을 프로 비전 합니다.|  
|**DefaultLanguage**|메타데이터에 저장된 로그인 기본 언어를 반환합니다. NULL을 반환 이외[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로 비전 된 사용자, 예를 들어 Windows 사용자를 인증 합니다.|  
|**HistoryLength**|암호 정책 적용 메커니즘을 사용하여 로그인에 대해 추적된 암호의 수를 반환합니다. 암호 정책이 적용되지 않을 경우 0이며 암호 정책 적용은 1에서 시작됩니다.|  
|**IsExpired**|로그인이 만료되었는지 여부를 나타납니다.|  
|**IsLocked**|로그인이 잠겼는지 여부를 나타납니다.|  
|**IsMustChange**|로그인이 다음에 연결할 때 해당 암호를 변경해야 하는지 여부를 나타냅니다.|  
|**LockoutTime**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인이 허용되는 로그인 시도 실패 횟수를 초과하여 잠긴 날짜를 반환합니다.|  
|**PasswordHash**|암호의 해시를 반환합니다.|  
|**PasswordLastSetTime**|현재 암호가 설정된 날짜를 반환합니다.|  
|**PasswordHashAlgorithm**|암호를 해시하는 데 사용되는 알고리즘을 반환합니다.|  
  
## <a name="returns"></a>반환 값  
 데이터 형식은 요청된 값에 따라 달라집니다.  
  
 **IsLocked**, **IsExpired**, 및 **IsMustChange** 형식의 **int**합니다.  
  
-   로그인이 지정된 상태에 있으면 1을 반환합니다.  
  
-   로그인이 지정된 상태에 있지 않으면 0을 반환합니다.  
  
 **BadPasswordCount** 및 **HistoryLength** 형식의 **int**합니다.  
  
 **BadPasswordTime**, **LockoutTime**, **PasswordLastSetTime** 형식의 **datetime**합니다.  
  
 **PasswordHash** 유형의 **varbinary**합니다.  
  
 로그인이 올바른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인이 아니면 NULL을 반환합니다.  
  
 **DaysUntilExpiration** 유형의 **int**합니다.  
  
-   로그인이 만료되었거나 쿼리한 날에 만료되는 경우 0입니다.  
  
-   Windows의 로컬 보안 정책으로 인해 암호가 만료되지 않는 경우 -1입니다.  
  
-   CHECK_POLICY 또는 CHECK_EXPIRATION이 로그인에 대해 OFF이거나 운영 체제에서 암호 정책을 지원하지 않는 경우 NULL입니다.  
  
 **PasswordHashAlgorithm** 은 int 형식입니다.  
  
-   0 SQL7.0 해시일 경우  
  
-   sha-1 해시 하는 경우 1  
  
-   2 SHA-2 해시일 경우  
  
-   로그인이 올바른 SQL Server 로그인이 아니면 NULL을 반환합니다.  
  
## <a name="remarks"></a>주의  
 이 기본 제공 함수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 암호 정책 설정에 대한 정보를 반환합니다. 속성 이름 속성의 이름은 대/소문자 구분, 않으므로 **BadPasswordCount** 및 **badpasswordcount** 동일 합니다. 값은 **PasswordHash, PasswordHashAlgorithm**, 및 **PasswordLastSetTime** 속성의 지원 되는 모든 구성에서 사용할 수 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 있지만 다른 속성은만 사용 가능한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 실행 되 고 [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] 고 CHECK_POLICY 및 CHECK_EXPIRATION이 모두 사용 하도록 설정 합니다. 자세한 내용은 [Password Policy](../../relational-databases/security/password-policy.md)을 참조하세요.  
  
## <a name="permissions"></a>Permissions  
 로그인에 대한 VIEW 권한이 필요합니다. 암호 해시를 요청하는 경우 CONTROL SERVER 권한도 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-checking-whether-a-login-must-change-its-password"></a>1. 로그인이 해당 암호를 변경해야 하는지 여부 확인  
 다음 예제에서는 검사 하는지 여부를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 `John3` 다음의 인스턴스로 연결할 때 해당 암호를 변경 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
```  
SELECT LOGINPROPERTY('John3', 'IsMustChange');  
GO  
```  
  
### <a name="b-checking-whether-a-login-is-locked-out"></a>2. 로그인이 잠겼는지 여부 확인  
 다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 `John3`가 잠겼는지 여부를 확인합니다.  
  
```  
SELECT LOGINPROPERTY('John3', 'IsLocked');  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sys.server_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)  
  
  
