---
description: ALTER EXTERNAL LIBRARY(Transact-SQL)
title: ALTER EXTERNAL LIBRARY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/26/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: machine-learning
ms.topic: language-reference
f1_keywords:
- ALTER EXTERNAL LIBRARY
- ALTER_EXTERNAL_LIBRARY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER EXTERNAL LIBRARY
author: dphansen
ms.author: davidph
manager: cgronlund
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: d2a53c17787810aa3ebdd47c64810caab42844c2
ms.sourcegitcommit: bd3a135f061e4a49183bbebc7add41ab11872bae
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92300443"
---
# <a name="alter-external-library-transact-sql"></a>ALTER EXTERNAL LIBRARY(Transact-SQL)  
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

기존 외부 패키지 라이브러리의 콘텐츠를 수정합니다.

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||sqlallproducts-allversions"
> [!NOTE]
> SQL Server 2017에서는 R 언어 및 Windows 플랫폼이 지원됩니다. Windows 및 Linux 플랫폼의 R, Python 및 외부 언어는 SQL Server 2019 이상에서 지원됩니다.
::: moniker-end

::: moniker range="=azuresqldb-mi-current"
> [!NOTE]
> Azure SQL Managed Instance에서 라이브러리를 제거한 다음 **sqlmlutils** 를 사용하여 변경된 버전을 설치하면 라이브러리를 변경할 수 있습니다. **sqlmlutils** 에 대한 자세한 내용은 [sqlmlutils를 사용하여 Python 패키지 설치](../../machine-learning/package-management/install-additional-python-packages-on-sql-server.md?context=%252fazure%252fazure-sql%252fmanaged-instance%252fcontext%252fml-context&view=azuresqldb-mi-current) 및 [sqlmlutils를 사용하여 새 R 패키지 설치](../../machine-learning/package-management/install-additional-r-packages-on-sql-server.md?context=%252fazure%252fazure-sql%252fmanaged-instance%252fcontext%252fml-context&view=azuresqldb-mi-current)를 참조하세요.
::: moniker-end

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
## <a name="syntax-for-sql-server-2019"></a>SQL Server 2019용 구문

```syntaxsql
ALTER EXTERNAL LIBRARY library_name
[ AUTHORIZATION owner_name ]
SET <file_spec>
WITH ( LANGUAGE = <language> )
[ ; ]

<file_spec> ::=
{
    (CONTENT = { <client_library_specifier> | <library_bits> | NONE}
    [, PLATFORM = <platform> )
}

<client_library_specifier> :: =
{
      '[\\computer_name\]share_name\[path\]manifest_file_name'
    | '[local_path\]manifest_file_name'
    | '<relative_path_in_external_data_source>'
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
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
## <a name="syntax-for-sql-server-2017"></a>SQL Server 2017용 구문

```syntaxsql
ALTER EXTERNAL LIBRARY library_name
[ AUTHORIZATION owner_name ]
SET <file_spec>
WITH ( LANGUAGE = 'R' )
[ ; ]

<file_spec> ::=
{
    (CONTENT = { <client_library_specifier> | <library_bits> | NONE}
    [, PLATFORM = WINDOWS )
}

<client_library_specifier> :: =
{
      '[\\computer_name\]share_name\[path\]manifest_file_name'
    | '[local_path\]manifest_file_name'
    | '<relative_path_in_external_data_source>'
}

<library_bits> :: =
{ 
      varbinary_literal 
    | varbinary_expression 
}
```
::: moniker-end

::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
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

기존 패키지 라이브러리의 이름을 지정합니다. 라이브러리 범위는 사용자로 지정됩니다. 라이브러리 이름은 특정 사용자 또는 소유자의 컨텍스트 내에서 고유해야 합니다.

라이브러리 이름은 임의로 할당될 수 없습니다. 즉, 호출 런타임이 패키지를 로드할 때 예상하는 이름을 사용해야 합니다.

**owner_name**

외부 라이브러리를 소유하는 사용자 또는 역할의 이름을 지정합니다.

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions"
**file_spec**

특정 플랫폼에 대한 패키지의 콘텐츠를 지정합니다. 플랫폼당 한 개의 파일 아티팩트만 지원됩니다.

파일은 로컬 경로 또는 네트워크 경로 형식으로 지정할 수 있습니다. 데이터 원본 옵션이 지정된 경우, 파일 이름은 `EXTERNAL DATA SOURCE`에 참조된 컨테이너에 대한 상대 경로일 수 있습니다.

선택적으로 파일에 대한 OS 플랫폼을 지정할 수 있습니다. 특정 언어 또는 런타임에 대해 각 OS 플랫폼당 한 개의 파일 아티팩트 또는 콘텐츠만 허용됩니다.
::: moniker-end

**library_bits**

패키지의 콘텐츠를 어셈블리와 유사한 16진수 리터럴로 지정합니다.

이 옵션은 라이브러리를 변경하기 위해 필요한 권한을 가지고 있지만 서버에 대한 파일 액세스가 제한되어 콘텐츠를 서버에서 액세스할 수 있는 경로에 저장할 수 없는 경우 유용합니다.

그 대신에 패키지 콘텐츠를 이진 형식의 변수로 전달할 수 있습니다.

::: moniker range=">=sql-server-2017 <=sql-server-2017||=sqlallproducts-allversions"
**platform = WINDOWS**

라이브러리의 콘텐츠에 대한 플랫폼을 지정합니다. 이 값은 다른 플랫폼을 추가하기 위해 기존 라이브러리를 수정할 때 필요합니다.
SQL Server 2017에서는 Windows 플랫폼만 지원됩니다.
::: moniker-end

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
**platform**

라이브러리의 콘텐츠에 대한 플랫폼을 지정합니다. 이 값은 다른 플랫폼을 추가하기 위해 기존 라이브러리를 수정할 때 필요합니다. 
SQL Server 2019에서는 Windows 및 Linux 플랫폼이 지원됩니다.
::: moniker-end

::: moniker range=">=sql-server-2017 <=sql-server-2017||=sqlallproducts-allversions"
**LANGUAGE = ‘R’**

패키지의 언어를 지정합니다. R은 SQL Server 2017에서 지원됩니다.
::: moniker-end

::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
**language**

패키지의 언어를 지정합니다. Azure SQL Managed Instance에서 값은 **R** 또는 **Python** 일 수 있습니다.
::: moniker-end

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
**language**

패키지의 언어를 지정합니다. 값은 **R** , **Python** 또는 외부 언어의 이름일 수 있습니다( [CREATE EXTERNAL LANGUAGE](create-external-language-transact-sql.md) 참조).
::: moniker-end

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="remarks"></a>설명

::: moniker range=">=sql-server-2017 <=sql-server-2017||=sqlallproducts-allversions"
R 언어의 경우 패키지를 Windows용 .ZIP 확장명의 압축된 보관 파일 형태로 준비해야 합니다. SQL Server 2017에서는 Windows 플랫폼만 지원됩니다.  
::: moniker-end

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
R 언어의 경우 파일을 사용할 때 패키지를 .ZIP 확장명의 압축된 보관 파일 형태로 준비해야 합니다. 

Python 언어의 경우 .whl 또는 .zip 파일의 패키지는 압축된 보관 파일 형태로 준비되어야 합니다. 패키지가 이미 .zip 파일이면 새 .zip 파일에 포함되어야 합니다. 패키지를 .whl 또는 .zip 파일로 직접 업로드하는 것은 현재 지원되지 않습니다.
::: moniker-end

`ALTER EXTERNAL LIBRARY` 문은 라이브러리 비트를 데이터베이스에 업로드하기만 합니다. 수정된 라이브러리는 사용자가 라이브러리를 호출하는 [sp_execute_external_script(Transact-SQL)](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)의 코드를 실행할 때 설치됩니다.

시스템 패키지라고 불리는 여러 패키지가 SQL 인스턴스에 미리 설치되어 있습니다. 사용자는 시스템 패키지를 추가, 업데이트, 제거할 수 없습니다.

## <a name="permissions"></a>사용 권한

기본적으로 **dbo** 사용자 또는 **db_owner** 역할의 멤버는 ALTER EXTERNAL LIBRARY를 실행할 수 있는 권한이 있습니다. 또한 외부 라이브러리를 만든 사용자가 해당 외부 라이브러리를 변경할 수 있습니다.

## <a name="examples"></a>예제

다음 예제에서는 `customPackage`라는 외부 라이브러리를 변경합니다.

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||sqlallproducts-allversions"
### <a name="replace-the-contents-of-a-library-using-a-file"></a>파일을 사용하여 라이브러리의 콘텐츠 바꾸기

다음 예제에서는 업데이트된 비트가 포함된 압축된 파일을 사용하여 `customPackage`라는 외부 라이브러리를 수정합니다.

```sql
ALTER EXTERNAL LIBRARY customPackage 
SET 
  (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\customPackage.zip')
WITH (LANGUAGE = 'R');
```

업데이트된 라이브러리를 설치하려면 저장 프로시저 `sp_execute_external_script`를 실행합니다.

```sql
EXEC sp_execute_external_script 
@language =N'R', 
@script=N'library(customPackage)'
;
```
::: moniker-end

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Python 언어의 경우 `'R'`을 `'Python'`으로 바꾸면 이 예제가 작동합니다.
::: moniker-end

### <a name="alter-an-existing-library-using-a-byte-stream"></a>바이트 스트림을 사용하여 외부 라이브러리 변경

다음 예제에서는 새 비트를 16진수 리터럴로 전달하여 기존 라이브러리를 변경합니다.

```SQL
ALTER EXTERNAL LIBRARY customLibrary 
SET (CONTENT = 0xABC123...) WITH (LANGUAGE = 'R');
```

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions"
Python 언어의 경우 `'R'`을 `'Python'`으로 바꾸면 이 예제가 작동합니다.
::: moniker-end

> [!NOTE]
> 이 코드 샘플은 구문만 보여줍니다. `CONTENT =`의 이진 값은 읽기 쉽도록 잘렸으며, 작업 중인 라이브러리를 생성하지 않습니다. 이진 변수의 실제 콘텐츠는 훨씬 더 깁니다.

## <a name="see-also"></a>참고 항목

[CREATE EXTERNAL LIBRARY(Transact-SQL)](create-external-library-transact-sql.md)  
[DROP EXTERNAL LIBRARY(Transact-SQL)](drop-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)