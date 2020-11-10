---
description: CREATE CRYPTOGRAPHIC PROVIDER(Transact-SQL)
title: CREATE CRYPTOGRAPHIC PROVIDER(Transact-SQL) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE_CRYPTOGRAPHIC_TSQL
- CRYPTOGRAPHIC PROVIDER
- PROVIDER_TSQL
- CREATE CRYPTOGRAPHIC
- CREATE CRYPTOGRAPHIC PROVIDER
- CRYPTOGRAPHIC_PROVIDER_TSQL
- CREATE_CRYPTOGRAPHIC_PROVIDER_TSQL
- PROVIDER
dev_langs:
- TSQL
helpviewer_keywords:
- 33085 (Database Engine error)
- CREATE CRYPTOGRAPHIC PROVIDER statement
- 33032 (Database Engine error)
ms.assetid: 059a39a6-9d32-4d3f-965b-0a1ce75229c7
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 91478060af31e142f94730b9df3c0a3cdf2a24ef
ms.sourcegitcommit: 49ee3d388ddb52ed9cf78d42cff7797ad6d668f2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2020
ms.locfileid: "94384802"
---
# <a name="create-cryptographic-provider-transact-sql"></a>CREATE CRYPTOGRAPHIC PROVIDER(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  EKM(확장 가능 키 관리) 공급자에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내에 암호화 공급자를 만듭니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql  
CREATE CRYPTOGRAPHIC PROVIDER provider_name   
    FROM FILE = path_of_DLL  
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *provider_name*  
 EKM(확장 가능 키 관리) 공급자의 이름입니다.  
  
 *path_of_DLL*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] EKM(확장 가능 키 관리) 인터페이스를 구현하는 .dll의 경로입니다. **Microsoft Azure 주요 자격 증명 모음용 SQL Server 커넥터** 를 사용하는 경우 기본 위치는 **'C:\Program Files\Microsoft SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll'** 입니다.  
  
## <a name="remarks"></a>설명  
 공급자에서 만든 모든 키는 해당 GUID로 공급자를 참조합니다. GUID는 모든 버전의 DLL에 보존됩니다.  
  
 SQLEKM 인터페이스를 구현하는 DLL은 인증서를 사용하여 디지털로 서명해야 합니다. 그러면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 서명을 확인합니다. 여기에는 해당 루트가 Windows 시스템에서 **Trusted Root Cert Authorities** 위치에 설치해야 하는 해당 인증서 체인이 포함됩니다. 서명이 제대로 확인되지 않으면 CREATE CRYPTOGRAPHIC PROVIDER 문이 실패합니다. 인증서 및 인증서 체인에 대한 자세한 내용은 [SQL Server Certificates and Asymmetric Keys](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)를 참조하십시오.  
  
 EKM 공급자 dll이 필요한 메서드를 모두 구현하지 않으면 CREATE CRYPTOGRAPHIC PROVIDER가 다음과 같은 오류 33085를 반환할 수 있습니다.  
  
 `One or more methods cannot be found in cryptographic provider library '%.*ls'.`  
  
 EKM 공급자 dll을 만드는 데 사용한 헤더 파일이 오래된 경우에는 CREATE CRYPTOGRAPHIC PROVIDER가 다음과 같은 오류 33032를 반환할 수 있습니다.  
  
 `SQL Crypto API version '%02d.%02d' implemented by provider is not supported. Supported version is '%02d.%02d'.`  
  
## <a name="permissions"></a>사용 권한  
 CONTROL SERVER 권한 또는 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 .dll 파일로부터 `SecurityProvider`라는 암호화 공급자를 만듭니다. .dll 파일의 이름은 `c:\SecurityProvider\SecurityProvider_v1.dll`이고 이 파일은 서버에 설치됩니다. 먼저 공급자의 인증서가 서버에 설치되어 있어야 합니다.  
  
```sql  
-- Install the provider  
CREATE CRYPTOGRAPHIC PROVIDER SecurityProvider  
    FROM FILE = 'C:\SecurityProvider\SecurityProvider_v1.dll';  
```  
  
## <a name="see-also"></a>참고 항목  
 [확장 가능 키 관리 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [ALTER CRYPTOGRAPHIC PROVIDER&#40;Transact-SQL&#41;](../../t-sql/statements/alter-cryptographic-provider-transact-sql.md)   
 [DROP CRYPTOGRAPHIC PROVIDER&#40;Transact-SQL&#41;](../../t-sql/statements/drop-cryptographic-provider-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [Azure Key Vault를 사용한 확장 가능 키 관리&#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
 [Azure Key Vault를 사용하여 SQL Server TDE 확장 가능 키 관리 설정](../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)  
 [sys.cryptographic_providers](../../relational-databases/system-catalog-views/sys-cryptographic-providers-transact-sql.md)  
 [sys.dm_cryptographic_provider_properties](../../relational-databases/system-dynamic-management-views/sys-dm-cryptographic-provider-properties-transact-sql.md)
  
  
