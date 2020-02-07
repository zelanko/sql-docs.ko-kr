---
title: Transact-SQL을 사용하여 내부 열 암호화 구성 | Microsoft Docs
ms.custom: ''
ms.date: 10/10/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: b7e8118dc6404bf0f23422e030737403857367d8
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "73595568"
---
# <a name="configure-column-encryption-in-place-with-transact-sql"></a>Transact-SQL을 사용하여 내부 열 암호화 구성
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

이 문서에서는 [ALTER TABLE](../../../odbc/microsoft/alter-table-statement.md)/`ALTER COLUMN` 문으로 보안 enclave를 사용한 Always Encrypted를 이용하여 열에서 내부 암호화 작업을 수행하는 방법을 설명합니다. 내부 암호화 및 일반적인 필수 구성 요소에 대한 기본 정보는 [보안 enclave를 사용한 Always Encrypted를 이용하여 내부 열 암호화 구성](always-encrypted-enclaves-configure-encryption.md)을 참조하세요.

`ALTER TABLE` 또는 `ALTER COLUMN` 문을 사용하여 열에 대상 암호화 구성을 설정할 수 있습니다. 이 문을 실행하면 서버 쪽 보안 enclave는 문의 열 정의에 지정된 현재 및 대상 암호화 구성에 따라 열에 저장된 데이터를 암호화, 다시 암호화 또는 암호 해독합니다. 
- 열이 암호화되어 있지 않은 경우, 열 정의에 `ENCRYPTED WITH` 절을 지정하면 암호화됩니다.
- 열이 암호화되어 있는 경우, 열 정의에 `ENCRYPTED WITH` 절을 지정하지 않으면 해당 열이 암호 해독됩니다(일반 텍스트 열로 변환됨).
- 열이 암호화되어 있는 경우, `ENCRYPTED WITH` 절을 지정하고 지정된 열 암호화 유형 또는 열 암호화 키가 현재 사용된 암호화 유형 또는 열 암호화 키와 다르면 열이 다시 암호화됩니다. 

> [!NOTE]
> 열을 `NULL` 또는 `NOT NULL`로 변경하거나 데이터 정렬을 변경하는 경우를 제외하고. 단일 `ALTER TABLE`/`ALTER COLUMN` 문에서 암호화 작업을 다른 변경과 결합할 수 없습니다. 예를 들어 단일 `ALTER TABLE`/`ALTER COLUMN` Transact-SQL 문에서 열을 암호화하는 동시에 데이터 형식을 변경할 수는 없습니다. 두 개의 개별 문을 사용합니다.

서버 쪽 보안 enclave를 사용하는 모든 쿼리와 마찬가지로 내부 암호화를 트리거하는 `ALTER TABLE`/`ALTER COLUMN` 문은 Always Encrypted 및 enclave 계산을 사용하는 연결을 통해 보내야 합니다. 

이 문서의 나머지 부분에서는 SQL Server Management Studio에서 `ALTER TABLE`/`ALTER COLUMN` 문을 사용하여 내부 암호화를 트리거하는 방법을 설명합니다. 또는 애플리케이션에서 `ALTER TABLE`/`ALTER COLUMN`을 실행할 수 있습니다. 

> [!NOTE]
> 현재, SqlServer PowerShell 모듈의 [Invoke-Sqlcmd](https://docs.microsoft.com/powershell/module/sqlserver/invoke-sqlcmd) cmdlet, [sqlcmd](../../../tools/sqlcmd-utility.md) 등 SSMS 이외의 도구는 내부 암호화 작업에 `ALTER TABLE`/`ALTER COLUMN`를 사용하도록 지원하지 않습니다.

## <a name="perform-in-place-encryption-with-transact-sql-in-ssms"></a>SSMS에서 Transact-SQL을 사용하여 내부 암호화 수행
### <a name="pre-requisites"></a>필수 구성 요소
- [보안 enclave를 사용한 Always Encrypted를 이용하여 내부 열 암호화 구성](always-encrypted-enclaves-configure-encryption.md)에 설명된 필수 구성 요소
- SQL Server Management Studio 18.3 이상

### <a name="steps"></a>단계
1. 데이터베이스 연결에서 Always Encrypted 및 enclave 계산을 사용하도록 설정하여 쿼리 창을 엽니다. 자세한 내용은 [데이터베이스 연결에 Always Encrypted 사용 및 사용 안 함](always-encrypted-query-columns-ssms.md#en-dis)을 참조하세요.
2. 쿼리 창에서 `ENCRYPTED WITH` 절에 enclave 사용 열 암호화 키를 지정하여 `ALTER TABLE`/`ALTER COLUMN` 문을 실행합니다. 열이 문자열 열(예: `char`, `varchar`, `nchar`, `nvarchar`)인 경우에도 데이터 정렬을 BIN2 데이터 정렬로 변경해야 할 수 있습니다. 
    
    > [!NOTE]
    > 열 마스터 키가 Azure Key Vault에 저장된 경우 Azure에 로그인하라는 메시지가 표시될 수 있습니다.

3. 테이블에 액세스하는 모든 일괄 처리 및 저장 프로시저의 계획 캐시를 지워 매개 변수 암호화 정보를 새로 고칩니다. 
 
    ```sql
    ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
    ```
    > [!NOTE]
    > 영향을 받는 쿼리 계획을 캐시에서 제거하지 않으면 암호화 후 첫 번째 쿼리 실행이 실패할 수 있습니다.

    > [!NOTE]
    > 쿼리 성능이 일시적으로 저하될 수 있으므로 `ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE` 또는 `DBCC FREEPROCCACHE`를 사용하여 계획 캐시를 신중하게 지웁니다. 캐시를 지울 때 나타나는 부정적인 영향을 최소화하기 위해 영향을 받는 쿼리 계획만 선택적으로 제거할 수 있습니다.

4.  [sp_refresh_parameter_encryption](../../system-stored-procedures/sp-refresh-parameter-encryption-transact-sql.md)을 호출하여 [sys.parameters](../..//system-catalog-views/sys-parameters-transact-sql.md)에 보관되었으며 열 암호화로 인해 무효화되었을 수 있는 각 모듈(저장 프로시저, 함수, 뷰, 트리거)의 매개 변수 메타데이터를 업데이트합니다.

### <a name="examples"></a>예
#### <a name="encrypting-a-column-in-place"></a>내부 열 암호화
아래 예제에서는 다음을 가정합니다.
- `CEK1`은 enclave 사용 열 암호화 키입니다.
- `SSN` 열은 일반 텍스트이며 현재 Latin1, 비 BIN2 데이터 정렬(예: `Latin1_General_CI_AI_KS_WS`)과 같은 기본 데이터베이스 데이터 정렬을 사용하고 있습니다.

이 문은 임의 암호화 및 enclave 사용 열 암호화 키를 사용하여 `SSN` 열을 내부에서 암호화합니다. 또한 기본 데이터베이스 데이터 정렬을 해당(동일한 코드 페이지) BIN2 데이터 정렬로 덮어씁니다.

이 작업은 온라인으로 수행됩니다(`ONLINE = ON`). 또한 테이블 스키마 변경의 영향을 받는 쿼리 계획을 다시 만드는 `ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE` 호출도 진행됩니다.

```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char] COLLATE Latin1_General_BIN2
ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
WITH
(ONLINE = ON);
GO
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
GO
```

#### <a name="re-encrypt-a-column-in-place-to-change-encryption-type"></a>암호화 유형 변경을 위해 전체 열 다시 암호화
아래 예제에서는 다음을 가정합니다.
- `SSN` 열은 결정적 암호화와 enclave 사용 열 암호화 키 `CEK1`를 사용하여 암호화됩니다.
- 열 수준에서 설정된 현재 데이터 정렬은 `Latin1_General_BIN2`입니다.

아래 문은 임의 암호화와 동일한 키(`CEK1`)를 사용하여 열을 다시 암호화합니다.

```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char](11) COLLATE Latin1_General_BIN2
ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1]
, ENCRYPTION_TYPE = Randomized
, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL;
GO
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
GO
```

#### <a name="re-encrypt-a-column-in-place-to-rotate-a-column-encryption-key"></a>열 암호화 키 순환을 위해 전체 열을 다시 암호화
아래 예제에서는 다음을 가정합니다.
- `SSN` 열은 임의 암호화와 enclave 사용 열 암호화 키 `CEK1`를 사용하여 암호화됩니다.
- `CEK2`은 enclave 사용 열 암호화 키입니다(`CEK1`과 다름).
- 열 수준에서 설정된 현재 데이터 정렬은 `Latin1_General_BIN2`입니다.

아래 문은 `CEK2`를 사용하여 열을 다시 암호화합니다.

```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char](11) COLLATE Latin1_General_BIN2
ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK2]
, ENCRYPTION_TYPE = Randomized
, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL;
GO
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
GO
```
#### <a name="decrypt-a-column-in-place"></a>열 바로 암호 해독
아래 예제에서는 다음을 가정합니다.
- `SSN`은 enclave 사용 열 암호화 키를 사용하여 암호화됩니다.
- 열 수준에서 설정된 현재 데이터 정렬은 `Latin1_General_BIN2`입니다.

아래 문은 열의 암호를 해독합니다. (데이터 정렬은 그대로 유지됩니다. 하지만 같은 문에서 데이터 정렬을 예를 들어 비 BIN2 데이터 정렬로 변경하도록 선택할 수 있습니다.)

```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char](11) COLLATE Latin1_General_BIN2
WITH (ONLINE = ON);
GO
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
GO
```

## <a name="next-steps"></a>다음 단계
- [보안 Enclave를 사용한 Always Encrypted를 사용하여 열 쿼리](always-encrypted-enclaves-query-columns.md)
- [보안 Enclave를 사용한 Always Encrypted를 사용하여 열에 인덱스 만들기 및 사용](always-encrypted-enclaves-create-use-indexes.md)
- [보안 enclave를 사용한 Always Encrypted를 이용하여 애플리케이션 개발](always-encrypted-enclaves-client-development.md)

## <a name="see-also"></a>참고 항목  
- [보안 enclave를 사용한 Always Encrypted를 이용하여 내부 열 암호화 구성](always-encrypted-enclaves-configure-encryption.md)
- [기존 암호화된 열에 관해 보안 Enclave를 사용한 Always Encrypted 사용](always-encrypted-enclaves-enable-for-encrypted-columns.md)
- [자습서: SSMS를 사용하여 보안 Enclave를 사용한 Always Encrypted 시작](../tutorial-getting-started-with-always-encrypted-enclaves.md)