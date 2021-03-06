---
description: CREATE EXTERNAL LANGUAGE(Transact-SQL) - SQL Server
title: CREATE EXTERNAL LANGUAGE(Transact-SQL) - SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 04/03/2020
ms.prod: sql
ms.technology: language-extensions
ms.topic: language-reference
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15'
ms.openlocfilehash: 826265f7d04ac96c3e2c9dcdc4a144bb1ca382c8
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97439008"
---
# <a name="create-external-language-transact-sql"></a>CREATE EXTERNAL LANGUAGE(Transact-SQL)
[!INCLUDE [SQL Server 2019 and later](../../includes/applies-to-version/sqlserver2019.md)]

지정된 파일 경로 또는 바이트 스트림에서 데이터베이스의 외부 언어 확장을 등록합니다. 이 명령문은 데이터베이스 관리자가 SQL Server에서 지원되는 OS 플랫폼에 새 외부 언어를 등록하는 일반 메커니즘의 역할을 합니다. 자세한 내용은 [언어 확장](../../language-extensions/language-extensions-overview.md)을 참조하세요.

> [!NOTE]
> **R** 및 **Python** 은 예약된 이름이며 해당 특정 이름을 사용하여 외부 언어를 만들 수 없습니다. **R** 및 **Python** 사용 방법에 대한 자세한 내용은 [SQL Server Machine Learning Services](../../machine-learning/index.yml)를 참조하세요.

## <a name="syntax"></a>구문

```syntaxsql
CREATE EXTERNAL LANGUAGE language_name  
[ AUTHORIZATION owner_name ]  
FROM <file_spec> [ ,...2 ]  
[ ; ]  

<file_spec> ::=  
{
    ( CONTENT = { <external_lang_specifier> | <content_bits> },
    FILE_NAME = <external_lang_file_name>
    [ , PLATFORM = <platform> ]
    [ , PARAMETERS = <external_lang_parameters> ]
    [ , ENVIRONMENT_VARIABLES = <external_lang_env_variables> ] )
}

<external_lang_specifier> :: =  
{
    '[file_path\]os_file_name'  
}

<content_bits> :: =  
{
    varbinary_literal
    | varbinary_expression
}

<external_lang_file_name> :: =  
'extension_file_name'


<platform> :: =
{
    WINDOWS
  | LINUX
}

<external_lang_parameters> :: =  
'extension_specific_parameters'
```

### <a name="arguments"></a>인수

**language_name**

언어는 데이터베이스 범위 개체입니다. 언어 이름은 데이터베이스 내에서 고유해야 합니다.

**owner_name**

외부 언어를 소유하는 사용자 또는 역할의 이름을 지정합니다. 값을 지정하지 않으면 현재 사용자에게 소유권이 부여됩니다. 사용 권한에 따라 다른 사용자가 특정 언어를 사용하여 스크립트를 실행하는 명시적 사용 권한을 부여받아야 할 수 있습니다.

**file_spec**

언어 확장의 콘텐츠를 지정합니다. 플랫폼에 따라 특정 언어에 대해 filespec이 한 개만 허용됩니다.

**external_lang_specifier**

확장 코드가 포함된 .zip 또는 tar.gz 파일에 대한 전체 파일 경로입니다. 이 콘텐츠는 .zip 파일(Windows의 경우) 또는 tar.gz(Linux의 경우)에 대한 경로가 될 수 있습니다.

**content_bits**

언어의 콘텐츠를 어셈블리와 유사한 16진수 리터럴로 지정합니다.

이 옵션은 언어를 만들거나 기존 언어를 변경해야 하지만(그리고 그렇게 하기 위해 필요한 사용 권한을 가지고 있지만) 서버의 파일 시스템이 제한되어 라이브러리 파일을 서버가 액세스할 수 있는 위치에 복사할 수 없는 경우에 유용합니다.

**external_lang_file_name**

확장명 .dll 또는 .so 파일의 이름입니다. 이 이름은 올바른 파일을 식별하기 위해 필요하며, 이 경우 <external_lang_specifier> .zip 또는 tar.gz에 여러 개의 .dll 또는 .so 파일이 있습니다.

**external_lang_parameters**

이 인수를 통해 외부 언어 런타임에 대한 매개 변수 세트를 지정할 수 있습니다. 매개 변수 값은 외부 프로세스가 시작된 후 외부 런타임에 제공됩니다. 그러나 환경 변수는 외부 프로세스가 시작하기 전에 언어 확장에서 액세스할 수 있습니다.

**external_lang_env_variables**

이 인수를 통해 외부 프로세스가 시작하기 전에 외부 언어 런타임에 환경 변수 세트를 지정할 수 있습니다. 환경 변수의 예로 런타임 자체의 홈 디렉터리가 있습니다. 다음은 그 예입니다.  JRE_HOME.

**platform**

이 매개 변수는 하이브리드 OS 시나리오에 필요합니다. 하이브리드 아키텍처에서 언어는 플랫폼당 한 번 등록해야 합니다. 플랫폼 및 언어 이름은 외부 언어마다 고유한 키입니다. 플랫폼을 지정하지 않으면 현재 OS를 가정합니다.

## <a name="permissions"></a>사용 권한

`CREATE EXTERNAL LANGUAGE` 권한이 필요합니다. 기본적으로 **db_owner** 역할의 멤버인 **dbo** 가 있는 사용자는 외부 언어를 만들 사용 권한이 있습니다. 기타 모든 사용자의 경우, 권한으로 CREATE EXTERNAL LIBRARY를 지정하는 [GRANT](./grant-database-permissions-transact-sql.md) 문을 사용하여 명시적으로 권한을 부여해야 합니다.

라이브러리를 수정하려면 별도의 권한 `ALTER ANY EXTERNAL LANGUAGE`가 필요합니다.

### <a name="execute-external-script-permission"></a>EXECUTE EXTERNAL SCRIPT 사용 권한

EXECUTE EXTERNAL SCRIPT 권한을 사용하여 특정 언어에 대한 외부 스크립트 실행 권한을 부여할 수 있습니다. 이는 특정 언어에 대한 실행 권한을 부여할 수 없는 EXECUTE ANY EXTERNAL SCRIPT 데이터베이스 사용 권한과는 다릅니다.

즉, **dbo** 이외의 사용자는 특정 언어를 실행하려면 사용 권한을 부여받아야 합니다.

```sql
GRANT EXECUTE EXTERNAL SCRIPT ON EXTERNAL LANGUAGE ::language_name 
TO database_principal_name;
```

### <a name="reference-permissions-to-external-libraries"></a>외부 라이브러리에 대한 참조 사용 권한

어셈블리와 마찬가지로 외부 언어에 대해서는 외부 라이브러리와 외부 언어 간의 링크가 있도록 하기 위해 참조 사용 권한이 필요합니다. 예를 들어 외부 언어가 삭제될 예정인 경우 먼저 사용자가 해당 언어를 참조하는 모든 외부 라이브러리가 삭제되었는지 확인해야 합니다. 외부 언어를 계층의 외부 라이브러리가 아닌 더 높은 개체로 볼 수 있습니다.

## <a name="examples"></a>예

### <a name="a-create-an-external-language-in-a-database"></a>A. 데이터베이스에 외부 언어 만들기  

다음 예제는 Windows에서 SQL Server의 데이터베이스에 외부 언어가 호출한 Java를 추가합니다.

```sql
CREATE EXTERNAL LANGUAGE Java 
FROM (CONTENT = N'<path-to-zip>', FILE_NAME = 'javaextension.dll');
GO
```

### <a name="b-create-an-external-language-for-both-windows-and-linux"></a>B. Windows 및 Linux 겸용 외부 언어 만들기

Windows용 하나와 Linux용 하나로 최대 두 개의 `<file_spec>`를 지정할 수 있습니다.

```sql
CREATE EXTERNAL LANGUAGE Java
FROM
(CONTENT = N'<path-to-zip>', FILE_NAME = 'javaextension.dll', PLATFORM = WINDOWS),
(CONTENT = N'<path-to-tar.gz>', FILE_NAME = 'javaextension.so', PLATFORM = LINUX);
GO
```
### <a name="c-grant-permissions-to-execute-external-script"></a>C. 외부 스크립트 실행 권한 부여

다음 예제에서는 **Java** 외부 언어를 사용하여 스크립트를 실행할 수 있도록 **mylogin** 에 보안 주체 액세스 권한을 부여합니다.

```sql
GRANT EXECUTE EXTERNAL SCRIPT ON EXTERNAL LANGUAGE ::Java 
TO mylogin;
```


## <a name="see-also"></a>참고 항목

[ALTER EXTERNAL LANGUAGE(Transact-SQL)](alter-external-language-transact-sql.md)  
[DROP EXTERNAL LANGUAGE(Transact-SQL)](drop-external-language-transact-sql.md)  
[sys.external_languages](../../relational-databases/system-catalog-views/sys-external-languages-transact-sql.md)  
[sys.external_language_files](../../relational-databases/system-catalog-views/sys-external-language-files-transact-sql.md)