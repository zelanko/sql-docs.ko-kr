---
title: CREATE CREDENTIAL(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CREDENTIAL_TSQL
- SQL13.SWB.CREDENTIAL.GENERAL.F1
- CREATE CREDENTIAL
- CREATE_CREDENTIAL_TSQL
- CREDENTIAL
dev_langs:
- TSQL
helpviewer_keywords:
- SECRET clause
- authentication [SQL Server], credentials
- CREATE CREDENTIAL statement
- credentials [SQL Server], CREATE CREDENTIAL statement
ms.assetid: d5e9ae69-41d9-4e46-b13d-404b88a32d9d
caps.latest.revision: 51
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 73fb92ad30fc8328b96622df828dd668e6e553ba
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38061261"
---
# <a name="create-credential-transact-sql"></a>CREATE CREDENTIAL(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  서버 수준 자격 증명을 만듭니다. 자격 증명은 SQL Server 외부의 리소스에 연결하는 데 필요한 인증 정보가 포함된 레코드입니다. 대부분의 자격 증명에는 Windows 사용자 및 암호가 들어 있습니다. 예를 들어 일부 위치에 데이터베이스 백업을 저장 하면 해당 위치에 액세스할 수 있는 특별 자격 증명을 제공하기 위해 SQL Server를 요청할 수 있습니다. 자세한 내용은 [자격 증명(데이터베이스 엔진)](../../relational-databases/security/authentication-access/credentials-database-engine.md)을 참조하세요.

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]

> [!NOTE]  
>  데이터베이스 수준의 자격 증명을 만들려면 [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)을 사용하세요. 서버에서 여러 데이터베이스에 대한 동일한 자격 증명을 사용해야 할 때 서버 수준의 자격 증명을 사용하세요. 데이터베이스 범위 자격 증명을 사용하여 데이터베이스의 이식성을 더 높게 만드십시오. 데이터베이스를 새 서버로 이동할 때 데이터베이스 범위 자격 증명도 함께 이동됩니다. [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에서 데이터베이스 범위 자격 증명을 사용합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
CREATE CREDENTIAL credential_name   
WITH IDENTITY = 'identity_name'  
    [ , SECRET = 'secret' ]  
        [ FOR CRYPTOGRAPHIC PROVIDER cryptographic_provider_name ]  
```  
  
## <a name="arguments"></a>인수  
 *credential_name*  
 만들려는 자격 증명의 이름을 지정합니다. *credential_name*은 번호(#) 기호로 시작할 수 없습니다. 시스템 자격 증명은 ##으로 시작합니다.  SAS(공유 액세스 서명)를 사용할 때 이 이름은 컨테이너 경로와 일치해야 하며 https로 시작해야 하고 슬래시를 포함하지 말아야 합니다. 아래의 예 4를 참조하십시오.  
  
 IDENTITY **='***identity_name***'**  
 서버 외부에 연결할 때 사용할 계정의 이름을 지정합니다. Azure Key Vault에 액세스하기 위해 자격 증명을 사용하는 경우, **IDENTITY**가 Key Vault의 이름입니다. 아래의 예 3을 참조하세요. 자격 증명이 SAS(공유 액세스 서명)를 사용하는 경우 **IDENTITY**는 *SAS*입니다. 아래의 예 4를 참조하십시오.  
  
 SECRET **='***secret***'**  
 나가는 인증에 필요한 암호를 지정합니다.  
  
 Azure Key Vault에 액세스하기 위해 자격 증명을 사용하는 경우, **CREATE CREDENTIAL**의 **SECRET** 인수에는 사이에 공백 없이 함께 전달할 Azure Active Directory에 포함된 **Service Principal**의 *\<Client ID>*(하이픈 없이) 및 *\<Secret>* 가 필요합니다. 아래의 예 3을 참조하세요. 자격 증명이 SAS(공유 액세스 서명)를 사용하는 경우 **IDENTITY**는 SAS 토큰입니다. 아래의 예 4를 참조하십시오.  Azure 컨테이너에 저장된 액세스 정책 및 공유 액세스 서명을 만드는 방법은 [1 단원: Azure 컨테이너에 저장 된 액세스 정책 및 공유 액세스 서명 만들기](../../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md)를 참조합니다.  
  
 CRYPTOGRAPHIC PROVIDER에 대해서는 *cryptographic_provider_name*  
 *EKM(Enterprise Key Management) 공급자*의 이름을 지정합니다. Key Management에 대한 자세한 내용은 [Extensible Key Management &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)를 참조하세요.  
  
## <a name="remarks"></a>Remarks  

 IDENTITY가 Windows 사용자인 경우 암호는 해당 사용자의 암호일 수 있습니다. 암호는 서비스 마스터 키를 사용하여 암호화됩니다. 서비스 마스터 키가 다시 생성되면 암호가 새 서비스 마스터 키를 사용하여 다시 암호화됩니다.  
  
 자격 증명을 만든 다음에는 [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md) 또는 [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md)을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에 매핑할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인은 단 하나의 자격 증명에만 매핑될 수 있지만 단일 자격 증명은 여러 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에 매핑될 수 있습니다. 자세한 내용은 [자격 증명 &#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)를 참조하세요. 서버 수준 자격 증명은 데이터베이스 사용자가 아닌 로그인에만 매핑할 수 있습니다. 
  
 자격 증명에 대한 정보는 [sys.credentials](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md) 카탈로그 뷰에 표시됩니다.  
  
 공급자에 대해 매핑된 로그인 자격 증명이 없으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정에 매핑된 자격 증명이 사용됩니다.  
  
 자격 증명이 고유한 공급자에 대해 사용되는 경우 로그인에 여러 개의 매핑된 자격 증명이 있을 수 있습니다. 로그인별로 각 공급자에 하나의 매핑된 자격 증명만 있어야 합니다. 동일한 자격 증명이 다른 로그인에 매핑될 수 있습니다.  
  
## <a name="permissions"></a>Permissions  
 **ALTER ANY CREDENTIAL** 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-basic-example"></a>1. 기본 예  
 다음 예에서는 `AlterEgo`라는 자격 증명을 만듭니다. 이 자격 증명에는 Windows 사용자 `Mary5` 및 암호가 들어 있습니다.  
  
```  
CREATE CREDENTIAL AlterEgo WITH IDENTITY = 'Mary5',   
    SECRET = '<EnterStrongPasswordHere>';  
GO  
```  
  
### <a name="b-creating-a-credential-for-ekm"></a>2. EKM에 대한 자격 증명 만들기  
 다음 예에서는 이전에 EKM 모듈에서 관리 도구의 기본 계정 유형 및 암호를 사용하여 만든 `User1OnEKM`이라는 계정을 사용합니다. 서버의 **sysadmin** 계정은 EKM 계정에 연결하는 데 사용되는 자격 증명을 만들고 이를 `User1`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계정에 할당합니다.  
  
```  
CREATE CREDENTIAL CredentialForEKM  
    WITH IDENTITY='User1OnEKM', SECRET='<EnterStrongPasswordHere>'  
    FOR CRYPTOGRAPHIC PROVIDER MyEKMProvider;  
GO  
  
/* Modify the login to assign the cryptographic provider credential */  
ALTER LOGIN Login1  
ADD CREDENTIAL CredentialForEKM;  
  
/* Modify the login to assign a non cryptographic provider credential */   
ALTER LOGIN Login1  
WITH CREDENTIAL = AlterEgo;  
GO  
```  
  
### <a name="c-creating-a-credential-for-ekm-using-the-azure-key-vault"></a>3. Azure Key Vault를 사용하는 EKM에 대한 자격 증명 만들기  
 다음 예제에서는 **Microsoft Azure Key Vault용 SQL Server 커넥터**를 사용하여 Azure Key Vault에 액세스할 때 사용하기 위하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 자격 증명을 만듭니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 커넥터를 사용하는 완전한 예에 대해서는 [Extensible Key Management Using Azure Key Vault &#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)를 참조하세요.  
  
> [!IMPORTANT]  
>  **CREATE CREDENTIAL** 의 **IDENTITY** 인수에는 키 자격 증명 모음 이름이 필요합니다. **CREATE CREDENTIAL**의 **SECRET** 인수에는 사이에 공백 없이 함께 전달할 *\<Client ID>*(하이픈 없이) 및 *\<Secret>* 이 필요합니다.  
  
 다음 예제에서 **클라이언트 ID** (`EF5C8E09-4D2A-4A76-9998-D93440D8115D`)는 하이픈이 제거되어 문자열 `EF5C8E094D2A4A769998D93440D8115D` 로 입력되어 있으며 **암호** 는 문자열 *SECRET_DBEngine*으로 표현되었습니다.  
  
```  
USE master;  
CREATE CREDENTIAL Azure_EKM_TDE_cred   
    WITH IDENTITY = 'ContosoKeyVault',   
    SECRET = 'EF5C8E094D2A4A769998D93440D8115DSECRET_DBEngine'   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov ;  
```  
  
 다음 에제는 **Client ID** 및 **Secret** 문자열에 대한 변수를 사용하여 동일한 자격 증명을 만든 후, **SECRET** 인수를 형성하기 위해 함께 연결합니다. **REPLACE** 함수는 클라이언트 ID로부터 하이픈을 제거하기 위해 사용됩니다.  
  
```  
DECLARE @AuthClientId uniqueidentifier = 'EF5C8E09-4D2A-4A76-9998-D93440D8115D';  
DECLARE @AuthClientSecret varchar(200) = 'SECRET_DBEngine';  
DECLARE @pwd varchar(max) = REPLACE(CONVERT(varchar(36), @AuthClientId) , '-', '') + @AuthClientSecret;  
  
EXEC ('CREATE CREDENTIAL Azure_EKM_TDE_cred   
    WITH IDENTITY = 'ContosoKeyVault', SECRET = ''' + @PWD + '''   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov ;');  
```  
  
### <a name="d-creating-a-credential-using-a-sas-token"></a>4. SAS 토큰을 사용하여 자격 증명 만들기  
 **적용 대상**: [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)을 통한 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]입니다.  
  
 다음 예제에서는 SAS 토큰을 사용하여 공유 액세스 서명 자격 증명을 만듭니다.  Azure 컨테이너에 저장된 액세스 정책과 공유 액세스 서명을 만든 다음, 공유 액세스 서명을 사용하여 자격 증명을 만드는 방법에 대한 자습서는 [자습서: SQL Server 2016 데이터베이스와 함께 Microsoft Azure Blob 저장소 서비스 사용하기](../../relational-databases/tutorial-use-azure-blob-storage-service-with-sql-server-2016.md)를 참조합니다.  
  
> [!IMPORTANT]  
>  **CREDENTIAL NAME** 인수는 이름이 컨테이너 경로와 일치하고 https로 시작하고 후행 슬래시를 포함하지 않을 것을 요구합니다. **IDENTITY** 인수는 이름, *공유 액세스 서명*을 요구합니다. **SECRET** 인수는 공유 액세스 서명 토큰을 요구합니다.  
  
```  
USE master  
CREATE CREDENTIAL [https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>] -- this name must match the container path, start with https and must not contain a trailing forward slash.  
   WITH IDENTITY='SHARED ACCESS SIGNATURE' -- this is a mandatory string and do not change it.   
   , SECRET = 'sharedaccesssignature' –- this is the shared access signature token   
GO    
```  
  
## <a name="see-also"></a>참고 항목  
 [자격 증명&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [ALTER CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-credential-transact-sql.md)   
 [DROP CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-credential-transact-sql.md)   
 [CREATE DATABASE SCOPED CREDENTIAL&#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [sys.credentials&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)   
 [2단원: 공유 액세스 서명을 사용하여 SQL Server 자격 증명 만들기](../../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)   
 [공유 액세스 서명](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)  
  
  
