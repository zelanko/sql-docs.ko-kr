---
description: CREATE EXTERNAL LIBRARY(Transact-SQL) - SQL Server
title: CREATE EXTERNAL LIBRARY(Transact-SQL) - SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 08/26/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: machine-learning
ms.topic: language-reference
f1_keywords:
- CREATE EXTERNAL LIBRARY
- CREATE_EXTERNAL_LIBRARY_TSQL
- EXTERNAL LIBRARY
- EXTERNAL_LIBRARY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE EXTERNAL LIBRARY
author: dphansen
ms.author: davidph
manager: cgronlund
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current'
ms.openlocfilehash: a408cfb25f40ee58c1aeb521c11938026d9241cb
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97439018"
---
# <a name="create-external-library-transact-sql"></a>CREATE EXTERNAL LIBRARY(Transact-SQL)  
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15"
R, Python 또는 Java 패키지 파일을 지정된 바이트 스트림 또는 파일 경로의 데이터베이스에 업로드합니다. 이 명령문은 데이터베이스 관리자가 새 외부 언어 런타임 및 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]에서 지원되는 OS 플랫폼에 필요한 아티팩트를 업로드하기 위한 일반 메커니즘의 역할을 합니다. 

> [!NOTE]
> SQL Server 2017에서는 R 언어 및 Windows 플랫폼이 지원됩니다. Windows 및 Linux 플랫폼의 R, Python 및 외부 언어는 SQL Server 2019 이상에서 지원됩니다.
::: moniker-end

::: moniker range="=azuresqldb-mi-current"
R 또는 Python 패키지 파일을 지정된 바이트 스트림 또는 파일 경로의 데이터베이스에 업로드합니다. 이 문은 데이터베이스 관리자가 필요한 아티팩트를 업로드하기 위한 일반 메커니즘의 역할을 합니다. 

> [!NOTE]
> Azure SQL Managed Instance에서 **sqlmlutils** 를 사용하여 라이브러리를 설치할 수 있습니다. 자세한 내용은 [sqlmlutils를 사용하여 Python 패키지 설치](../../machine-learning/package-management/install-additional-python-packages-on-sql-server.md?context=%252fazure%252fazure-sql%252fmanaged-instance%252fcontext%252fml-context&view=azuresqldb-mi-current) 및 [sqlmlutils를 사용하여 새 R 패키지 설치](../../machine-learning/package-management/install-additional-r-packages-on-sql-server.md?context=%252fazure%252fazure-sql%252fmanaged-instance%252fcontext%252fml-context&view=azuresqldb-mi-current)를 참조하세요.
::: moniker-end

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15"
## <a name="syntax-for-sql-server-2019"></a>SQL Server 2019용 구문

```syntaxsql
CREATE EXTERNAL LIBRARY library_name  
[ AUTHORIZATION owner_name ]  
FROM <file_spec> [ ,...2 ]  
WITH ( LANGUAGE = <language> )  
[ ; ]  

<file_spec> ::=  
{  
    (CONTENT = { <client_library_specifier> | <library_bits> }  
    [, PLATFORM = <platform> ])  
}  

<client_library_specifier> :: = 
{
    '[file_path\]manifest_file_name'  
} 

<library_bits> :: =  
{ 
      varbinary_literal 
    | varbinary_expression 
}

<platform> :: = 
{
      WINDOWS
    | LINUX
}

<language> :: = 
{
      'R'
    | 'Python'
    | <external_language>
}

```
::: moniker-end
::: moniker range=">=sql-server-2017 <=sql-server-2017"
## <a name="syntax-for-sql-server-2017"></a>SQL Server 2017용 구문

```syntaxsql
CREATE EXTERNAL LIBRARY library_name  
[ AUTHORIZATION owner_name ]  
FROM <file_spec> [ ,...2 ]  
WITH ( LANGUAGE = 'R' )  
[ ; ]  

<file_spec> ::=  
{  
    (CONTENT = { <client_library_specifier> | <library_bits> }  
    [, PLATFORM = WINDOWS ])  
}  

<client_library_specifier> :: = 
{
    '[file_path\]manifest_file_name'
} 

<library_bits> :: =  
{ 
      varbinary_literal 
    | varbinary_expression 
}
```
::: moniker-end

::: moniker range="=azuresqldb-mi-current"
## <a name="syntax-for-azure-sql-managed-instance"></a>Azure SQL Managed Instance용 구문

```syntaxsql
CREATE EXTERNAL LIBRARY library_name  
[ AUTHORIZATION owner_name ]  
FROM <file_spec> [ ,...2 ]  
WITH ( LANGUAGE = <language> )  
[ ; ]  

<file_spec> ::=  
{  
    (CONTENT = <library_bits>)  
}  

<library_bits> :: =  
{ 
      varbinary_literal 
    | varbinary_expression 
}

<language> :: = 
{
      'R'
    | 'Python'
}
```
::: moniker-end

### <a name="arguments"></a>인수

**library_name**

인스턴스에 업로드된 라이브러리는 퍼블릭 또는 프라이빗일 수 있습니다. 라이브러리가 `dbo`의 멤버에 의해 만들어진 경우, 라이브러리는 공용이며 모든 사용자와 공유될 수 있습니다. 그렇지 않으면 라이브러리는 해당 사용자에게만 프라이빗으로 제공됩니다.

라이브러리 이름은 특정 사용자 또는 소유자의 컨텍스트 내에서 고유해야 합니다. 예를 들어 두 사용자 **RUser1** 및 **RUser2** 는 모두 R 라이브러리 `ggplot2`를 개별적으로 업로드할 수도 있고 따로 업로드할 수도 있습니다. 그러나 **RUser1** 이 새 버전의 `ggplot2`를 업로드하려는 경우 두 번째 인스턴스는 이름을 다르게 지정하거나 기존 라이브러리를 대체해야 합니다.

라이브러리 이름은 임의로 할당될 수 없으며, 라이브러리 이름은 외부 스크립트에서 라이브러리를 로드하는 데 필요한 이름과 같아야 합니다.

**owner_name**

외부 라이브러리를 소유하는 사용자 또는 역할의 이름을 지정합니다. 값을 지정하지 않으면 현재 사용자에게 소유권이 부여됩니다.

데이터베이스 소유자가 소유한 라이브러리는 데이터베이스 및 런타임에 대해 전역인 것으로 간주합니다. 다시 말해서 데이터베이스 소유자는 많은 사용자가 공유하는 라이브러리 또는 패키지의 공통 집합을 포함하는 라이브러리를 만들 수 있습니다. 외부 라이브러리가 `dbo` 사용자 이외의 사용자가 만든 경우, 외부 라이브러리는 해당 사용자에게만 프라이빗으로 제공됩니다.

사용자 **RUser1** 이 외부 스크립트를 실행하는 경우 `libPath`의 값은 여러 경로를 포함할 수 있습니다. 첫 번째 경로는 언제나 데이터베이스 소유자가 만든 공유 라이브러리에 대한 경로입니다. `libPath`의 두 번째 부분은 **RUser1** 에 의해 개별적으로 업로드된 패키지를 포함하는 경로를 지정합니다.

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15"
**file_spec**

특정 플랫폼에 대한 패키지의 콘텐츠를 지정합니다. 플랫폼당 한 개의 파일 아티팩트만 지원됩니다.

파일은 로컬 경로 또는 네트워크 경로 형식으로 지정할 수 있습니다.

**<client_library_specifier>** 에 지정된 파일에 액세스하려는 경우 SQL Server는 현재 Windows 로그인의 보안 컨텍스트를 가장합니다. **<client_library_specifier>** 에서 네트워크 위치(UNC 경로)를 지정하는 경우에는 위임 제한 때문에 현재 로그인의 가장이 해당 네트워크 위치로 전달되지 않습니다. 이 경우에는 SQL Server 서비스 계정의 보안 컨텍스트를 사용하여 액세스합니다. 자세한 내용은 [자격 증명(데이터베이스 엔진)](../../relational-databases/security/authentication-access/credentials-database-engine.md)을 참조하세요.

선택적으로 파일에 대한 OS 플랫폼을 지정할 수 있습니다. 특정 언어 또는 런타임에 대해 각 OS 플랫폼당 한 개의 파일 아티팩트 또는 콘텐츠만 허용됩니다.
::: moniker-end

**library_bits**

패키지의 콘텐츠를 어셈블리와 유사한 16진수 리터럴로 지정합니다. 

이 옵션은 라이브러리를 만들거나 기존 라이브러리를 변경해야 하지만(그리고 그렇게 하기 위해 필요한 권한을 가지고 있지만) 서버의 파일 시스템이 제한되어 라이브러리 파일을 서버가 액세스할 수 있는 위치에 복사할 수 없는 경우에 유용합니다.

::: moniker range="=sql-server-2017"
**PLATFORM = WINDOWS**

라이브러리의 콘텐츠에 대한 플랫폼을 지정합니다. 값은 기본적으로 SQL Server가 실행 중인 호스트 플랫폼입니다. 그러므로 사용자는 값을 지정하지 않아도 됩니다. 이는 여러 플랫폼이 지원되거나 사용자가 다른 플랫폼을 지정해야 하는 경우에 필요합니다.
SQL Server 2017에서는 Windows 플랫폼만 지원됩니다.
::: moniker-end

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15"
**플랫폼**

라이브러리의 콘텐츠에 대한 플랫폼을 지정합니다. 값은 기본적으로 SQL Server가 실행 중인 호스트 플랫폼입니다. 그러므로 사용자는 값을 지정하지 않아도 됩니다. 이는 여러 플랫폼이 지원되거나 사용자가 다른 플랫폼을 지정해야 하는 경우에 필요합니다.
SQL Server 2019에서는 Windows 및 Linux 플랫폼이 지원됩니다.
::: moniker-end

::: moniker range="=sql-server-2017"
**LANGUAGE = ‘R’**

패키지의 언어를 지정합니다. R은 SQL Server 2017에서 지원됩니다.
::: moniker-end

::: moniker range="=azuresqldb-mi-current"
**language**

패키지의 언어를 지정합니다. Azure SQL Managed Instance에서 이 값은 `R` 또는 `Python`일 수 있습니다.
::: moniker-end

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15"
**language**

패키지의 언어를 지정합니다. 값은 `R`, `Python` 또는 외부 언어의 이름일 수 있습니다([CREATE EXTERNAL LANGUAGE](create-external-language-transact-sql.md) 참조).
::: moniker-end

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="remarks"></a>설명

::: moniker range=">=sql-server-2017 <=sql-server-2017"
R 언어의 경우 파일을 사용할 때 패키지를 Windows용 .ZIP 확장명의 압축된 보관 파일 형태로 준비해야 합니다. 
SQL Server 2017에서는 Windows 플랫폼만 지원됩니다.
::: moniker-end

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15"
R 언어의 경우 파일을 사용할 때 패키지를 .ZIP 확장명의 압축된 보관 파일 형태로 준비해야 합니다.  

Python 언어의 경우 .whl 또는 .zip 파일의 패키지는 압축된 보관 파일 형태로 준비되어야 합니다. 패키지가 이미 .zip 파일이면 새 .zip 파일에 포함되어야 합니다. 패키지를 .whl 또는 .zip 파일로 직접 업로드하는 것은 현재 지원되지 않습니다.
::: moniker-end

`CREATE EXTERNAL LIBRARY` 문은 라이브러리 비트를 데이터베이스에 업로드합니다. 라이브러리는 사용자가 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)를 사용하여 외부 스크립트를 실행하고 패키지 또는 라이브러리를 호출할 때 설치됩니다.

인스턴스에 업로드된 라이브러리는 퍼블릭 또는 프라이빗일 수 있습니다. 라이브러리가 `dbo`의 멤버에 의해 만들어진 경우, 라이브러리는 공용이며 모든 사용자와 공유될 수 있습니다. 그렇지 않으면 라이브러리는 해당 사용자에게만 프라이빗으로 제공됩니다.

시스템 패키지라고 불리는 여러 패키지가 SQL 인스턴스에 미리 설치되어 있습니다. 사용자는 시스템 패키지를 추가, 업데이트, 제거할 수 없습니다.

## <a name="permissions"></a>사용 권한

`CREATE EXTERNAL LIBRARY` 권한이 필요합니다. 기본적으로 **db_owner** 역할의 멤버인 **dbo** 가 있는 사용자는 외부 라이브러리를 만들 수 있는 권한이 있습니다. 기타 모든 사용자의 경우, 권한으로 CREATE EXTERNAL LIBRARY를 지정하는 [GRANT](./grant-database-permissions-transact-sql.md) 문을 사용하여 명시적으로 권한을 부여해야 합니다.

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15"
SQL Server 2019에서 'CREATE EXTERNAL LIBRARY' 권한 외에도 사용자가 해당 외부 언어에 대한 외부 라이브러리를 만들기 위해서는 외부 언어에 대한 참조 권한도 필요합니다.

```sql
GRANT REFERENCES ON EXTERNAL LANGUAGE::Java to user
GRANT CREATE EXTERNAL LIBRARY to user
```

::: moniker-end

모든 라이브러리를 수정하려면 별도의 권한인 `ALTER ANY EXTERNAL LIBRARY`가 필요합니다.

파일 경로를 사용하여 외부 라이브러리를 만들려면 사용자는 Windows 인증 로그인이거나 sysadmin 고정 서버 역할의 멤버여야 합니다.

## <a name="examples"></a>예제

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15"
### <a name="add-an-external-library-to-a-database"></a>데이터베이스에 외부 라이브러리 추가  

다음 예제에서는 `customPackage`라는 외부 라이브러리를 데이터베이스에 추가합니다.

```sql
CREATE EXTERNAL LIBRARY customPackage
FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\customPackage.zip') WITH (LANGUAGE = 'R');
```

라이브러리가 성공적으로 인스턴스에 업로드된 후 사용자는 `sp_execute_external_script` 프로시저를 실행하여 라이브러리를 설치합니다.

```sql
EXEC sp_execute_external_script 
@language =N'R', 
@script=N'library(customPackage)'
```
::: moniker-end

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15"
SQL Server 2019의 Python 언어의 경우, 이 예제는 `'R'`을 `'Python'`으로 대체하여 작동합니다.
::: moniker-end

### <a name="installing-packages-with-dependencies"></a>종속성이 있는 패키지 설치

설치할 패키지가 종속성을 가지고 있는 경우, 대상 패키지의 설치를 시도하기 _전에_ 첫 번째 수준 종속성과 두 번째 수준 종속성을 모두 분석하고 모든 필요한 패키지를 사용할 수 있도록 해야 합니다.

예를 들어 새 패키지 `packageA`를 설치하려고 한다고 가정합니다.

+ `packageA`는 `packageB`에 대한 종속성이 있음
+ `packageB`는 `packageC`에 대한 종속성이 있음

`packageA`의 설치에 성공하려면 SQL Server에 `packageA`를 추가하는 것과 동시에 `packageB` 및 `packageC`에 대한 라이브러리를 만들어야 합니다. 필요한 패키지 버전도 확인해야 합니다.

실제로 인기 있는 패키지에 대한 패키지 종속성은 대개 이처럼 간단한 예제보다 훨씬 더 복잡합니다. 예를 들어 **ggplot2** 에는 30개가 넘는 패키지가 필요할 수 있으며 그러한 패키지에는 서버에서 사용할 수 없는 추가 패키지가 필요할 수 있습니다. 누락된 패키지 또는 잘못된 패키지 버전을 사용하면 설치가 실패할 수 있습니다.

단지 패키지 매니페스트만 조사하여 모든 종속성을 결정하기는 어려울 수 있으므로 [miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html) 같은 패키지를 사용하여 설치를 성공적으로 완료하는 데 필요할 수 있는 모든 패키지를 식별하는 것이 좋습니다.

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15"

+ 대상 패키지 및 해당 종속성 업로드 모든 파일은 서버에 액세스할 수 있는 폴더에 있어야 합니다.

    ```sql
    CREATE EXTERNAL LIBRARY packageA 
    FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\packageA.zip') 
    WITH (LANGUAGE = 'R'); 
    GO

    CREATE EXTERNAL LIBRARY packageB FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\packageB.zip') 
    WITH (LANGUAGE = 'R');
    GO

    CREATE EXTERNAL LIBRARY packageC FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\packageC.zip') 
    WITH (LANGUAGE = 'R');
    GO
    ```

+ 필요한 패키지를 먼저 설치합니다.

    필요한 패키지가 인스턴스에 이미 업로드된 경우 다시 추가할 필요는 없습니다. 기존 패키지가 올바른 버전인지 여부만 확인하면 됩니다. 
    
    `sp_execute_external_script`을 먼저 실행하여 패키지 `packageA`를 설치하면 필요한 패키지 `packageC` 및 `packageB`가 올바른 순서로 설치됩니다.

    그러나 필요한 패키지를 사용할 수 없는 경우 대상 패키지 `packageA`의 설치가 실패합니다.

    ```sql
    EXEC sp_execute_external_script 
    @language =N'R', 
    @script=N'
    # load the desired package packageA
    library(packageA)
    '
    ```
::: moniker-end

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15"
SQL Server 2019의 Python 언어의 경우, 이 예제는 `'R'`을 `'Python'`으로 대체하여 작동합니다.
::: moniker-end

### <a name="create-a-library-from-a-byte-stream"></a>바이트 스트림에서 라이브러리 만들기

패키지 파일을 서버의 위치에 저장하는 기능이 없는 경우 패키지 콘텐츠를 변수에 전달할 수 있습니다. 다음 예제에서는 비트를 16진수 리터럴로 전달하여 라이브러리를 만듭니다.

```SQL
CREATE EXTERNAL LIBRARY customLibrary FROM (CONTENT = 0xABC123...) WITH (LANGUAGE = 'R');
```

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15"
SQL Server 2019의 Python 언어의 경우, 이 예제는 **'R'** 을 **'Python'** 으로 대체하여 작동합니다.
::: moniker-end

> [!NOTE]
> 이 코드 샘플은 구문만 보여줍니다. `CONTENT =`의 이진 값은 읽기 쉽도록 잘렸으며, 작업 중인 라이브러리를 생성하지 않습니다. 이진 변수의 실제 콘텐츠는 훨씬 더 깁니다.

### <a name="change-an-existing-package-library"></a>기존 패키지 라이브러리 변경

`ALTER EXTERNAL LIBRARY` DDL 문을 사용하여 새 라이브러리 콘텐츠를 추가하거나 기존 라이브러리 콘텐츠를 수정할 수 있습니다. 기존 라이브러리를 수정하려면 별도의 `ALTER ANY EXTERNAL LIBRARY` 권한이 필요합니다.

자세한 내용은 [ALTER EXTERNAL LIBRARY](alter-external-library-transact-sql.md)를 참조하세요.

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15"
### <a name="add-a-java-jar-file-to-a-database"></a>데이터베이스에 Java.jar 파일 추가  

다음 예제에서는 `customJar`이라는 외부 jar 파일을 데이터베이스에 추가합니다.

```sql
CREATE EXTERNAL LIBRARY customJar
FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\customJar.jar') 
WITH (LANGUAGE = 'Java');
```

라이브러리가 성공적으로 인스턴스에 업로드된 후 사용자는 `sp_execute_external_script` 프로시저를 실행하여 라이브러리를 설치합니다.

```sql
EXEC sp_execute_external_script
    @language = N'Java'
    , @script = N'customJar.MyCLass.myMethod'
    , @input_data_1 = N'SELECT * FROM dbo.MyTable'
WITH RESULT SETS ((column1 int))
```

### <a name="add-an-external-package-for-both-windows-and-linux"></a>Windows 및 Linux용 외부 패키지 추가

Windows용 하나와 Linux용 하나로 최대 두 개의 `<file_spec>`를 지정할 수 있습니다.

```sql
CREATE EXTERNAL LIBRARY lazyeval 
FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\packageA.zip', PLATFORM = WINDOWS),
(CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\packageA.tar.gz', PLATFORM = LINUX)
WITH (LANGUAGE = 'R')
```

`sp_execute_external_script`를 사용하여 패키지를 설치할 때 SQL Server 인스턴스가 실행 중인 플랫폼에 따라 해당 플랫폼의 라이브러리 콘텐츠가 사용됩니다.

```sql
EXECUTE sp_execute_external_script 
    @LANGUAGE = N'R',
    @SCRIPT = N'
library(packageA)
```
::: moniker-end

## <a name="see-also"></a>참고 항목

[ALTER EXTERNAL LIBRARY(Transact-SQL)](alter-external-library-transact-sql.md)  
[DROP EXTERNAL LIBRARY(Transact-SQL)](drop-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)