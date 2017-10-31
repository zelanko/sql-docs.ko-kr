---
title: ALTER CRYPTOGRAPHIC PROVIDER (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 04/20/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_CRYPTOGRAPHIC_PROVIDER_TSQL
- ALTER CRYPTOGRAPHIC PROVIDER
- ALTER_CRYPTOGRAPHIC_TSQL
- ALTER CRYPTOGRAPHIC
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER CRYPTOGRAPHIC PROVIDER
ms.assetid: 876b6348-fb29-49e1-befc-4217979f6416
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b1579fb75de53747a26e647f69c7fc70346738fa
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="alter-cryptographic-provider-transact-sql"></a>ALTER CRYPTOGRAPHIC PROVIDER(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내 암호화 공급자인 EKM(확장 가능 키 관리) 공급자를 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
ALTER CRYPTOGRAPHIC PROVIDER provider_name   
    [ FROM FILE = path_of_DLL ]  
    ENABLE | DISABLE  
```  
  
## <a name="arguments"></a>인수  
 *provider_name*  
 EKM(확장 가능 키 관리) 공급자의 이름입니다.  
  
 *Path_of_DLL*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] EKM(확장 가능 키 관리) 인터페이스를 구현하는 .dll 파일의 경로입니다.  
  
 ENABLE | DISABLE  
 공급자를 설정하거나 해제합니다.  
  
## <a name="remarks"></a>주의  
 공급자 변경 시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 EKM(확장 가능 키 관리)을 구현하는 데 사용되는 .dll 파일도 변경하려면 ALTER CRYPTOGRAPHIC PROVIDER 문을 사용해야 합니다.  
  
 ALTER CRYPTOGRAPHIC PROVIDER 문을 통해 .dll 파일 경로가 업데이트되면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 다음 동작을 수행합니다.  
-   공급자를 해제합니다.  
-   DLL 서명을 확인하고 .dll 파일의 GUID가 카탈로그에 기록된 것과 같은지 확인합니다.  
-   카탈로그의 DLL 버전을 업데이트합니다.  
  

EKM 공급자가 DISABLE로 설정된 경우 새 연결에서 암호화 문으로 공급자를 사용하려는 모든 시도는 실패하게 됩니다.  
  
공급자를 해제하려면 공급자를 사용하는 모든 세션을 종료해야 합니다.  
  
EKM 공급자 dll이 필요한 메서드를 모두 구현하지 않으면 ALTER CRYPTOGRAPHIC PROVIDER가 다음과 같은 오류 33085를 반환할 수 있습니다.  
  
 `One or more methods cannot be found in cryptographic provider library '%.*ls'.`  
  
EKM 공급자 dll을 만드는 데 사용한 헤더 파일이 오래된 경우에는 ALTER CRYPTOGRAPHIC PROVIDER가 다음과 같은 오류 33032를 반환할 수 있습니다.  
  
 `SQL Crypto API version '%02d.%02d' implemented by provider is not supported. Supported version is '%02d.%02d'.`  
  
## <a name="permissions"></a>Permissions  
 암호화 공급자에 대한 CONTROL 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 라는 암호화 공급자 변경 `SecurityProvider` 에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)],.dll 파일의 최신 버전으로 합니다. 새 버전의 이름은 `c:\SecurityProvider\SecurityProvider_v2.dll`이며 서버에 설치됩니다. 공급자의 인증서는 서버에 설치되어야 합니다.  
  
1. 업그레이드를 수행 하는 공급자를 사용 하지 않도록 설정 합니다. 이 암호화 열려 있는 모든 세션을 종료 합니다.  
```  
ALTER CRYPTOGRAPHIC PROVIDER SecurityProvider   
DISABLE;  
GO  
```  

2. 공급자의.dll 파일을 업그레이드 합니다. GUID와 이전 버전에서 동일 해야 하지만 버전 다를 수 있습니다.  
```  
ALTER CRYPTOGRAPHIC PROVIDER SecurityProvider  
FROM FILE = 'c:\SecurityProvider\SecurityProvider_v2.dll';  
GO  
```  

3. 업그레이드 된 공급자를 사용 하도록 설정 합니다.   
```  
ALTER CRYPTOGRAPHIC PROVIDER SecurityProvider   
ENABLE;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [확장 가능 키 관리 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/create-cryptographic-provider-transact-sql.md)   
 [DROP CRYPTOGRAPHIC PROVIDER&#40;Transact-SQL&#41;](../../t-sql/statements/drop-cryptographic-provider-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [Azure Key Vault를 사용한 확장 가능 키 관리&#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
  

