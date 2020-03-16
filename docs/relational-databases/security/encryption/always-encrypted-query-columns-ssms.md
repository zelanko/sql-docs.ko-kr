---
title: SQL Server Management Studio로 Always Encrypted를 사용하는 열 쿼리 | Microsoft Docs
ms.custom: ''
ms.date: 10/31/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Always Encrypted, configure with SSMS
ms.assetid: 29816a41-f105-4414-8be1-070675d62e84
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 221c5c0fa216b8d5fba7f133b717a3d102aea963
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79287137"
---
# <a name="query-columns-using-always-encrypted-with-sql-server-management-studio"></a>SQL Server Management Studio로 Always Encrypted를 사용하는 열 쿼리
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

이 문서에서는 [SSMS(SQL Server Management Studio)](../../../ssms/download-sql-server-management-studio-ssms.md)를 사용하여 [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)로 암호화된 열을 쿼리하는 방법을 설명합니다. SSMS를 사용하여 다음을 수행할 수 있습니다.
- 암호화된 열에 저장된 암호 텍스트 값을 검색합니다. 
- 암호화된 열에 저장된 일반 텍스트 값을 검색합니다.   
- 암호화된 열을 대상으로 하는 일반 텍스트 값을 보냅니다(예: `INSERT` 또는 `UPDATE` 문에 포함하거나 `WHERE` 문에서 `SELECT` 절의 조회 매개 변수로).

## <a name="retrieving-ciphertext-values-stored-in-encrypted-columns"></a>암호화된 열에 저장된 암호 텍스트 값 검색    
데이터의 암호를 해독하지 않고 암호화된 열에 저장된 데이터의 암호 텍스트를 검색하는 SELECT 쿼리를 실행하는 경우 데이터를 보호하는 열 마스터 키에 대한 액세스 권한이 필요하지 않습니다. SSMS에서 암호화된 열의 값을 암호 텍스트로 검색하려면 다음을 수행합니다.

1. 쿼리가 실행되는 열을 보호하는 키에 대한 메타데이터에 액세스할 수 있어야 합니다. 실제 열 마스터 키에 액세스할 필요는 없지만 데이터베이스의 열 마스터 키 및 열 암호화 키 메타데이터 개체를 보려면 데이터베이스 수준 사용 권한이 필요합니다. 자세한 내용은 아래 [암호화된 열을 쿼리하기 위한 권한](#permissions-for-querying-encrypted-columns)을 참조하세요.
1. 암호 텍스트 값을 검색하는 `SELECT` 쿼리를 실행할 쿼리 편집기 창에 대한 데이터베이스 연결에 Always Encrypted가 사용 안 함으로 설정되어야 합니다. 아래의 [데이터베이스 연결에 Always Encrypted 사용 및 사용 안 함](#en-dis)을 참조하세요.     
1. `SELECT` 쿼리를 실행합니다. 암호화된 열에서 검색된 모든 데이터는 이진(암호화) 값으로 반환됩니다.   

### <a name="example"></a>예제
`SSN` 이 `Patients` 테이블의 암호화된 열이라고 가정할 경우, 아래 표시된 쿼리는 데이터베이스 연결에 Always Encrypted가 사용되지 않는 경우 이진 암호 텍스트 값을 검색합니다.   

![always-encrypted-ciphertext](../../../relational-databases/security/encryption/media/always-encrypted-ciphertext.png)
 
## <a name="retrieving-plaintext-values-stored-in-encrypted-columns"></a>암호화된 열에 저장된 일반 텍스트 값 검색    
암호화된 열에서 일반 텍스트 값을 검색하여 값의 암호를 해독하려면   
1. 쿼리가 실행되는 열을 보호하는 키에 대한 열 마스터 키와 메타데이터에 액세스할 수 있어야 합니다. 자세한 내용은 아래 [암호화된 열을 쿼리하기 위한 권한](#permissions-for-querying-encrypted-columns)을 참조하세요.
1.  데이터를 검색하고 암호를 해독하는 `SELECT` 쿼리를 실행할 쿼리 편집기 창에 대한 데이터베이스 연결에 Always Encrypted가 사용으로 설정되어야 합니다. 이는 SSMS에서 사용하는 .NET Framework Data Provider for SQL Server에 쿼리 결과 집합의 암호화된 데이터의 암호를 해독하도록 지시합니다. 아래의 [데이터베이스 연결에 Always Encrypted 사용 및 사용 안 함](#en-dis)을 참조하세요.
1.  `SELECT` 쿼리를 실행합니다. 암호화된 열에서 검색된 모든 데이터는 원래 데이터 형식의 일반 텍스트 값으로 반환됩니다.
 
### <a name="example"></a>예제
SSN이 `char(11)` 테이블의 암호화된 `Patients` 열이라고 가정할 경우, 아래 표시된 쿼리는 Always Encrypted가 데이터베이스 연결에 사용되고 `SSN` 열에 대해 구성된 열 마스터 키에 대한 액세스 권한이 있는 경우 일반 텍스트 값을 반환합니다.   

![always-encrypted-plaintext](../../../relational-databases/security/encryption/media/always-encrypted-plaintext.png)
 
## <a name="sending-plaintext-values-targeting-encrypted-columns"></a>암호화된 열을 대상으로 하는 일반 텍스트 값 보내기       
암호화된 열을 대상으로 하는 값을 보내는 쿼리(예: 암호화된 열에 저장된 값을 삽입, 업데이트 또는 필터링하는 쿼리)를 실행하려면 다음을 수행합니다.

1. 쿼리가 실행되는 열을 보호하는 키에 대한 열 마스터 키와 메타데이터에 액세스할 수 있어야 합니다. 자세한 내용은 아래의 [암호화된 열을 쿼리하기 위한 권한](#permissions-for-querying-encrypted-columns)을 참조하세요.
1.  데이터를 검색하고 암호를 해독하는 `SELECT` 쿼리를 실행할 쿼리 편집기 창에 대한 데이터베이스 연결에 Always Encrypted가 사용으로 설정되어야 합니다. 이는 SSMS에서 사용하는 .NET Framework Data Provider for SQL Server에 쿼리 결과 집합의 암호화된 데이터의 암호를 해독하도록 지시합니다. 아래의 [데이터베이스 연결에 Always Encrypted 사용 및 사용 안 함](#en-dis)을 참조하세요.
1. 쿼리 편집기 창에 Always Encrypted에 대한 매개 변수화가 사용하도록 설정되어 있는지 확인합니다. SSMS 버전 17.0 이상이 필요합니다. Transact-SQL 변수를 선언하고 데이터베이스로 전송(삽입, 업데이트 또는 필터링)할 값으로 초기화합니다. 자세한 내용은 아래의 [Always Encrypted에 대한 매개 변수화](#param) 를 참조하세요.

1. 데이터베이스에 TRANSACT-SQL 변수 값을 전송하는 쿼리를 실행합니다. SSMS은 이 변수를 쿼리 매개 변수로 변환하고 해당 값을 암호화하여 데이터베이스로 전송합니다.   

### <a name="example"></a>예제
`SSN` 이 `char(11)` 테이블의 암호화된 `Patients` 열이라고 가정할 경우, 아래 스크립트는 Always Encrypted가 데이터베이스 연결에 사용되고, Always Encrypted에 대한 매개 변수화가 쿼리 편집기 창에 사용하도록 설정되며, `'795-73-9838'` 열에 대해 구성된 열 마스터 키에 대한 액세스 권한이 있는 경우 SSN 열에서 `LastName` 이 포함된 행을 찾아서 `SSN` 열의 값을 반환합니다.   

![always-encrypted-patients](../../../relational-databases/security/encryption/media/always-encrypted-patients.png)

## <a name="permissions-for-querying-encrypted-columns"></a>암호화된 열을 쿼리하기 위한 권한

암호 텍스트 데이터를 검색하는 쿼리를 포함하여 암호화된 열에 대해 쿼리를 실행하려면 데이터베이스에서 `VIEW ANY COLUMN MASTER KEY DEFINITION` 및 `VIEW ANY COLUMN ENCRYPTION KEY DEFINITION` 권한이 있어야 합니다.

위 권한 외에도 쿼리 결과의 암호를 해독하거나 쿼리 매개 변수(Transact-SQL 변수를 매개 변수화하여 생성된)를 암호화하려면 대상 열을 보호하는 열 마스터 키에 대한 액세스 권한도 필요합니다.

- **인증서 저장소 - 로컬 컴퓨터** - 열 마스터 키로 사용되는 인증서에 대한 `Read` 권한이 있거나 컴퓨터의 관리자여야 합니다.   
- **Azure Key Vault** - 열 마스터 키를 포함하는 자격 증명 모음에 대한 `get`, `unwrapKey` 및 `verify` 권한이 필요합니다.
- **KSP(키 저장소 공급자)** – 저장소 및 KSP 구성에 따라 키 저장소 또는 키를 사용할 때 필수 사용 권한 및 자격 증명을 확인하는 메시지가 표시될 수도 있습니다.   
- **CSP(암호화 서비스 공급자)** – 저장소 및 CSP 구성에 따라 키 저장소 또는 키를 사용할 때 필수 사용 권한 및 자격 증명을 확인하는 메시지가 표시될 수도 있습니다.

자세한 내용은 [열 마스터 키 만들기 및 저장(상시 암호화)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)를 참조하세요.

## <a name="en-dis"></a> 데이터베이스 연결에 Always Encrypted 사용 및 사용 안 함   
SSMS에서 데이터베이스에 연결하는 경우 데이터베이스 연결에 Always Encrypted를 사용하거나 사용하지 않도록 설정할 수 있습니다. 기본적으로 Always Encrypted는 사용 안 함으로 설정됩니다. 

데이터베이스 연결에 Always Encrypted를 사용하도록 설정하면 SQL Server Management Studio에서 사용하는 .NET Framework Data Provider for SQL Server가 다음 작업을 투명하게 시도합니다.   
-   암호화된 열에서 검색된 값의 암호를 해독하여 쿼리 결과에 반환합니다.   
-   암호화된 데이터베이스 열을 대상으로 하는 매개 변수화된 TRANSACT-SQL 변수의 값을 암호화합니다.   

연결에 대해 Always Encrypted를 사용하도록 설정하지 않으면 SSMS가 사용하는 .NET Framework Data Provider for SQL Server는 쿼리 매개 변수를 암호화하거나 결과의 암호를 해독하지 않습니다.

새 연결을 만들거나 **서버에 연결** 대화 상자를 사용하여 기존 연결을 변경하는 경우 Always Encrypted를 사용하거나 사용하지 않도록 설정할 수 있습니다. 

Always Encrypted를 사용하거나 사용하지 않도록 설정하려면 다음을 수행합니다.
1. **서버에 연결** 대화 상자를 엽니다. 자세한 내용은 [SQL Server 인스턴스에 연결](../../../ssms/tutorials/connect-query-sql-server.md#connect-to-a-sql-server-instance)을 참조하세요.
1. **옵션 >>** 을 클릭합니다.
1. SSMS 18 이상 버전을 사용하는 경우:
    1. **Always Encrypted** 탭을 선택합니다.
    1. Always Encrypted를 사용하도록 설정하려면 **Always Encrypted 사용(열 암호화)** 를 선택합니다. Always Encrypted를 사용하지 않도록 설정하려면 **Always Encrypted 사용(열 암호화)** 을 선택하지 않아야 합니다.
    1. [!INCLUDE [sssqlv15-md](../../../includes/sssqlv15-md.md)]를 사용하고 SQL Server 인스턴스가 보안 enclave로 구성된 경우 Enclave 증명 URL을 지정할 수 있습니다. SQL Server 인스턴스에서 보안 enclave를 사용하지 않는 경우 **Enclave 증명 URL** 텍스트 상자를 비워 두어야 합니다. 자세한 내용은 [보안 Enclave를 사용한 Always Encrypted](always-encrypted-enclaves.md)를 참조하세요.
1. SSMS 17 이하 버전을 사용하는 경우:
    1. **추가 속성** 탭을 선택합니다.
    1. Always Encrypted를 사용하도록 설정하려면 `Column Encryption Setting = Enabled`를 입력합니다. Always Encrypted 사용하지 않도록 설정하려면 `Column Encryption Setting = Disabled`를 지정하거나 **추가 속성** 탭에서 **열 암호화 설정**의 설정을 제거합니다(기본값은 **사용 안 함**).   
 1. **연결**을 클릭합니다.

> [!TIP]
> 기존 쿼리 편집기 창에 대해 Always Encrypted의 사용을 설정하거나 해제하려면 다음을 수행합니다.   
> 1.    쿼리 편집기 창의 아무 곳이나 마우스 오른쪽 단추로 클릭합니다.
> 2.    **연결** > **연결 변경...** 을 선택합니다. 그러면 쿼리 편집기 창의 현재 연결에 대한 **서버에 연결** 대화 상자가 열립니다. 
> 2.    위의 단계에 따라 Always Encrypted를 사용하거나 사용하지 않도록 설정하고 **연결**을 클릭합니다.  
   
## <a name="param"></a>Always Encrypted에 대한 매개 변수화   
 
Always Encrypted에 대한 매개 변수화는 Transact-SQL 변수를 쿼리 매개 변수( [SqlParameter 클래스](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx)의 인스턴스)로 자동으로 변환하는 SQL Server Management Studio의 기능입니다. SSMS 버전 17.0 이상이 필요합니다. 이 기능을 사용하면 기본 .NET Framework Data Provider for SQL Server이 암호화된 열을 대상으로 하는 데이터를 검색하고, 이러한 데이터를 데이터베이스로 전송하기 전에 암호화합니다. 
  
매개 변수화하지 않으면 .NET Framework Data Provider가 쿼리 편집기에서 작성한 각 문을 매개 변수화되지 않은 쿼리로 전달합니다. 쿼리에 암호화된 열을 대상으로 하는 리터럴 또는 Transact-SQL 변수가 포함된 경우 .NET Framework Data Provider for SQL Server는 쿼리를 데이터베이스로 전송하기 전에 검색 및 암호화할 수 없습니다. 따라서 일반 텍스트 리터럴 Transact-SQL 변수와 암호화된 열 간의 형식 불일치로 인해 쿼리에 실패합니다. 예를 들어 `SSN` 열이 암호화된 것으로 가정할 경우 매개 변수화하지 않으면 다음 쿼리가 실패합니다.   

```sql
DECLARE @SSN NCHAR(11) = '795-73-9838'
SELECT * FROM [dbo].[Patients]
WHERE [SSN] = @SSN
```

### <a name="enabling-and-disabling-parameterization-for-always-encrypted"></a>Always Encrypted에 대한 매개 변수화 사용 및 사용 안 함

Always Encrypted에 대한 매개 변수화를 기본적으로 사용하지 않도록 설정됩니다.

현재 쿼리 편집기 창에 Always Encrypted에 대한 매개 변수화를 사용하도록/사용하지 않도록 설정하려면 다음을 수행합니다.

1. 주 메뉴에서 **쿼리** 를 선택합니다.
2. **쿼리 옵션...** 을 선택합니다.
3. **실행** > **고급**으로 이동합니다.
4. **Always Encrypted에 대해 매개 변수화 사용**을 선택하거나 선택 취소합니다.
5. **확인**을 클릭합니다.

향후 쿼리 편집기 창에 Always Encrypted에 대한 매개 변수화를 사용하도록/사용하지 않도록 설정하려면 다음을 수행합니다.

1. 주 메뉴에서 **도구** 를 선택합니다.
2. **옵션...** 을 선택합니다.
3. **쿼리 실행** > **SQL Server** > **고급**으로 이동합니다.
4. **Always Encrypted에 대해 매개 변수화 사용**을 선택하거나 선택 취소합니다.
5. **확인**을 클릭합니다.

Always Encrypted가 설정된 데이터베이스 연결을 사용하지만 매개 변수화가 사용되지 않는 쿼리 편집기 창에서 쿼리를 실행하는 경우 사용하도록 설정하라는 메시지가 나타납니다.

> [!NOTE]
> Always Encrypted에 대한 매개 변수화는 Always Encrypted가 설정된 데이터베이스 연결을 사용하는 쿼리 편집기 창에서만 작동합니다([Always Encrypted에 대한 매개 변수화 사용 및 사용 안 함](#enabling-and-disabling-parameterization-for-always-encrypted) 참조). 쿼리 편집기 창에서 Always Encrypted가 설정되지 않은 데이터베이스 연결을 사용하는 경우에는 Transact-SQL 변수가 매개 변수화되지 않습니다.

### <a name="how-parameterization-for-always-encrypted-works"></a>Always Encrypted에 대한 매개 변수화의 작동 방식

쿼리 편집기 창에 대해 데이터베이스 연결에서 Always Encrypted에 대한 매개 변수화와 Always Encrypted 동작이 둘 다 사용하도록 설정된 경우 SQL Server Management Studio는 다음 필수 조건을 충족하는 Transact-SQL 변수를 매개 변수화합니다.

- 동일한 문에 선언되고 초기화된 변수(인라인 초기화). 별도의 `SET` 문을 사용하여 선언된 변수는 매개 변수화되지 않습니다.
- 단일 리터럴을 사용하여 초기화된 변수. 연산자나 함수가 포함된 식을 사용하여 초기화된 변수는 매개 변수화되지 않습니다.

다음은 SQL Server Management Studio가 매개 변수화하는 변수의 예입니다.

```sql
DECLARE @SSN char(11) = '795-73-9838';
   
DECLARE @BirthDate date = '19990104';
DECLARE @Salary money = $30000;
```

또한 SQL Server Management Studio가 매개 변수화하지 않는 변수의 몇 가지 예도 있습니다.

```sql
DECLARE @Name nvarchar(50); --Initialization separate from declaration
SET @Name = 'Abel';

DECLARE @StartDate date = GETDATE(); -- a function used instead of a literal

DECLARE @NewSalary money = @Salary * 1.1; -- an expression used instead of a literal
```
 
시도한 매개 변수화가 성공하려면   
- 매개 변수화할 변수의 초기화에 사용된 리터럴 형식이 변수 선언의 형식과 일치해야 합니다.   
- 변수의 선언된 형식이 날짜 형식이거나 시간 형식인 경우 변수는 다음 ISO 8601 규격 형식 중 하나를 사용하는 문자열을 사용하여 초기화되어야 합니다.   

매개 변수화 오류가 발생하는 TRANSACT-SQL 변수 선언의 예는 다음과 같습니다.   
```sql
DECLARE @BirthDate date = '01/04/1999' -- unsupported date format   
   
DECLARE @Number int = 1.1 -- the type of the literal does not match the type of the variable   
```
SQL Server Management Studio는 Intellisense를 사용하여 성공적으로 매개 변수화할 수 있는 변수와 매개 변수화 시도에 실패하는 변수(및 이유)를 알려 줍니다.   

성공적으로 매개 변수화할 수 있는 변수의 선언은 쿼리 편집기에 경고 밑줄로 표시됩니다. 경고 밑줄이 표시된 선언 문에 마우스를 놓으면 결과 [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) 개체(매핑된 변수)의 키 속성 값을 비롯한 매개 변수화 프로세스의 결과가 표시됩니다. [SqlDbType](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.sqldbtype.aspx), [크기](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.size.aspx), [정밀도](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.precision.aspx)를 [배율](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.scale.aspx), [SqlValue](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.sqlvalue.aspx). **오류 목록** 보기의 **경고** 탭에서 성공적으로 매개 변수화된 모든 변수의 전체 목록을 볼 수 있습니다. **오류 목록** 보기를 열려면 주 메뉴에서 **보기** 를 선택한 다음 **오류 목록**을 선택합니다.    

SQL Server Management Studio가 변수를 매개 변수화하려고 시도했지만 매개 변수화에 실패한 경우 해당 변수의 선언이 오류 밑줄로 표시됩니다. 오류 밑줄이 표시된 선언 문 위에 마우스를 놓으면 오류에 대한 결과가 표시됩니다. **오류 목록** 보기의 **오류** 탭에서 모든 변수에 대한 전체 매개 변수화 오류 목록을 볼 수도 있습니다는. **오류 목록** 보기를 열려면 주 메뉴에서 **보기** 를 선택한 다음 **오류 목록**을 선택합니다.   

아래 스크린샷은 6개 변수 선언의 예를 보여 줍니다. SQL Server Management Studio에서 처음 세 개의 변수를 성공적으로 매개 변수화했습니다. 마지막 세 변수는 매개 변수화에 대한 필수 조건을 충족하지 않았으므로 SQL Server Management Studio에서 매개 변수화를 시도하지 않았습니다(선언이 표시되지 않음).

![always-encrypted-parameter-warnings](../../../relational-databases/security/encryption/media/always-encrypted-parameter-warnings.png)
 
아래의 또 다른 예제는 매개 변수화에 대한 필수 조건을 충족하지만 변수가 잘못 초기화되어 매개 변수화 시도에 실패한 두 변수를 보여 줍니다.    
 
![always-encrypted-error](../../../relational-databases/security/encryption/media/always-encrypted-error.png)
 
> [!NOTE]
> Always Encrypted는 형식 변환의 제한된 하위 집합을 지원하므로 대부분의 경우 Transact-SQL 변수의 데이터 형식은 대상으로 하는 대상 데이터베이스 열의 형식과 같아야 합니다. 예를 들어 `SSN` 테이블의 `Patients` 열 형식이 `char(11)`이라고 가정할 경우, 아래 쿼리는 `@SSN` 변수의 형식( `nchar(11)`)이 열 형식과 일치하지 않으므로 실패합니다.   

```sql
DECLARE @SSN nchar(11) = '795-73-9838'
SELECT * FROM [dbo].[Patients]
WHERE [SSN] = @SSN;
```

    Msg 402, Level 16, State 2, Line 5   
    The data types char(11) encrypted with (encryption_type = 'DETERMINISTIC', 
    encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'CEK_Auto1', 
    column_encryption_key_database_name = 'Clinic') collation_name = 'Latin1_General_BIN2' 
    and nchar(11) encrypted with (encryption_type = 'DETERMINISTIC', 
    encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'CEK_Auto1', 
    column_encryption_key_database_name = 'Clinic') are incompatible in the equal to operator. 

> [!NOTE]
> 매개 변수화를 사용하지 않으면 형식 변환을 포함하여 전체 쿼리가 SQL Server/Azure SQL Database 내에서 처리됩니다. 매개 변수화를 사용하면 일부 형식 변환이 SQL Server Management Studio 내의 .NET Framework에서 수행됩니다. .NET Framework 형식 시스템과 SQL Server 형식 시스템 간의 차이(예: float와 같은 일부 형식의 정밀도 차이)로 인해 매개 변수화를 사용하여 실행된 쿼리는 매개 변수화를 사용하지 않고 실행된 쿼리와 다른 결과를 생성할 수 있습니다. 

## <a name="next-steps"></a>다음 단계
- [Always Encrypted를 사용하여 애플리케이션 개발](always-encrypted-client-development.md)


## <a name="see-also"></a>참고 항목
- [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
