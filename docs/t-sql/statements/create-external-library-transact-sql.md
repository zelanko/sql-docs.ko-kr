---
title: "외부 라이브러리 (Transact SQL) 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 10/05/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE EXTERNAL LIBRARY
- CREATE_EXTERNAL_LIBRARY_TSQL
- EXTERNAL LIBRARY
- EXTERNAL_LIBRARY_TSQL
dev_langs: TSQL
helpviewer_keywords: CREATE EXTERNAL LIBRARY
author: jeannt
ms.author: jeannt
manager: craigg
ms.openlocfilehash: fe1cb90bce5717d194defd2c684d7b20fc29a061
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="create-external-library-transact-sql"></a>외부 라이브러리 (Transact SQL) 만들기  

[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]  

데이터베이스에 지정 된 바이트 스트림 또는 파일 경로에서 R 패키지를 업로드합니다.

이 문은 역할에서 지 원하는 운영 체제 플랫폼 및 모든 새 외부 언어 런타임 (R, Python, Java, 등)에 필요한 아티팩트를 업로드 하 고 데이터베이스 관리자는 일반 메커니즘을 [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)]합니다. 현재는 R 언어 및 Windows 플랫폼은 지원 됩니다.

## <a name="syntax"></a>구문

```
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

라이브러리는 사용자에 게 범위를 데이터베이스에 추가 됩니다. 즉, 라이브러리 이름을 특정 사용자 또는 소유자의 컨텍스트 내에서 고유한 것으로 간주 됩니다 및 라이브러리 이름은 사용자별로 고유 해야 합니다. 예를 들어 두 명의 사용자가 **RUser1** 및 **RUser2** 둘 다 개별적으로 고 개별적으로 업로드할 수 R 라이브러리 `ggplot2`합니다.

**owner_name**

사용자 또는 외부 라이브러리를 소유 하는 역할의 이름을 지정 합니다. 값을 지정하지 않으면 현재 사용자에게 소유권이 부여됩니다.

데이터베이스 소유자가 소유한 라이브러리는 데이터베이스 및 런타임 전역으로 간주 됩니다. 즉, 데이터베이스 소유자는 라이브러리 또는 많은 사용자가 공유 하는 패키지는 공통 집합이 포함 된 라이브러리를 만들 수 있습니다. 외부 라이브러리를 만드는 경우 사용자가 아니라는 `dbo` 사용자, 외부 라이브러리는 해당 사용자만 전용입니다.

때 사용자 **RUser1** 값 R 스크립트를 실행할 `libPath` 여러 경로가 포함 될 수 있습니다. 첫 번째 경로 경로 데이터베이스 소유자가 만든 공유 라이브러리를 항상 합니다. 두 번째 부분은 `libPath` 에서 개별적으로 업로드 된 패키지가 포함 된 경로 지정 **RUser1**합니다.

**file_spec**

특정 플랫폼에 대 한 패키지의 콘텐츠를 지정합니다. 플랫폼 마다 아티팩트 파일을 하나만 사용할 수 있습니다.

로컬 경로 또는 네트워크 경로 형식의 파일을 지정할 수 있습니다.

필요에 따라 파일에는 OS 플랫폼을 지정할 수 있습니다. 하나의 파일 아티팩트 또는 콘텐츠는 런타임 또는 특정 언어에 대 한 각 운영 체제 플랫폼에 대해 허용 됩니다.

**library_bits**

어셈블리에 유사한 16 진수 리터럴로 패키지의 콘텐츠를 지정합니다. 이 옵션에는 사용자가 필요한 권한이 없는 파일 경로 서버에서 액세스할 수 있는 임의의 폴더로 않지만 경우 라이브러리를 변경 하는 라이브러리를 만들 수 있습니다.

**플랫폼 = WINDOWS**

라이브러리의 콘텐츠에 대 한 플랫폼을 지정합니다. SQL Server가 실행 되는 호스트 플랫폼 기본값입니다. 따라서 사용자는 값을 지정할 필요가 없습니다. 사용자가을 다른 플랫폼을 지정 해야 하거나 여러 플랫폼을 사용할 수 있는 경우 필수입니다. Windows가 지원 되는 유일한 플랫폼입니다.

## <a name="remarks"></a>주의

R 언어 파일을 사용 하는 경우, 패키지를 사용 하 여 압축 된 보관 파일의 형태로 준비 해야는 합니다. Windows 용 ZIP 확장입니다. 현재 Windows 플랫폼만 지원 됩니다.

`CREATE EXTERNAL LIBRARY` 문이 데이터베이스에만 라이브러리 비트를 업로드 합니다. 실행 될 때까지 사용자는 외부 스크립트를 나중에 실행 하 여 라이브러리 실제로 설치 되지 않습니다 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)합니다.  

인스턴스에 업로드 하는 라이브러리에는 공개 프로필과 개인 수 있습니다. 라이브러리의 멤버에 의해 만들어지면 `dbo`, 라이브러리는 공용 및 모든 사용자와 공유할 수 있습니다. 그렇지 않은 경우 라이브러리는 해당 사용자만의 전용.

SQL Server 2017 릴리스에서 데이터 원본으로 blob을 사용할 수 없습니다.

## <a name="permissions"></a>Permissions

필요는 `CREATE ANY EXTERNAL LIBRARY` 권한.

라이브러리를 수정 하려면 별도 권한 필요 `ALTER ANY EXTERNAL LIBRARY`합니다.

## <a name="examples"></a>예

### <a name="a-add-an-external-library-to-a-database"></a>1. 데이터베이스에 외부 라이브러리를 추가 합니다.  

다음 예제에서는 데이터베이스에 customPackage 라는 외부 라이브러리를 추가 합니다.

```sql
CREATE EXTERNAL LIBRARY customPackage 
FROM 
  (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\customPackage.zip')
WITH (LANGUAGE = 'R');
```  

라이브러리 인스턴스에 업로드 되 면 사용자 실행은 `sp_execute_external_script` 라이브러리를 설치 하려면의 절차입니다.

```sql
EXEC sp_execute_external_script 
@language =N'R', 
@script=N'
# load customPackage
library(customPackage)
'
```

### <a name="b-installing-packages-with-dependencies"></a>2. 종속성 패키지를 설치합니다.

경우 `packageB` 에 종속 `packageA`, 다음 같은 일반 원칙을 따릅니다.

+ 대상 패키지 및 해당 종속성을 모두를 업로드 합니다.

    두 패키지 모두 서버에 액세스할 수 있는 폴더에 있어야 합니다.

    ```sql
    CREATE EXTERNAL LIBRARY packageA 
    FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\packageA.zip') 
    WITH (LANGUAGE = 'R'); 
    
    CREATE EXTERNAL LIBRARY packageB FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\packageB.zip') 
    WITH (LANGUAGE = 'R');
    ```

+ 종속성이 먼저 설치 됩니다.

    필수 패키지 하는 경우 `packageA` 이미 업로드 인스턴스에 그 해야 설치 되지 않은 별도로 합니다. 필수 패키지 `packageA` 때 설치 됩니다. `sp_execute_external_script` 패키지를 설치 하려면 먼저 실행은 `packageB`합니다.

    그러나 경우 필요한 패키지 `packageA`, 사용할 수 없거나, 대상 패키지의 설치 `packageB` 실패 합니다.

    ```sql
    EXEC sp_execute_external_script 
    @language =N'R', 
    @script=N'
    # load packageB
    library(packageB)
    # call customPackageBFunc
    OutputDataSet <- customPackageBFunc()
    '
    with result sets (([result] int));    
    ```

### <a name="c-create-a-library-from-a-byte-stream"></a>3. 바이트 스트림에서 라이브러리 만들기

다음 예에서는 전달 하 여 라이브러리를 만듭니다 리터럴 16으로 bits를 업데이트 합니다.

```SQL
CREATE EXTERNAL LIBRARY customLibrary FROM (CONTENT = 0xabc123) WITH (LANGUAGE = 'R');
```

### <a name="d-change-an-existing-package-library"></a>4. 기존 패키지 라이브러리를 변경 합니다.

`ALTER EXTERNAL LIBRARY` DDL 문을 사용 하 여 새 라이브러리 콘텐츠를 추가 하거나 기존 라이브러리 콘텐츠를 수정할 수 있습니다. 기존 라이브러리를 수정 하려면 필요는 `ALTER ANY EXTERNAL LIBRARY` 권한.

자세한 내용은 참조 [외부 라이브러리 ALTER](alter-external-library-transact-sql.md)합니다.

### <a name="e-delete-a-package-library"></a>5. 패키지 라이브러리 삭제

데이터베이스에서 패키지 라이브러리를 삭제 하는 문을 실행 합니다.

```sql
DROP EXTERNAL LIBRARY customPackage <user_name>;
```

> [!NOTE]
> 다른 달리 `DROP` 에 문을 [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)],이 문은 사용자 권한을 지정 하는 선택적 매개 변수를 지원 합니다. 이 옵션을 사용 하면 일반 사용자가 업로드 되는 라이브러리를 삭제 하려면 소유권 역할이 할당 된 사용자입니다.

## <a name="see-also"></a>참고 항목

[ALTER 외부 라이브러리 (Transact SQL)](alter-external-library-transact-sql.md)  
[DROP 외부 라이브러리 (Transact SQL)](drop-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  
