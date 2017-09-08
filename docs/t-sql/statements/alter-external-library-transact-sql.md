---
title: "외부 라이브러리 (Transact SQL) ALTER | Microsoft Docs"
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
- ALTER EXTERNAL LIBRARY
- ALTER_EXTERNAL_LIBRARY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER EXTERNAL LIBRARY
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 541419770828e01cca82fb33ead1b22170f8e4f3
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="alter-external-library-transact-sql"></a>ALTER 외부 라이브러리 (Transact SQL)  
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]  

기존 라이브러리 콘텐츠를 수정합니다.  

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

**플랫폼 = WINDOWS**

라이브러리의 콘텐츠에 대 한 플랫폼을 지정합니다. 다른 플랫폼을 추가 하려면 기존 라이브러리를 수정 하는 경우이 값이 필요 합니다. Windows가 지원 되는 유일한 플랫폼입니다.

## <a name="remarks"></a>주의

R 언어에 대 한 패키지를 사용 하 여 압축 된 보관 파일의 형태로 준비 해야는 합니다. Windows 용 ZIP 확장입니다. 현재 Windows 플랫폼만 지원 됩니다.  
`ALTER EXTERNAL LIBRARY` 문이 데이터베이스에만 라이브러리 비트를 업로드 합니다. 실행 될 때까지 사용자는 외부 스크립트를 나중에 실행 하 여 수정 된 라이브러리 실제로 설치 되지 않습니다 [(Transact SQL) sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)합니다.

## <a name="permissions"></a>Permissions
필요는 `ALTER ANY EXTERNAL LIBRARY` 권한. 외부 라이브러리를 만든 사용자는 해당 외부 라이브러리를 변경할 수 있습니다.

## <a name="examples"></a>예

다음 예제에서는 customPackage 라는 외부 라이브러리를 수정 합니다.

```sql  
ALTER EXTERNAL LIBRARY customPackage 
SET 
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


## <a name="see-also"></a>참고 항목  
[외부 라이브러리 (Transact SQL) 만들기](create-external-library-transact-sql.md)
[DROP 외부 라이브러리 (Transact SQL)](drop-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  

