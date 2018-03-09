---
title: "외부 라이브러리 (Transact SQL) DROP | Microsoft Docs"
ms.custom: 
ms.date: 08/17/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP EXTERNAL LIBRARY
- DROP_EXTERNAL_LIBRARY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DROP EXTERNAL LIBRARY
author: jeannt
ms.author: jeannt
manager: craigg
ms.openlocfilehash: 8c45da28bf795fca50454fde21eb7d2c3c798296
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="drop-external-library-transact-sql"></a>DROP 외부 라이브러리 (Transact SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

기존 패키지 라이브러리를 삭제합니다.

## <a name="syntax"></a>구문  

```
DROP EXTERNAL LIBRARY library_name  
[ AUTHORIZATION owner_name ];  
```

### <a name="arguments"></a>인수

**library_name**

기존 패키지 라이브러리의 이름을 지정합니다.

라이브러리는 사용자에 게 범위가 지정 됩니다. 즉, 라이브러리 이름은 특정 사용자 또는 소유자의 컨텍스트 내에서 고유 간주 됩니다.

**owner_name**

사용자 또는 외부 라이브러리를 소유 하는 역할의 이름을 지정 합니다.

데이터베이스 소유자는 다른 사용자가 만든 라이브러리를 삭제할 수 있습니다.

### <a name="return-values"></a>반환 값

정보 메시지는 문이 성공적으로 반환 됩니다.

## <a name="remarks"></a>주의

다른 달리 `DROP` SQL Server의 문을이 문에 지정할 선택적 권한 부여 절을 지정 합니다. 이 통해 **dbo** 또는 사용자에 게는 **db_owner** 패키지 라이브러리를 삭제 하는 역할은 데이터베이스에서 일반 사용자가 업로드 합니다.

## <a name="examples"></a>예

명명 된 사용자 지정 R 패키지를 추가 `customPackage`, 데이터베이스에:

```sql
CREATE EXTERNAL LIBRARY customPackage 
FROM 'C:\Users\Username\CustomPackages\customPackage.zip';
```

삭제 된 `customPackage` 라이브러리입니다.

```sql
DROP EXTERNAL LIBRARY customPackage <user_name>;
```

## <a name="see-also"></a>참고 항목  
[외부 라이브러리 (Transact SQL) 만들기](create-external-library-transact-sql.md)  
[ALTER 외부 라이브러리 (Transact SQL)](alter-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  

