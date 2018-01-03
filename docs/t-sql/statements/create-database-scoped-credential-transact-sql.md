---
title: "데이터베이스 범위 이름 자격 증명 (Transact SQL) 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 02/27/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: "21"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 6b0cb350ffccb7ad61335de314765f2b85dc0821
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/02/2018
---
# <a name="create-database-scoped-credential-transact-sql"></a>데이터베이스 범위 이름 자격 증명 (Transact SQL) 만들기
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  데이터베이스 자격 증명을 만듭니다. 데이터베이스 자격 증명은 서버 로그인 또는 데이터베이스 사용자에 매핑되지 않습니다. 자격 증명은 데이터베이스에 대 한 액세스가 필요한 작업을 수행 하 고 언제 든 지 외부 위치에 대 한 액세스를 데이터베이스에서 사용 됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
 
CREATE DATABASE SCOPED CREDENTIAL credential_name   
WITH IDENTITY = 'identity_name'  
    [ , SECRET = 'secret' ]  
  
```  
  
## <a name="arguments"></a>인수  
 *credential_name*  
 만들려는 데이터베이스 범위 자격 증명의 이름을 지정 합니다. *credential_name* 숫자 (#) 기호로 시작할 수 없습니다. 시스템 자격 증명은 ##으로 시작합니다.  
  
 IDENTITY **='***identity_name***'**  
 서버 외부에 연결할 때 사용할 계정의 이름을 지정합니다. Id 이름 이어야 합니다는 파일을 Azure Blob 저장소에서 가져오려면 `SHARED ACCESS SIGNATURE`합니다.  공유 액세스 서명에 대 한 자세한 내용은 참조 [를 사용 하 여 공유 액세스 서명 (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)합니다.  
  
 비밀 **='***비밀***'**  
 나가는 인증에 필요한 암호를 지정합니다. `SECRET`Azure Blob 저장소에서 파일을 가져오는 데 필요 합니다.   
>  [!WARNING]
>  SAS 키 값으로 시작는 '?' (물음표)입니다. 앞에 오는 제거 해야 SAS 키를 사용 하는 경우 '?'입니다. 그렇지 않으면 작업을 차단 될 수 있습니다.  
  
## <a name="remarks"></a>주의  
 데이터베이스 범위 자격 증명은 외부의 리소스에 연결 하는 데 필요한 인증 정보를 포함 하는 레코드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 대부분의 자격 증명에는 Windows 사용자 및 암호가 들어 있습니다.  
  
 만드는 데이터베이스 범위 자격 증명, 데이터베이스 마스터 키 자격 증명을 보호 하기 위해 있어야 합니다. 자세한 내용은 [CREATE MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)를 참조하세요.  
  
 IDENTITY가 Windows 사용자인 경우 암호는 해당 사용자의 암호일 수 있습니다. 암호는 서비스 마스터 키를 사용하여 암호화됩니다. 서비스 마스터 키가 다시 생성되면 암호가 새 서비스 마스터 키를 사용하여 다시 암호화됩니다.  
   
 데이터베이스 범위 자격 증명에 대 한 정보에 표시 되는 [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md) 카탈로그 뷰에 있습니다.  
  
 
 Hereare 일부 응용 프로그램의 데이터베이스 범위 자격 증명:  
  
- [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]데이터베이스 범위 자격 증명을 사용 하 여 public이 아닌 Azure blob 저장소 또는 polybase Kerberos 보안 Hadoop 클러스터에 액세스할 수 있습니다. 자세한 내용은 참고 [외부 데이터 원본 만들기 (Transact SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md)합니다.  

- [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]polybase 액세스 public이 아닌 Azure blob 저장소에 데이터베이스 범위 자격 증명을 사용합니다. 자세한 내용은 참고 [외부 데이터 원본 만들기 (Transact SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md)합니다.
  
- [!INCLUDE[ssSDS](../../includes/sssds-md.md)]데이터베이스의 전역 쿼리 기능에 대 한 범위 지정 된 자격 증명을 사용 하 여 합니다. 데이터베이스의 여러 분할 영역 간에 쿼리 하는 기능입니다.  
  
- [!INCLUDE[ssSDS](../../includes/sssds-md.md)]Azure blob 저장소에 확장된 이벤트 파일을 쓸 데이터베이스 범위 자격 증명을 사용 합니다.  
  
- [!INCLUDE[ssSDS](../../includes/sssds-md.md)]데이터베이스 탄력적 풀에 대 한 범위 지정 된 자격 증명을 사용 하 여 합니다. 자세한 내용은 참조 [폭발적 증가 탄력적 데이터베이스도 같은](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/)  

- [대량 삽입](../../t-sql/statements/bulk-insert-transact-sql.md) 및 [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) 사용 하 여 데이터베이스 범위 자격 증명이 Azure blob 저장소에서 데이터에 액세스 합니다. 자세한 내용은 참조 [예의 대량 데이터에에서 액세스를 Azure Blob 저장소](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md)합니다. 
  
## <a name="permissions"></a>Permissions  
 필요한 **제어** 데이터베이스에 대 한 권한이 있습니다.  
  
## <a name="examples"></a>예  
### <a name="a-creating-a-database-scoped-credential-for-your-application"></a>1. 데이터베이스를 만드는 응용 프로그램에 대 한 자격 증명의 범위.
 다음 예에서는 라는 데이터베이스 범위 자격 증명 `AppCred`합니다. Windows 사용자를 포함 하는 데이터베이스 범위 자격 증명 `Mary5` 및 암호.  
  
```sql  
-- Create a db master key if one does not already exist, using your own password.  
CREATE MASTER KEY ENCRYPTION BY PASSWORD='<EnterStrongPasswordHere>';  
  
-- Create a database scoped credential.  
CREATE DATABASE SCOPED CREDENTIAL AppCred WITH IDENTITY = 'Mary5',   
    SECRET = '<EnterStrongPasswordHere>';  
GO  
```  

### <a name="b-creating-a-database-scoped-credential-for-a-shared-access-signature"></a>2. 공유 액세스 서명에 대 한 자격 증명의 범위는 데이터베이스 만들기.   
다음 예제에서는 데이터베이스 범위 자격 증명을 만드는 데 사용할 수는 [외부 데이터 원본](../../t-sql/statements/create-external-data-source-transact-sql.md), 작업을 수행할 수 있는 대량 작업을 같은 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 및 [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md). SQL Server, APS 또는 SQL DW에 PolyBase 사용 하 여 공유 액세스 서명에 사용할 수 없습니다.
```sql
CREATE DATABASE SCOPED CREDENTIAL MyCredentials  
WITH IDENTITY = 'SHARED ACCESS SIGNATURE',
SECRET = 'QLYMgmSXMklt%2FI1U6DcVrQixnlU5Sgbtk1qDRakUBGs%3D';
```
  
### <a name="c-creating-a-database-scoped-credential-for-polybase-connectivity-to-azure-data-lake-store"></a>3. 데이터베이스를 만드는 Azure 데이터 레이크 저장소 PolyBase 연결에 대 한 자격 증명의 범위.  
다음 예제에서는 데이터베이스 범위 자격 증명을 만드는 데 사용할 수는 [외부 데이터 원본](../../t-sql/statements/create-external-data-source-transact-sql.md), Azure SQL 데이터 웨어하우스에 PolyBase에서 사용할 수 있습니다.

Azure 데이터 레이크 저장소 서비스 간 인증에 대 한 Azure Active Directory 응용 프로그램을 사용합니다.
하십시오 [AAD 응용 프로그램을 만들려면](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory) 하 고 데이터베이스 범위 자격 증명을 만들려면 하려고 하기 전에 client_id, OAuth_2.0_Token_EndPoint, 및 키를 문서화 합니다.

```sql
CREATE DATABASE SCOPED CREDENTIAL ADL_User
WITH
    IDENTITY = '<client_id>@\<OAuth_2.0_Token_EndPoint>'
    SECRET = '<key>'
;
```  
  
  
  
## <a name="more-information"></a>자세한 정보  
 [자격 증명 &#40; 데이터베이스 엔진 &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [ALTER DATABASE SCOPED credential&#40; Transact SQL &#41;](../../t-sql/statements/alter-database-scoped-credential-transact-sql.md)   
 [DROP DATABASE SCOPED credential&#40; Transact SQL &#41;](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)   
 [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  
