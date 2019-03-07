---
title: DROP EXTERNAL LIBRARY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP EXTERNAL LIBRARY
- DROP_EXTERNAL_LIBRARY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DROP EXTERNAL LIBRARY
author: dphansen
ms.author: davidph
manager: cgronlund
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 129aafce2e270f85506d056d5d083d34176aa8a0
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57018019"
---
# <a name="drop-external-library-transact-sql"></a>DROP EXTERNAL LIBRARY(Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

기존 패키지 라이브러리를 삭제합니다. 패키지 라이브러리는 지원되는 외부 런타임(예: R, Python 또는 Java)에서 사용합니다.

> [!NOTE]
> SQL Server 2017에서는 R 언어 및 Windows 플랫폼이 지원됩니다. Windows 플랫폼의 R, Python 및 Java는 SQL Server 2019 CTP 2.3에서 지원됩니다. Linux에 대한 지원은 후속 릴리스에서 계획되어 있습니다.

## <a name="syntax"></a>구문

```sql
DROP EXTERNAL LIBRARY library_name
[ AUTHORIZATION owner_name ];
```

### <a name="arguments"></a>인수

**library_name**

기존 패키지 라이브러리의 이름을 지정합니다.

라이브러리 범위는 사용자로 지정됩니다. 라이브러리 이름은 특정 사용자 또는 소유자의 컨텍스트 내에서 고유해야 합니다.

**owner_name**

외부 라이브러리를 소유하는 사용자 또는 역할의 이름을 지정합니다.

데이터베이스 소유자는 다른 사용자가 만든 라이브러리를 삭제할 수 있습니다.

## <a name="permissions"></a>Permissions

라이브러리를 삭제하려면 ALTER ANY EXTERNAL LIBRARY 권한이 필요합니다. 기본적으로 모든 데이터베이스 소유자 또는 개체 소유자는 외부 라이브러리도 삭제할 수 있습니다.

### <a name="return-values"></a>반환 값

정보 메시지는 명령문이 성공한 경우 반환됩니다.

## <a name="remarks"></a>Remarks

SQL Server의 `DROP` 문과 달리 이 명령문은 옵션 인증 절 지정을 지원합니다. 이를 통해 **dbo** 또는 **db_owner** 역할의 사용자는 데이터베이스의 일반 사용자가 업로드한 패키지 라이브러리를 삭제할 수 있습니다.

## <a name="examples"></a>예

데이터베이스에 사용자 지정 R 패키지 `customPackage`를 추가합니다.

```sql
CREATE EXTERNAL LIBRARY customPackage 
FROM (CONTENT = 'C:\temp\customPackage_v1.1.zip')
WITH (LANGUAGE = 'R');
GO
```

`customPackage` 라이브러리를 삭제합니다.

```sql
DROP EXTERNAL LIBRARY customPackage;
```

## <a name="see-also"></a>관련 항목:

[CREATE EXTERNAL LIBRARY(Transact-SQL)](create-external-library-transact-sql.md)  
[ALTER EXTERNAL LIBRARY(Transact-SQL)](alter-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  

