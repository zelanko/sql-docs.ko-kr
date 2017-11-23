---
title: CREATE CREDENTIAL (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 01/09/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREDENTIAL_TSQL
- SQL13.SWB.CREDENTIAL.GENERAL.F1
- CREATE CREDENTIAL
- CREATE_CREDENTIAL_TSQL
- CREDENTIAL
dev_langs: TSQL
helpviewer_keywords:
- SECRET clause
- authentication [SQL Server], credentials
- CREATE CREDENTIAL statement
- credentials [SQL Server], CREATE CREDENTIAL statement
ms.assetid: d5e9ae69-41d9-4e46-b13d-404b88a32d9d
caps.latest.revision: "51"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f0e46404d775da09f4aaeb7b9640dd2a35d3cfa2
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="create-credential-transact-sql"></a>CREATE CREDENTIAL(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  서버 수준 자격 증명을 만듭니다. 자격 증명은 SQL Server 외부의 리소스에 연결 하는 데 필요한 인증 정보를 포함 하는 레코드입니다. 대부분의 자격 증명에는 Windows 사용자 및 암호가 들어 있습니다. 예를 들어 일부 위치에 데이터베이스 백업을 저장 하면 해당 위치에 액세스할 수 있는 특별 한 자격 증명을 제공 하도록 SQL Server 필요할 수 있습니다. 자세한 내용은 참조 [자격 증명 (데이터베이스 엔진)](../../relational-databases/security/authentication-access/credentials-database-engine.md)합니다.
  
> [!NOTE]  
>  데이터베이스 수준 사용에 자격 증명 하려면 [데이터베이스 범위 자격 증명 만들기 &#40; Transact SQL &#41; ](../../t-sql/statements/create-database-scoped-credential-transact-sql.md). 서버에서 여러 데이터베이스에 대 한 동일한 자격 증명을 사용 해야 할 때 서버 수준 자격 증명을 사용 합니다. 데이터베이스 범위 자격 증명을 사용 하 여 데이터베이스를 이식 하려면. 데이터베이스를 새 서버로 이동 될 때 데이터베이스 범위 자격 증명 함께 이동 됩니다. 사용 하 여 데이터베이스 범위 자격 증명이 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]합니다.  
  
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
 만들려는 자격 증명의 이름을 지정합니다. *credential_name* 숫자 (#) 기호로 시작할 수 없습니다. 시스템 자격 증명은 ##으로 시작합니다.  이 이름은 컨테이너 경로 일치 해야 하는 공유 액세스 서명 (SAS)를 사용할 때 https로 시작 하며 슬래시를 포함 해서는 안 됩니다. 예 4 아래를 참조 하십시오.  
  
 IDENTITY **='***identity_name***'**  
 서버 외부에 연결할 때 사용할 계정의 이름을 지정합니다. 자격 증명은 사용 하 여 Azure 키 자격 증명 모음에 액세스 하는 경우는 **IDENTITY** 주요 자격 증명 모음 이름입니다. 아래의 예 3을 참조하세요. 자격 증명이 공유 액세스 서명 (SAS)를 사용 하는 경우는 **IDENTITY** 은 *공유 액세스 서명이*합니다. 예 4 아래를 참조 하십시오.  
  
 비밀 **='***비밀***'**  
 나가는 인증에 필요한 암호를 지정합니다.  
  
 Azure 키 자격 증명 모음에 액세스 하려면 자격 증명이 사용 되는 경우는 **비밀** 의 인수 **CREATE CREDENTIAL** 필요는  *\<클라이언트 ID >* (하이픈 없이) 및  *\<비밀 >* 의 **서비스 사용자** 서로 공백 없이 함께 전달할 Azure Active Directory에 있습니다. 아래의 예 3을 참조하세요. 자격 증명에는 공유 액세스 서명을 사용 하는 경우는 **비밀** 는 공유 액세스 서명 토큰입니다. 예 4 아래를 참조 하십시오.  Azure 컨테이너에 저장된 된 액세스 정책 및 공유 액세스 서명을 만드는 방법은 참조 [1 단원: Azure 컨테이너에 저장 된 액세스 정책 및 공유 액세스 서명을 만들고](../../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md)합니다.  
  
 암호화 공급자에 대 한 *cryptographic_provider_name*  
 이름을 지정는 *엔터프라이즈 키 관리 공급자 (EKM)*합니다. 키 관리에 대 한 자세한 내용은 참조 하세요. [확장 가능 키 관리 &#40; Ekm&#41; ](../../relational-databases/security/encryption/extensible-key-management-ekm.md).  
  
## <a name="remarks"></a>주의  

 IDENTITY가 Windows 사용자인 경우 암호는 해당 사용자의 암호일 수 있습니다. 암호는 서비스 마스터 키를 사용하여 암호화됩니다. 서비스 마스터 키가 다시 생성되면 암호가 새 서비스 마스터 키를 사용하여 다시 암호화됩니다.  
  
 자격 증명을 만든 후에 매핑할 수 있습니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용 하 여 로그인 [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md) 또는 [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md)합니다. A [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 자격 증명 하나만 매핑될 수 있지만 여러에 하나의 자격 증명을 매핑할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 합니다. 자세한 내용은 참조 [자격 증명 &#40; 데이터베이스 엔진 &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)합니다. 서버 수준 자격 증명 하지을 데이터베이스 사용자를 로그인에만 매핑할 수 있습니다. 
  
 자격 증명에 대 한 정보에 표시 됩니다는 [sys.credentials](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md) 카탈로그 뷰에 있습니다.  
  
 공급자에 대해 매핑된 로그인 자격 증명이 없으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정에 매핑된 자격 증명이 사용됩니다.  
  
 자격 증명이 고유한 공급자에 대해 사용되는 경우 로그인에 여러 개의 매핑된 자격 증명이 있을 수 있습니다. 로그인별로 각 공급자에 하나의 매핑된 자격 증명만 있어야 합니다. 동일한 자격 증명이 다른 로그인에 매핑될 수 있습니다.  
  
## <a name="permissions"></a>Permissions  
 필요한 **ALTER ANY CREDENTIAL** 권한.  
  
## <a name="examples"></a>예  
  
### <a name="a-basic-example"></a>1. 기본 예  
 다음 예에서는 `AlterEgo`라는 자격 증명을 만듭니다. 이 자격 증명에는 Windows 사용자 `Mary5` 및 암호가 들어 있습니다.  
  
```  
CREATE CREDENTIAL AlterEgo WITH IDENTITY = 'Mary5',   
    SECRET = '<EnterStrongPasswordHere>';  
GO  
```  
  
### <a name="b-creating-a-credential-for-ekm"></a>2. EKM에 대한 자격 증명 만들기  
 다음 예에서는 이전에 EKM 모듈에서 관리 도구의 기본 계정 유형 및 암호를 사용하여 만든 `User1OnEKM`이라는 계정을 사용합니다. **sysadmin** 서버에서 계정에 할당 하 고 EKM 계정에 연결 하는 데 사용 되는 자격 증명을 만듭니다는 `User1` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계정:  
  
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
 다음 예제에서는 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 대 한 자격 증명은 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 사용 하 여 Azure 키 자격 증명 모음에 액세스할 때 사용할는 **Microsoft Azure 키 자격 증명 모음 용 SQL Server 커넥터**합니다. 사용 하 여의 전체 예제는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 커넥터 참조 [확장 가능 키 관리를 사용 하 여 Azure 키 자격 증명 모음 &#40; SQL Server &#41; ](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md).  
  
> [!IMPORTANT]  
>  **CREATE CREDENTIAL** 의 **IDENTITY** 인수에는 키 자격 증명 모음 이름이 필요합니다. **비밀** 의 인수 **CREATE CREDENTIAL** 필요는  *\<클라이언트 ID >* (하이픈 없이) 및  *\<암호 >*  서로 공백 없이 함께 전달할 수 있습니다.  
  
 다음 예제에서 **클라이언트 ID** (`EF5C8E09-4D2A-4A76-9998-D93440D8115D`)는 하이픈이 제거되어 문자열 `EF5C8E094D2A4A769998D93440D8115D` 로 입력되어 있으며 **암호** 는 문자열 *SECRET_DBEngine*으로 표현되었습니다.  
  
```  
USE master;  
CREATE CREDENTIAL Azure_EKM_TDE_cred   
    WITH IDENTITY = 'ContosoKeyVault',   
    SECRET = 'EF5C8E094D2A4A769998D93440D8115DSECRET_DBEngine'   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov ;  
```  
  
 다음 예제에 대 한 변수를 사용 하 여 동일한 자격 증명을 만듭니다는 **클라이언트 ID** 및 **비밀** 다음 서로 연결 되 고 폼을 하는 문자열은 **비밀** 인수입니다. **대체** 함수는 id입니다. 클라이언트에서 하이픈을 제거 하는 데 사용 됩니다  
  
```  
DECLARE @AuthClientId uniqueidentifier = 'EF5C8E09-4D2A-4A76-9998-D93440D8115D';  
DECLARE @AuthClientSecret varchar(200) = 'SECRET_DBEngine';  
DECLARE @pwd varchar(max) = REPLACE(CONVERT(varchar(36), @AuthClientId) , '-', '') + @AuthClientSecret;  
  
EXEC ('CREATE CREDENTIAL Azure_EKM_TDE_cred   
    WITH IDENTITY = 'ContosoKeyVault', SECRET = ''' + @PWD + '''   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov ;');  
```  
  
### <a name="d-creating-a-credential-using-a-sas-token"></a>4. SAS 토큰을 사용 하 여 자격 증명 만들기  
 **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 통해 [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)합니다.  
  
 다음 예제에서는 SAS 토큰을 사용 하 여 공유 액세스 서명 자격 증명을 만듭니다.  Azure 컨테이너에 대해 저장 된 액세스 정책과 공유 액세스 서명을 만들고 공유 액세스 서명을 사용 하 여 자격 증명을 만드는 다음에 대 한 자습서를 참조 하십시오. [자습서: SQL Server 2016으로 Microsoft Azure Blob 저장소 서비스를 사용 하 여 데이터베이스](Tutorial:%20Using%20the%20Microsoft%20Azure%20Blob%20storage%20service%20with%20SQL%20Server%202016%20databases.md)합니다.  
  
> [!IMPORTANT]  
>  **자격 증명 이름** 인수 이름을 컨테이너 경로 일치 해야 https로 시작 하 고 후행 슬래시를 포함 하지 않습니다. **IDENTITY** 인수는 이름에 필요 하지만 *공유 액세스 서명을*합니다. **비밀** 인수 공유 액세스 서명 토큰에 필요 합니다.  
  
```  
USE master  
CREATE CREDENTIAL [https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>] -- this name must match the container path, start with https and must not contain a trailing forward slash.  
   WITH IDENTITY='SHARED ACCESS SIGNATURE' -- this is a mandatory string and do not change it.   
   , SECRET = 'sharedaccesssignature' –- this is the shared access signature token   
GO    
```  
  
## <a name="see-also"></a>관련 항목:  
 [자격 증명 &#40; 데이터베이스 엔진 &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [ALTER CREDENTIAL &#40; Transact SQL &#41;](../../t-sql/statements/alter-credential-transact-sql.md)   
 [DROP CREDENTIAL &#40; Transact SQL &#41;](../../t-sql/statements/drop-credential-transact-sql.md)   
 [DATABASE SCOPED credential&#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [sys.credentials&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)   
 [2 단원: 공유 액세스 서명을 사용 하 여 SQL Server 자격 증명 만들기](../../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)   
 [공유 액세스 서명](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)  
  
  
