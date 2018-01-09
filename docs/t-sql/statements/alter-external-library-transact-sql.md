---
title: "외부 라이브러리 (Transact SQL) ALTER | Microsoft Docs"
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
- ALTER EXTERNAL LIBRARY
- ALTER_EXTERNAL_LIBRARY_TSQL
dev_langs: TSQL
helpviewer_keywords: ALTER EXTERNAL LIBRARY
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: e679664f02ffcb08d811a66229a21f1bdaf08077
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="alter-external-library-transact-sql"></a>ALTER 외부 라이브러리 (Transact SQL)  

[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

기존 외부 패키지 라이브러리의 콘텐츠를 수정합니다.

## <a name="syntax"></a>구문

```
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
  '[\\computer_name\]share_name\[path\]manifest_file_name'
| '[local_path\]manifest_file_name'
| '<relative_path_in_external_data_source>'

<library_bits> :: =
{ varbinary_literal | varbinary_expression }
```

### <a name="arguments"></a>인수

**library_name**

기존 패키지 라이브러리의 이름을 지정합니다. 라이브러리는 사용자에 게 범위가 지정 됩니다. 즉, 라이브러리 이름은 특정 사용자 또는 소유자의 컨텍스트 내에서 고유 간주 됩니다.

**owner_name**

사용자 또는 외부 라이브러리를 소유 하는 역할의 이름을 지정 합니다.

**file_spec**

특정 플랫폼에 대 한 패키지의 콘텐츠를 지정합니다. 플랫폼 마다 아티팩트 파일을 하나만 사용할 수 있습니다.

로컬 경로 또는 네트워크 경로 형식의 파일을 지정할 수 있습니다. 데이터 원본 옵션을 지정 하는 경우 파일 이름은에서 참조 하는 컨테이너와 관련 하 여 상대 경로 수는 `EXTERNAL DATA SOURCE`합니다.

필요에 따라 파일에는 OS 플랫폼을 지정할 수 있습니다. 하나의 파일 아티팩트 또는 콘텐츠는 런타임 또는 특정 언어에 대 한 각 운영 체제 플랫폼에 대해 허용 됩니다.

**DATA_SOURCE external_data_source_name =**

라이브러리 파일의 위치를 포함 하는 외부 데이터 원본의 이름을 지정 합니다. 이 위치는 Azure blob 저장소 경로 참조 해야 합니다. 사용 하 여 외부 데이터 원본을 만들려면 [외부 데이터 원본 만들기 (Transact SQL)](create-external-data-source-transact-sql.md)합니다.

> [!IMPORTANT] 
> 현재 SQL Server 2017 릴리스에서 데이터 원본으로 blob 지원 되지 않습니다.

**library_bits**

어셈블리에 유사한 16 진수 리터럴로 패키지의 콘텐츠를 지정합니다. 이 옵션에는 사용자가 필요한 권한이 없는 파일 경로 서버에서 액세스할 수 있는 임의의 폴더로 않지만 경우 라이브러리를 변경 하는 라이브러리를 만들 수 있습니다.

**플랫폼 = WINDOWS**

라이브러리의 콘텐츠에 대 한 플랫폼을 지정합니다. 다른 플랫폼을 추가 하려면 기존 라이브러리를 수정 하는 경우이 값이 필요 합니다. Windows가 지원 되는 유일한 플랫폼입니다.

## <a name="remarks"></a>주의

R 언어에 대 한 패키지를 사용 하 여 압축 된 보관 파일의 형태로 준비 해야는 합니다. Windows 용 ZIP 확장입니다. 현재 Windows 플랫폼만 지원 됩니다.  

`ALTER EXTERNAL LIBRARY` 문이 데이터베이스에만 라이브러리 비트를 업로드 합니다. 실행 될 때까지 사용자는 외부 스크립트를 나중에 실행 하 여 수정 된 라이브러리 실제로 설치 되지 않습니다 [(Transact SQL) sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)합니다.

## <a name="permissions"></a>Permissions

필요는 `ALTER ANY EXTERNAL LIBRARY` 권한. 외부 라이브러리를 만든 사용자는 해당 외부 라이브러리를 변경할 수 있습니다.

## <a name="examples"></a>예

다음 예에서는 라는 customPackage 외부 라이브러리를 수정 합니다.

### <a name="a-replace-the-contents-of-a-library-using-a-file"></a>1. 파일을 사용 하는 라이브러리의 내용을 대체합니다

다음 예제에서는 업데이트 된 비트를 포함 하는 압축 된 파일을 사용 하 여 customPackage 라는 외부 라이브러리를 수정 합니다.

```sql
ALTER EXTERNAL LIBRARY customPackage 
SET 
  (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\customPackage.zip')
WITH (LANGUAGE = 'R');
```  

업데이트 된 라이브러리를 설치 하려면 저장된 프로시저를 실행 `sp_execute_external_script`합니다.

```sql   
EXEC sp_execute_external_script 
@language =N'R', 
@script=N'
# load customPackage
library(customPackage)
# call customPackageFunc
OutputDataSet <- customPackageFunc()
'
WITH RESULT SETS (([result] int));
```

### <a name="b-alter-an-existing-library-using-a-byte-stream"></a>2. 바이트 스트림을 사용 하 여 기존 라이브러리를 변경 합니다.

다음 예제에서는 새 비트 리터럴는 16 진수 값으로 전달 하 여 기존 라이브러리를 변경 합니다.

```SQL
ALTER EXTERNAL LIBRARY customLibrary FROM (CONTENT = 0xabc123) WITH (LANGUAGE = 'R');
```

## <a name="see-also"></a>관련 항목:  

[외부 라이브러리 (Transact SQL) 만들기](create-external-library-transact-sql.md)
[DROP 외부 라이브러리 (Transact SQL)](drop-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  
