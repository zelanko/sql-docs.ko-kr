---
title: CREATE EXTERNAL LIBRARY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/05/2018
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
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
author: jeannt
ms.author: jeannt
manager: craigg
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 75da6dff4ff0fe120961376e5b86711fd7162f06
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="create-external-library-transact-sql"></a>CREATE EXTERNAL LIBRARY(Transact-SQL)  

[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]  

R 패키지를 지정된 바이트 스트림 또는 파일 경로에서 데이터베이스에 업로드합니다.

이 명령문은 데이터베이스 관리자가 새 외부 언어 런타임(R, Python, Java 등) 및 [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)]에서 지원되는 OS 플랫폼에 필요한 아티팩트를 업로드하기 위한 일반 메커니즘의 역할을 합니다. 

현재 R 언어 및 Windows 플랫폼만 지원됩니다. Python 및 Linux에 대한 지원은 후속 릴리스에서 계획되어 있습니다.

## <a name="syntax"></a>구문

```text
CREATE EXTERNAL LIBRARY library_name  
    [ AUTHORIZATION owner_name ]  
FROM <file_spec> [,…2]  
WITH ( LANGUAGE = 'R' )  
[ ; ]  

<file_spec> ::=  
{  
(CONTENT = { <client_library_specifier> | <library_bits> }  
[, PLATFORM = WINDOWS ])  
}  

<client_library_specifier> :: =  
  '[\\computer_name\]share_name\[path\]manifest_file_name'  
| '[local_path\]manifest_file_name'  
| '<relative_path_in_external_data_source>'  

<library_bits> :: =  
{ varbinary_literal | varbinary_expression }  
```

### <a name="arguments"></a>인수

**library_name**

라이브러리는 사용자로 범위 지정된 데이터베이스에 추가됩니다. 라이브러리 이름은 특정 사용자 또는 소유자의 컨텍스트 내에서 고유해야 합니다. 예를 들어 두 사용자 **RUser1** 및 **RUser2**는 모두 R 라이브러리 `ggplot2`를 개별적으로 업로드할 수도 있고 따로 업로드할 수도 있습니다. 그러나 **RUser1**이 새 버전의 `ggplot2`를 업로드하려는 경우 두 번째 인스턴스는 이름을 다르게 지정하거나 기존 라이브러리를 대체해야 합니다. 

라이브러리 이름은 임의로 할당될 수 없으며, R에서 R 라이브러리를 로드하는 데 필요한 이름과 같아야 합니다.

**owner_name**

외부 라이브러리를 소유하는 사용자 또는 역할의 이름을 지정합니다. 값을 지정하지 않으면 현재 사용자에게 소유권이 부여됩니다.

데이터베이스 소유자가 소유한 라이브러리는 데이터베이스 및 런타임에 대해 전역인 것으로 간주합니다. 다시 말해서 데이터베이스 소유자는 많은 사용자가 공유하는 라이브러리 또는 패키지의 공통 집합을 포함하는 라이브러리를 만들 수 있습니다. 외부 라이브러리가 `dbo` 사용자 이외의 사용자가 만든 경우, 외부 라이브러리는 해당 사용자 전용입니다.

사용자 **RUser1**이 R 스크립트를 실행하는 경우 `libPath`의 값은 여러 경로를 포함할 수 있습니다. 첫 번째 경로는 언제나 데이터베이스 소유자가 만든 공유 라이브러리에 대한 경로입니다. `libPath`의 두 번째 부분은 **RUser1**에 의해 개별적으로 업로드된 패키지를 포함하는 경로를 지정합니다.

**file_spec**

특정 플랫폼에 대한 패키지의 콘텐츠를 지정합니다. 플랫폼당 한 개의 파일 아티팩트만 지원됩니다.

파일은 로컬 경로 또는 네트워크 경로 형식으로 지정할 수 있습니다.

선택적으로 파일에 대한 OS 플랫폼을 지정할 수 있습니다. 특정 언어 또는 런타임에 대해 각 OS 플랫폼당 한 개의 파일 아티팩트 또는 콘텐츠만 허용됩니다.

**library_bits**

패키지의 콘텐츠를 어셈블리와 유사한 16진수 리터럴로 지정합니다. 

이 옵션은 라이브러리를 만들거나 기존 라이브러리를 변경해야 하지만(그리고 그렇게 하기 위해 필요한 권한을 가지고 있지만) 서버의 파일 시스템이 제한되어 라이브러리 파일을 서버가 액세스할 수 있는 위치에 복사할 수 없는 경우에 유용합니다.

**PLATFORM = WINDOWS**

라이브러리의 콘텐츠에 대한 플랫폼을 지정합니다. 값은 기본적으로 SQL Server가 실행 중인 호스트 플랫폼입니다. 그러므로 사용자는 값을 지정하지 않아도 됩니다. 이는 여러 플랫폼이 지원되거나 사용자가 다른 플랫폼을 지정해야 하는 경우에 필요합니다. 

SQL Server 2017에서는 Windows 플랫폼만 지원됩니다.

## <a name="remarks"></a>Remarks

R 언어의 경우 파일을 사용할 때 패키지를 Windows용 .ZIP 확장명의 압축된 보관 파일 형태로 준비해야 합니다. 현재 Windows 플랫폼만 지원됩니다. 

`CREATE EXTERNAL LIBRARY` 문은 라이브러리 비트를 데이터베이스에 업로드합니다. 라이브러리는 사용자가 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)를 사용하여 외부 스크립트를 실행하고 패키지 또는 라이브러리를 호출할 때 설치됩니다.

인스턴스에 업로드된 라이브러리는 공용 또는 개인일 수 있습니다. 라이브러리가 `dbo`의 멤버에 의해 만들어진 경우, 라이브러리는 공용이며 모든 사용자와 공유될 수 있습니다. 그렇지 않으면 라이브러리는 해당 사용자 개인 전용입니다.

## <a name="permissions"></a>사용 권한

`CREATE EXTERNAL LIBRARY` 권한이 필요합니다. 기본적으로 **db_owner** 역할의 멤버인 **dbo**가 있는 사용자는 외부 라이브러리를 만들 수 있는 권한이 있습니다. 기타 모든 사용자의 경우, 권한으로 CREATE EXTERNAL LIBRARY를 지정하는 [GRANT](https://docs.microsoft.com/sql/t-sql/statements/grant-database-permissions-transact-sql) 문을 사용하여 명시적으로 권한을 부여해야 합니다.

라이브러리를 수정하려면 별도의 권한 `ALTER ANY EXTERNAL LIBRARY`가 필요합니다.

## <a name="examples"></a>예

### <a name="a-add-an-external-library-to-a-database"></a>1. 데이터베이스에 외부 라이브러리 추가  

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

### <a name="b-installing-packages-with-dependencies"></a>2. 종속성이 있는 패키지 설치

설치할 패키지가 종속성을 가지고 있는 경우, 대상 패키지의 설치를 시도하기 _전에_ 첫 번째 수준 종속성과 두 번째 수준 종속성을 모두 분석하고 모든 필요한 패키지를 사용할 수 있도록 해야 합니다.

예를 들어 새 패키지 `packageA`를 설치하려고 한다고 가정합니다.

+ `packageA`는 `packageB`에 대한 종속성이 있음
+ `packageB`는 `packageC`에 대한 종속성이 있음

`packageA`의 설치에 성공하려면 SQL Server에 `packageA`를 추가하는 것과 동시에 `packageB` 및 `packageC`에 대한 라이브러리를 만들어야 합니다. 필요한 패키지 버전도 확인해야 합니다.

실제로 인기 있는 패키지에 대한 패키지 종속성은 대개 이처럼 간단한 예제보다 훨씬 더 복잡합니다. 예를 들어 **ggplot2**에는 30개가 넘는 패키지가 필요할 수 있으며 그러한 패키지에는 서버에서 사용할 수 없는 추가 패키지가 필요할 수 있습니다. 누락된 패키지 또는 잘못된 패키지 버전을 사용하면 설치가 실패할 수 있습니다.

단지 패키지 매니페스트만 조사하여 모든 종속성을 결정하기는 어려울 수 있으므로 [miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html) 같은 패키지를 사용하여 설치를 성공적으로 완료하는 데 필요할 수 있는 모든 패키지를 식별하는 것이 좋습니다.

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
    print(packageVersion("packageA"))
    '
    ```

### <a name="c-create-a-library-from-a-byte-stream"></a>3. 바이트 스트림에서 라이브러리 만들기

패키지 파일을 서버의 위치에 저장하는 기능이 없는 경우 패키지 콘텐츠를 변수에 전달할 수 있습니다. 다음 예제에서는 비트를 16진수 리터럴로 전달하여 라이브러리를 만듭니다.

```SQL
CREATE EXTERNAL LIBRARY customLibrary FROM (CONTENT = 0xabc123) WITH (LANGUAGE = 'R');
```

> [!NOTE]
> 이 코드 샘플은 구문만 보여줍니다. `CONTENT =`의 이진 값은 읽기 쉽도록 잘렸으며, 작업 중인 라이브러리를 생성하지 않습니다. 이진 변수의 실제 콘텐츠는 훨씬 더 깁니다.

### <a name="d-change-an-existing-package-library"></a>4. 기존 패키지 라이브러리 변경

`ALTER EXTERNAL LIBRARY` DDL 문을 사용하여 새 라이브러리 콘텐츠를 추가하거나 기존 라이브러리 콘텐츠를 수정할 수 있습니다. 기존 라이브러리를 수정하려면 별도의 `ALTER ANY EXTERNAL LIBRARY` 권한이 필요합니다.

자세한 내용은 [ALTER EXTERNAL LIBRARY](alter-external-library-transact-sql.md)를 참조하세요.

## <a name="see-also"></a>관련 항목:

[ALTER EXTERNAL LIBRARY(Transact-SQL)](alter-external-library-transact-sql.md)  
[DROP EXTERNAL LIBRARY(Transact-SQL)](drop-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  
