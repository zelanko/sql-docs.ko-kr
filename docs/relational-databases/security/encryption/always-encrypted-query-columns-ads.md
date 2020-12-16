---
description: Azure Data Studio를 사용하여 Always Encrypted를 이용하는 열 쿼리
title: Azure Data Studio를 사용하여 Always Encrypted를 이용하는 열 쿼리 | Microsoft Docs
ms.custom: ''
ms.date: 5/19/2020
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7ac5e42497a0167a0e935c116a1efd9cc466300c
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97477614"
---
# <a name="query-columns-using-always-encrypted-with-azure-data-studio"></a>Azure Data Studio를 사용하여 Always Encrypted를 이용하는 열 쿼리
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]

이 문서에서는 [Azure Data Studio](../../../azure-data-studio/what-is.md)를 사용하여 [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)로 암호화된 열을 쿼리하는 방법을 설명합니다. Azure Data Studio를 사용하면 다음 작업을 할 수 있습니다.
- 암호화된 열에 저장된 암호 텍스트 값을 검색합니다. 
- 암호화된 열에 저장된 일반 텍스트 값을 검색합니다.  
- 암호화된 열을 대상으로 하는 일반 텍스트 값을 보냅니다(예: `INSERT` 또는 `UPDATE` 문에 포함하거나 `WHERE` 문에서 `SELECT` 절의 조회 매개 변수로). 

## <a name="retrieving-ciphertext-values-stored-in-encrypted-columns"></a>암호화된 열에 저장된 암호 텍스트 값 검색    
이 섹션에서는 암호화된 열에 암호 텍스트로 저장된 데이터를 검색하는 방법을 설명합니다.

### <a name="steps"></a>단계
1. 암호 텍스트 값을 검색하는 `SELECT` 쿼리를 실행할 쿼리 창에 대한 데이터베이스 연결에 Always Encrypted가 사용 안 함으로 설정되어야 합니다. 아래의 [데이터베이스 연결에 Always Encrypted 사용 및 사용 안 함](#enabling-and-disabling-always-encrypted-for-a-database-connection)을 참조하세요.     
1. `SELECT` 쿼리를 실행합니다. 암호화된 열에서 검색된 모든 데이터는 이진(암호화) 값으로 반환됩니다.   

### <a name="example"></a>예제
`SSN` 이 `Patients` 테이블의 암호화된 열이라고 가정할 경우, 아래 표시된 쿼리는 데이터베이스 연결에 Always Encrypted가 사용되지 않는 경우 이진 암호 텍스트 값을 검색합니다.   

![SELECT * FROM [dbo].[Patients] 쿼리 및 이진 암호 텍스트 값으로 표시된 쿼리 결과 스크린샷](../../../relational-databases/security/encryption/media/always-encrypted-ads-query-ciphertext.png)
 
## <a name="retrieving-plaintext-values-stored-in-encrypted-columns"></a>암호화된 열에 저장된 일반 텍스트 값 검색    
이 섹션에서는 암호화된 열에 암호 텍스트로 저장된 데이터를 검색하는 방법을 설명합니다.

### <a name="prerequisites"></a>필수 구성 요소
- Azure Data Studio 버전 17.1 이상.
- 쿼리가 실행되는 열을 보호하는 키에 대한 열 마스터 키와 메타데이터에 액세스할 수 있어야 합니다. 자세한 내용은 아래 [암호화된 열을 쿼리하기 위한 권한](#permissions-for-querying-encrypted-columns)을 참조하세요.
- 열 마스터 키는 Azure Key Vault 또는 Windows 인증서 저장소에 저장해야 합니다. Azure Data Studio는 다른 키 저장소를 지원하지 않습니다.

### <a name="steps"></a>단계
1.  데이터를 검색하고 암호를 해독하는 `SELECT` 쿼리를 실행할 쿼리 창에 대한 데이터베이스 연결에 Always Encrypted를 사용 설정합니다. 이는 Azure Data Studio에서 사용하는 [Microsoft .NET Data Provider for SQL Server](../../../connect/ado-net/sql/sqlclient-support-always-encrypted.md)에 쿼리 결과 집합에 있는 암호화된 열의 암호를 해독하도록 지시합니다. 아래의 [데이터베이스 연결에 Always Encrypted 사용 및 사용 안 함](#enabling-and-disabling-always-encrypted-for-a-database-connection)을 참조하세요.
1.  `SELECT` 쿼리를 실행합니다. 암호화된 열에서 검색된 모든 데이터는 원래 데이터 형식의 일반 텍스트 값으로 반환됩니다.
 
### <a name="example"></a>예제
SSN이 `Patients` 테이블의 암호화된 열이라고 가정할 경우 아래 표시된 쿼리는 Always Encrypted가 데이터베이스 연결에 사용되고 `SSN` 열에 대해 구성된 열 마스터 키에 대한 액세스 권한이 있는 경우 일반 텍스트 값을 반환합니다.   

![SELECT * FROM [dbo].[Patients] 쿼리 및 일반 텍스트 값으로 표시된 쿼리 결과 스크린샷](../../../relational-databases/security/encryption/media/always-encrypted-ads-query-plaintext.png)
 
## <a name="sending-plaintext-values-targeting-encrypted-columns"></a>암호화된 열을 대상으로 하는 일반 텍스트 값 보내기       
이 섹션에서는 암호화된 열을 대상으로 값을 보내는 쿼리를 실행하는 방법을 설명합니다. 예를 들어 암호화된 열에 저장된 값을 삽입, 업데이트 또는 필터링하는 쿼리를 실행할 수 있습니다.

### <a name="prerequisites"></a>필수 구성 요소
- Azure Data Studio 버전 18.1 이상.
- 쿼리가 실행되는 열을 보호하는 키에 대한 열 마스터 키와 메타데이터에 액세스할 수 있어야 합니다. 자세한 내용은 아래 [암호화된 열을 쿼리하기 위한 권한](#permissions-for-querying-encrypted-columns)을 참조하세요.
- 열 마스터 키는 Azure Key Vault 또는 Windows 인증서 저장소에 저장해야 합니다. Azure Data Studio는 다른 키 저장소를 지원하지 않습니다.

### <a name="steps"></a>단계
1. 데이터를 검색하고 암호를 해독하는 `SELECT` 쿼리를 실행할 쿼리 창에 대한 데이터베이스 연결에 Always Encrypted를 사용 설정합니다. 이렇게 하면 Azure Data Studio에서 사용하는 [Microsoft .NET Data Provider for SQL Server](../../../connect/ado-net/sql/sqlclient-support-always-encrypted.md)는 암호화된 열을 대상으로 하는 쿼리 매개 변수를 암호화하고 암호화된 열에서 검색한 결과를 암호 해독합니다. 아래의 [데이터베이스 연결에 Always Encrypted 사용 및 사용 안 함](#enabling-and-disabling-always-encrypted-for-a-database-connection)을 참조하세요. 
1. 쿼리 창에서 Always Encrypted에 대한 매개 변수화를 사용 설정합니다. 자세한 내용은 아래의 [Always Encrypted에 대한 매개 변수화](#parameterization-for-always-encrypted) 를 참조하세요.
1. Transact-SQL 변수를 선언하고 데이터베이스로 전송(삽입, 업데이트 또는 필터링)할 값으로 초기화합니다. 
1. 데이터베이스에 TRANSACT-SQL 변수 값을 전송하는 쿼리를 실행합니다. Azure Data Studio는 이 변수를 쿼리 매개 변수로 변환하고 해당 값을 암호화하여 데이터베이스로 전송합니다.   

### <a name="example"></a>예제
`SSN`을 `Patients` 테이블에 있는 `char(11)` 열이라고 가정하는 아래 스크립트는 SSN 열에서 `'795-73-9838'`을 포함하는 행을 찾습니다. 데이터베이스 연결에 대한 Always Encrypted를 사용 설정하고, 쿼리 창에서 Always Encrypted에 대한 매개 변수화를 사용 설정했으며, `SSN` 열에 대해 구성한 열 마스터 키에 액세스할 수 있다면 결과가 반환됩니다.   

![DECLARE @SSN char(11) = '795-73-9838' SELECT * FROM [dbo].[Patients] WHERE [SSN] = @SSN 쿼리 및 쿼리 결과 스크린샷](../../../relational-databases/security/encryption/media/always-encrypted-ads-query-parameters.png)

## <a name="permissions-for-querying-encrypted-columns"></a>암호화된 열을 쿼리하기 위한 권한

암호 텍스트에서 데이터를 검색하는 쿼리를 비롯한 암호화된 열에 대한 쿼리를 실행하려면 데이터베이스에서 **VIEW ANY COLUMN MASTER KEY DEFINITION** 및 **VIEW ANY COLUMN ENCRYPTION KEY DEFINITION** 권한이 있어야 합니다.

위 권한 외에도 쿼리 결과의 암호를 해독하거나 쿼리 매개 변수(Transact-SQL 변수를 매개 변수화하여 생성된)를 암호화하려면 대상 열을 보호하는 열 마스터 키에 대한 액세스 권한도 필요합니다.

- **인증서 저장소: 로컬 컴퓨터:** 열 마스터 키로 사용되는 인증서에 대한 **읽기** 권한이 있거나 컴퓨터의 관리자여야 합니다.   
- **Azure Key Vault:** 열 마스터 키를 포함하는 키 자격 증명 모음에 대한 **get**, **unwrapKey** 및 **verify** 권한이 필요합니다.

자세한 내용은 [열 마스터 키 만들기 및 저장(상시 암호화)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)를 참조하세요.

## <a name="enabling-and-disabling-always-encrypted-for-a-database-connection"></a>데이터베이스 연결에 Always Encrypted 사용 및 사용 안 함   
Azure Data Studio에서 데이터베이스에 연결하는 경우 데이터베이스 연결에 Always Encrypted를 사용하거나 사용하지 않도록 설정할 수 있습니다. 기본적으로 Always Encrypted는 사용 안 함으로 설정됩니다. 

데이터베이스 연결에 Always Encrypted를 사용하도록 설정하면 Azure Data Studio에서 사용하는 [Microsoft .NET Data Provider for SQL Server](../../../connect/ado-net/sql/sqlclient-support-always-encrypted.md)가 다음 작업을 투명하게 시도합니다.   
-   암호화된 열에서 검색된 값의 암호를 해독하여 쿼리 결과에 반환합니다.   
-   암호화된 데이터베이스 열을 대상으로 하는 매개 변수화된 TRANSACT-SQL 변수의 값을 암호화합니다.   

연결에 대해 Always Encrypted를 사용하도록 설정하지 않으면 Microsoft .NET Data Provider for SQL Server는 쿼리 매개 변수를 암호화하거나 결과의 암호를 해독하지 않습니다.

데이터베이스에 연결할 때 Always Encrypted를 사용하거나 사용하지 않도록 설정할 수 있습니다. 데이터베이스 연결에 관한 일반적인 정보는 다음을 참조하세요.
- [빠른 시작: Azure Data Studio를 사용하여 SQL Server 연결 및 쿼리](../../../azure-data-studio/quickstart-sql-server.md)
- [빠른 시작: Azure Data Studio를 사용한 Azure SQL 데이터베이스 연결 및 쿼리](../../../azure-data-studio/quickstart-sql-database.md)

Always Encrypted를 사용하거나 사용하지 않도록 설정하려면 다음을 수행합니다.
1. **연결** 대화 상자에서 **고급...** 을 클릭합니다.
2. 연결에 대해 Always Encrypted를 사용하도록 설정하려면 **Always Encrypted** 필드를 **사용** 으로 설정합니다. Always Encrypted를 사용하지 않도록 설정하려면 **Always Encrypted** 필드를 비워 두거나 **사용 안 함** 으로 설정합니다.
3. [!INCLUDE [sssqlv15-md](../../../includes/sssqlv15-md.md)]를 사용하며 SQL Server 인스턴스가 보안 enclave로 구성되었다면 enclave 프로토콜 및 enclave 증명 URL을 지정할 수 있습니다. SQL Server 인스턴스에서 보안 enclave를 사용하지 않는다면 **증명 프로토콜** 과 **Enclave 증명 URL** 필드를 비워 두어야 합니다. 자세한 내용은 [보안 Enclave를 사용한 Always Encrypted](always-encrypted-enclaves.md)를 참조하세요.
4. **확인** 을 클릭하여 **고급 속성** 을 닫습니다.

![연결에 Always Encrypted를 사용하도록 설정하는 단계를 보여 주는 짧은 동영상](../../../relational-databases/security/encryption/media/always-encrypted-ads-connect.gif)

> [!TIP]
> 기존 쿼리 창에 대해 Always Encrypted을 사용하거나 사용하지 않도록 전환하려면 **연결 끊기** 를 클릭하고 **연결** 을 클릭한 다음 위의 단계를 모두 완료하여 원하는 **Always Encrypted** 필드 값으로 데이터베이스를 다시 연결합니다. 

> [!NOTE] 
> 현재 쿼리 창의 **연결 변경** 단추로는 Always Encrypted를 사용하거나 사용하지 않도록 전환할 수 없습니다.

## <a name="parameterization-for-always-encrypted"></a>Always Encrypted에 대한 매개 변수화

Always Encrypted에 대한 매개 변수화는 Transact-SQL 변수를 쿼리 매개 변수( [SqlParameter 클래스](/dotnet/api/microsoft.data.sqlclient.sqlparameter)의 인스턴스)로 자동으로 변환하는 Azure Data Studio 18.1 이상에서 제공하는 기능입니다. 이 기능을 사용하면 기본 [Microsoft .NET Data Provider for SQL Server](../../../connect/ado-net/sql/sqlclient-support-always-encrypted.md)에서 암호화된 열을 대상으로 하는 데이터를 검색하고, 이러한 데이터를 데이터베이스로 전송하기 전에 암호화할 수 있습니다.
  
매개 변수화하지 않으면 Microsoft .NET Data Provider for SQL Server는 쿼리 창에서 작성한 각 문을 매개 변수화되지 않은 쿼리로 전달합니다. 쿼리에 암호화된 열을 대상으로 하는 리터럴 또는 Transact-SQL 변수가 포함된 경우 .NET Framework Data Provider for SQL Server는 쿼리를 데이터베이스로 전송하기 전에 검색 및 암호화할 수 없습니다. 따라서 일반 텍스트 리터럴 Transact-SQL 변수와 암호화된 열 간의 형식 불일치로 인해 쿼리에 실패합니다. 예를 들어 `SSN` 열이 암호화된 것으로 가정할 경우 매개 변수화하지 않으면 다음 쿼리가 실패합니다.   

```sql
DECLARE @SSN CHAR(11) = '795-73-9838'
SELECT * FROM [dbo].[Patients]
WHERE [SSN] = @SSN
```

### <a name="enabling-and-disabling-parameterization-for-always-encrypted"></a>Always Encrypted에 대한 매개 변수화 사용 및 사용 안 함

Always Encrypted에 대한 매개 변수화를 기본적으로 사용하지 않도록 설정됩니다.

Always Encrypted에 대한 매개 변수화를 사용하거나 사용하지 않는 방법:

1. **파일** > **기본 설정** > **설정**(Mac에서는 **코드** > **기본 설정** > **설정**)을 선택합니다.
2. **데이터** > **Microsoft SQL Server** 로 이동합니다.
3. **Always Encrypted에 대해 매개 변수화 사용** 을 선택하거나 선택 취소합니다.
4. **설정** 창을 닫습니다.

![Always Encrypted에 매개 변수화를 사용하거나 사용하지 않도록 설정하는 방법을 보여 주는 짧은 동영상](../../../relational-databases/security/encryption/media/always-encrypted-ads-parameterization.gif)

> [!NOTE]
> Always Encrypted에 대한 매개 변수화는 Always Encrypted가 설정된 데이터베이스 연결을 사용하는 쿼리 창에서만 작동합니다( [데이터베이스 연결에 Always Encrypted 사용/사용 안 함](#enabling-and-disabling-always-encrypted-for-a-database-connection) 참조). 쿼리 창에서 Always Encrypted가 설정되지 않은 데이터베이스 연결을 사용하는 경우에는 Transact-SQL 변수가 매개 변수화되지 않습니다.

### <a name="how-parameterization-for-always-encrypted-works"></a>Always Encrypted에 대한 매개 변수화의 작동 방식

쿼리 창에 대해 Always Encrypted에 대한 매개 변수화와 Always Encrypted를 모두 사용 설정하면 Azure Data Studio는 다음 필수 조건을 충족하는 Transact-SQL 변수를 매개 변수화합니다.

- 동일한 문에 선언되고 초기화된 변수(인라인 초기화). 별도의 `SET` 문을 사용하여 선언된 변수는 매개 변수화되지 않습니다.
- 단일 리터럴을 사용하여 초기화된 변수. 연산자나 함수가 포함된 식을 사용하여 초기화된 변수는 매개 변수화되지 않습니다.

다음은 Azure Data Studio가 매개 변수화하는 변수의 예입니다.

```sql
DECLARE @SSN char(11) = '795-73-9838';
   
DECLARE @BirthDate date = '19990104';
DECLARE @Salary money = $30000;
```

이것은 Azure Data Studio가 매개 변수화하지 않는 변수의 몇 가지 예 입니다.

```sql
DECLARE @Name nvarchar(50); --Initialization separate from declaration
SET @Name = 'Abel';

DECLARE @StartDate date = GETDATE(); -- a function used instead of a literal

DECLARE @NewSalary money = @Salary * 1.1; -- an expression used instead of a literal
```
 
시도한 매개 변수화가 성공하려면   
- 매개 변수화할 변수의 초기화에 사용된 리터럴 형식이 변수 선언의 형식과 일치해야 합니다.   
- 변수의 선언된 형식이 날짜 형식이거나 시간 형식인 경우 변수는 다음 ISO 8601 규격 형식 중 하나를 사용하는 문자열을 사용하여 초기화되어야 합니다.   

매개 변수화 오류가 발생하는 Transact-SQL 변수 선언의 예는 다음과 같습니다.

```sql
DECLARE @BirthDate date = '01/04/1999' -- unsupported date format   
   
DECLARE @Number int = 1.1 -- the type of the literal does not match the type of the variable   
```

Azure Data Studio는 Intellisense를 사용하여 성공적으로 매개 변수화할 수 있는 변수와 매개 변수화 시도에 실패하는 변수(및 이유)를 알려 줍니다.   

성공적으로 매개 변수화할 수 있는 변수의 선언은 쿼리 창에 정보 메시지 밑줄로 표시됩니다. 정보 메시지 밑줄이 표시된 선언 문에 마우스 커서를 놓으면 결과 [SqlParameter Class](/dotnet/api/microsoft.data.sqlclient.sqlparameter) 개체( [SqlDbType](/dotnet/api/microsoft.data.sqlclient.sqlparameter.dbtype), [크기](/dotnet/api/microsoft.data.sqlclient.sqlparameter.size), [정밀도](/dotnet/api/microsoft.data.sqlclient.sqlparameter.precision), [배율](/dotnet/api/microsoft.data.sqlclient.sqlparameter.scale), [SqlValue](/dotnet/api/microsoft.data.sqlclient.sqlparameter.sqlvalue)로 매핑된 변수)의 키 속성 값을 비롯한 매개 변수화 프로세스의 결과를 포함하는 메시지가 표시됩니다. **문제** 보기에서 성공적으로 매개 변수화된 모든 변수의 전체 목록을 볼 수 있습니다. **문제** 보기를 열려면 **보기** > **문제** 를 선택합니다.    



Azure Data Studio에서 변수를 매개 변수화하려 했지만 매개 변수화에 실패한 경우 해당 변수의 선언이 오류 밑줄로 표시됩니다. 오류 밑줄이 표시된 선언 문 위에 마우스를 놓으면 오류에 대한 결과가 표시됩니다. **문제** 보기에서 모든 변수에 대한 전체 매개 변수화 오류 목록을 볼 수도 있습니다.

 
> [!NOTE]
> Always Encrypted는 형식 변환의 제한된 하위 집합을 지원하므로 대부분의 경우 Transact-SQL 변수의 데이터 형식은 대상으로 하는 대상 데이터베이스 열의 형식과 같아야 합니다. 예를 들어 `SSN` 테이블의 `Patients` 열 형식이 `char(11)`이라고 가정할 경우 아래 쿼리는 `@SSN` 변수의 형식(`nchar(11)`)이 열 형식과 일치하지 않으므로 실패합니다.   

```sql
DECLARE @SSN nchar(11) = '795-73-9838'
SELECT * FROM [dbo].[Patients]
WHERE [SSN] = @SSN;
```

```output
Msg 402, Level 16, State 2, Line 5   
The data types char(11) encrypted with (encryption_type = 'DETERMINISTIC', 
encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'CEK_Auto1', 
column_encryption_key_database_name = 'Clinic') collation_name = 'Latin1_General_BIN2' 
and nchar(11) encrypted with (encryption_type = 'DETERMINISTIC', 
encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'CEK_Auto1', 
column_encryption_key_database_name = 'Clinic') are incompatible in the equal to operator.
```

> [!NOTE]
> 매개 변수화를 사용하지 않으면 형식 변환을 포함하여 전체 쿼리가 SQL Server/Azure SQL Database 내에서 처리됩니다. 매개 변수화를 사용하면 Azure Data Studio에서 Microsoft .NET Data Provider for SQL Server가 일부 형식 변환을 수행합니다. Microsoft .NET 형식 시스템과 SQL Server 형식 시스템 간의 차이(예: float와 같은 일부 형식의 정밀도 차이)로 인해 매개 변수화를 사용하여 실행된 쿼리는 매개 변수화를 사용하지 않고 실행된 쿼리와 다른 결과를 생성할 수 있습니다. 

## <a name="next-steps"></a>다음 단계
- [Always Encrypted를 사용하여 애플리케이션 개발](always-encrypted-client-development.md)


## <a name="see-also"></a>참고 항목
- [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)