---
title: CREATE DATABASE SCOPED CREDENTIAL(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/25/2019
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DATABASE SCOPED CREDENTIAL
- DATABASE_SCOPED_CREDENTIAL_TSQL
- SCOPED_TSQL
- CREATE_DATABASE_SCOPED_CREDENTIAL
- CREATE_DATABASE_SCOPED_CREDENTIAL_TSQL
- SCOPED_CREDENTIAL_TSQL
- SCOPED_CREDENTIAL
helpviewer_keywords:
- DATABASE SCOPED CREDENTIAL statement
- credentials [SQL Server], DATABASE SCOPED CREDENTIAL statement
ms.assetid: fe830577-11ca-44e5-953b-2d589d54d045
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=aps-pdw-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 233068e84dca3d7d61e10867443cf30bbf942a59
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798356"
---
# <a name="create-database-scoped-credential-transact-sql"></a>CREATE DATABASE SCOPED CREDENTIAL(Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

데이터베이스 자격 증명을 만듭니다. 데이터베이스 자격 증명은 서버 로그인 또는 데이터베이스 사용자에 매핑되지 않습니다. 자격 증명은 데이터베이스가 액세스가 필요한 작업을 수행할 때 언제든 외부 위치에 액세스하기 위해 데이터베이스에서 사용됩니다.

![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>구문

``` 
CREATE DATABASE SCOPED CREDENTIAL credential_name
WITH IDENTITY = 'identity_name'
    [ , SECRET = 'secret' ]

```

## <a name="arguments"></a>인수

*credential_name* 만들려는 데이터베이스 범위 자격 증명의 이름을 지정합니다. *credential_name*은 번호(#) 기호로 시작할 수 없습니다. 시스템 자격 증명은 ##으로 시작합니다.

IDENTITY **=’** _identity\_name_ **’** 서버 외부에 연결할 때 사용할 계정의 이름을 지정합니다. Azure Blob Storage에서 공유 키를 사용하여 파일을 가져오려면 ID 이름이 `SHARED ACCESS SIGNATURE`여야 합니다. SQL DW로 데이터를 로드하기 위해 ID에 모든 유효한 값을 사용할 수 있습니다. 공유 액세스 서명에 대한 자세한 내용은 [SAS(공유 액세스 서명) 사용](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)을 참조하세요.

SECRET **=’** _secret_ **’** 나가는 인증에 필요한 암호를 지정합니다. `SECRET`은 Azure Blob 스토리지에서 파일을 가져오는 데 필요합니다. Azure Blob Storage에서 SQL DW 또는 병렬 데이터 웨어하우스로 로드하려면 Azure Storage Key가 암호여야 합니다.
> [!WARNING]
> SAS 키 값은 '?'(물음표)로 시작될 수 있습니다. SAS 키를 사용할 때는 앞의 '?'를 제거해야 합니다. 그렇지 않으면 작업이 차단될 수 있습니다.

## <a name="remarks"></a>Remarks

데이터베이스 범위 자격 증명은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 외부의 리소스에 연결하는 데 필요한 인증 정보가 포함된 레코드입니다. 대부분의 자격 증명에는 Windows 사용자 및 암호가 들어 있습니다.

데이터베이스 범위 자격 증명을 만들기 전에 자격 증명을 보호하려면 데이터베이스에 마스터 키가 있어야 합니다. 자세한 내용은 [CREATE MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)를 참조하세요.

IDENTITY가 Windows 사용자인 경우 암호는 해당 사용자의 암호일 수 있습니다. 암호는 서비스 마스터 키를 사용하여 암호화됩니다. 서비스 마스터 키가 다시 생성되면 암호가 새 서비스 마스터 키를 사용하여 다시 암호화됩니다.

데이터베이스 범위 자격 증명에 대한 내용은 [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md) 카탈로그 뷰를 참조하세요.

다음은 몇 가지 데이터베이스 범위 자격 증명 애플리케이션입니다.

- [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]는 데이터베이스 범위 자격 증명을 사용하여 PolyBase로 비공개 Azure BLOB 스토리지 또는 Kerberos 보안 Hadoop 클러스터에 액세스합니다. 자세한 내용은 [CREATE EXTERNAL DATA SOURCE(Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md)를 참조하세요.

- [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]는 데이터베이스 범위 자격 증명을 사용하여 PolyBase로 비공개 Azure BLOB 스토리지에 액세스합니다. 자세한 내용은 [CREATE EXTERNAL DATA SOURCE(Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md)를 참조하세요.

- [!INCLUDE[ssSDS](../../includes/sssds-md.md)]는 전역 쿼리 기능에 데이터베이스 범위 자격 증명을 사용합니다. 이것은 다수의 분할된 데이터베이스에서 쿼리를 수행할 수 있는 기능입니다.

- [!INCLUDE[ssSDS](../../includes/sssds-md.md)]는 데이터베이스 범위 자격 증명을 사용하여 확장 이벤트 파일을 Azure BLOB 스토리지에 씁니다.

- [!INCLUDE[ssSDS](../../includes/sssds-md.md)]는 탄력적 풀에 데이터베이스 범위 자격 증명을 사용합니다. 자세한 내용은 [탄력적 데이터베이스로 폭발적인 증가에 대처하기](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/)를 참조하세요.

- [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)와 [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)은 데이터베이스 범위 자격 증명을 사용하여 Azure BLOB 스토리지의 데이터에 액세스합니다. 자세한 내용은 [Azure Blob Storage의 데이터에 대량 액세스 예제](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md)를 참조하세요. 

## <a name="permissions"></a>사용 권한

데이터베이스에 대한 **CONTROL** 권한이 필요합니다.

## <a name="examples"></a>예

### <a name="a-creating-a-database-scoped-credential-for-your-application"></a>1\. 애플리케이션에 대한 데이터베이스 범위 자격 증명 만들기

다음 예에서는 `AppCred`라는 데이터베이스 범위 자격 증명을 만듭니다. 이 데이터베이스 범위 자격 증명에는 Windows 사용자 `Mary5` 및 암호가 들어 있습니다.

```sql
-- Create a db master key if one does not already exist, using your own password.
CREATE MASTER KEY ENCRYPTION BY PASSWORD='<EnterStrongPasswordHere>';

-- Create a database scoped credential.
CREATE DATABASE SCOPED CREDENTIAL AppCred WITH IDENTITY = 'Mary5',
    SECRET = '<EnterStrongPasswordHere>';
```

### <a name="b-creating-a-database-scoped-credential-for-a-shared-access-signature"></a>2\. 공유 액세스 서명을 위한 데이터베이스 범위 자격 증명 만들기

다음 예에서는 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 및 [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)과 같은 대량 작업을 수행할 수 있는 [외부 데이터 원본](../../t-sql/statements/create-external-data-source-transact-sql.md)을 만드는 데 사용할 수 있는 데이터베이스 범위 자격 증명을 만듭니다. 공유 액세스 서명은 SQL Server, APS 또는 SQL DW에서 PolyBase에 사용할 수 없습니다.

```sql
-- Create a db master key if one does not already exist, using your own password.
CREATE MASTER KEY ENCRYPTION BY PASSWORD='<EnterStrongPasswordHere>';

-- Create a database scoped credential.CREATE DATABASE SCOPED CREDENTIAL MyCredentials
WITH IDENTITY = 'SHARED ACCESS SIGNATURE',
SECRET = 'QLYMgmSXMklt%2FI1U6DcVrQixnlU5Sgbtk1qDRakUBGs%3D';
```

### <a name="c-creating-a-database-scoped-credential-for-polybase-connectivity-to-azure-data-lake-store"></a>C. Azure Data Lake Store에 대한 PolyBase 연결을 위한 데이터베이스 범위 자격 증명 만들기

다음 예에서는 Azure SQL Data Warehouse에서 PolyBase에 사용될 수 있는 [외부 데이터 원본](../../t-sql/statements/create-external-data-source-transact-sql.md)을 만드는 데 사용할 수 있는 데이터베이스 범위 자격 증명을 만듭니다.

Azure Data Lake Store는 서비스 간 인증에 Azure Active Directory 애플리케이션을 사용합니다.
데이터베이스 범위 자격 증명을 만들려면 그 전에 [AAD 애플리케이션을 만들고](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory) client_id, OAuth_2.0_Token_EndPoint 및 Key를 문서화하십시오.

```sql
-- Create a db master key if one does not already exist, using your own password.
CREATE MASTER KEY ENCRYPTION BY PASSWORD='<EnterStrongPasswordHere>';

-- Create a database scoped credential.
CREATE DATABASE SCOPED CREDENTIAL ADL_User
WITH
    IDENTITY = '<client_id>@\<OAuth_2.0_Token_EndPoint>'
    SECRET = '<key>'
;
```

## <a name="more-information"></a>자세한 정보

- [자격 증명&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)
- [ALTER DATABASE SCOPED CREDENTIAL&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-credential-transact-sql.md)
- [DROP DATABASE SCOPED CREDENTIAL&#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)
- [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)
- [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)
- [sys.credentials&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
