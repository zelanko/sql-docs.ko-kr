---
title: "외부 라이브러리 (Transact SQL) 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 08/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
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
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0f11a6b7633be392e1f789e12c43f2e5d6e56b47
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-external-library-transact-sql"></a>외부 라이브러리 (Transact SQL) 만들기  
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]  

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

**플랫폼 = WINDOWS**

라이브러리의 콘텐츠에 대 한 플랫폼을 지정합니다. SQL Server가 실행 되는 호스트 플랫폼 기본값입니다. 따라서 사용자는 값을 지정할 필요가 없습니다. 사용자가을 다른 플랫폼을 지정 해야 하거나 여러 플랫폼을 사용할 수 있는 경우 필수입니다. Windows가 지원 되는 유일한 플랫폼입니다.

## <a name="remarks"></a>주의

R 언어에 대 한 패키지를 사용 하 여 압축 된 보관 파일의 형태로 준비 해야는 합니다. Windows 용 ZIP 확장입니다. 현재 Windows 플랫폼만 지원 됩니다.  

`CREATE EXTERNAL LIBRARY` 문이 데이터베이스에만 라이브러리 비트를 업로드 합니다. 실행 될 때까지 사용자는 외부 스크립트를 나중에 실행 하 여 라이브러리 실제로 설치 되지 않습니다 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)합니다.  

## <a name="permissions"></a>Permissions  
필요는 `CREATE EXTERNAL LIBRARY` 권한.  

## <a name="examples"></a>예

### <a name="a-add-an-external-library-to-a-database"></a>1. 데이터베이스에 외부 라이브러리를 추가 합니다.  
다음 예제에서는 데이터베이스에 customPackage 라는 외부 라이브러리를 추가 합니다.   
```sql
CREATE EXTERNAL LIBRARY customPackage 
FROM 
  (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\customPackage.zip')
WITH (LANGUAGE = 'R');
```  
그런 다음 실행에서 `sp_execute_external_script` 라이브러리를 설치 하려면의 절차입니다.  
```sql
EXEC sp_execute_external_script 
@language =N'R', 
@script=N'
# load customPackage
library(customPackage)

# call customPackageFunc
OutputDataSet <- customPackageFunc()
'
with result sets (([result] int));    
```

### <a name="b-installing-packages-with-dependencies"></a>2. 종속성 패키지를 설치합니다.

경우 `packageB` 에 종속 `packageA`, 다음 코드 예를 들어 이러한 일반 원칙을 따릅니다.   
```
CREATE EXTERNAL LIBRARY packageA 
FROM 
  (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\ggplot2.zip') 
WITH (LANGUAGE = 'R'); 

CREATE EXTERNAL LIBRARY packageB FROM 
  (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\ggplot2.zip') 
WITH (LANGUAGE = 'R');
```

`packageA`및 `packageB` 둘 다 설치 시기는 `sp_execute_external_script` 먼저 실행 합니다.   
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

이렇게 하려면 패키지가 저장 되는 폴더를 서버에 액세스할 수 있어야 합니다. 

### <a name="change-an-existing-package-library"></a>기존 패키지 라이브러리를 변경 합니다.

`ALTER EXTERNAL LIBRARY` DDL 문을 사용 하 여 새 라이브러리 콘텐츠를 추가 하거나 기존 라이브러리 콘텐츠를 수정할 수 있습니다.   

### <a name="delete-a-package-library"></a>패키지 라이브러리 삭제

데이터베이스에서 패키지 라이브러리를 삭제 하는 문을 실행 합니다.

```sql
DROP EXTERNAL LIBRARY ggplot2 <user_name>;
```

> [!NOTE]
> 다른 달리 `DROP` 에 문을 [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)],이 문은 사용자 권한을 지정 하는 선택적 매개 변수를 지원 합니다. 이 옵션을 사용 하면 일반 사용자가 업로드 되는 라이브러리를 삭제 하려면 소유권 역할이 할당 된 사용자입니다. 

## <a name="see-also"></a>참고 항목  
[ALTER 외부 라이브러리 (Transact SQL)](alter-external-library-transact-sql.md)  
[DROP 외부 라이브러리 (Transact SQL)](drop-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  

