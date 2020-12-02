---
description: FILE_ID(Transact-SQL)
title: FILE_ID (Transact-SQL)| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FILE_ID
- FILE_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IDs [SQL Server], files
- file IDs [SQL Server]
- FILE_ID function
- names [SQL Server], files
- identification numbers [SQL Server], files
- file names [SQL Server], FILE_ID
ms.assetid: 6a7382cf-a360-4d62-b9d2-5d747f56f076
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9cdd99caf69ce254e1a42d345526515d2fb0472f
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96124701"
---
# <a name="file_id-transact-sql"></a>FILE_ID(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

현재 데이터베이스의 구성 요소 파일에 지정된 논리 이름의 경우 이 함수는 파일 ID 번호를 반환합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 대신 [FILE_IDEX](../../t-sql/functions/file-idex-transact-sql.md)를 사용하십시오.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql  
FILE_ID ( file_name )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
*file_name*  
반환될 파일 ID 값 `FILE_ID`가 포함된 파일의 논리적 이름을 나타내는 **sysname** 형식 식입니다.  
  
## <a name="return-types"></a>반환 형식  
**smallint**  
  
## <a name="remarks"></a>설명  
*file_name* 은 sys.master_files 또는 sys.database_files 카탈로그 뷰의 name 열에 표시되는 논리적 파일 이름과 일치합니다.  

*file_name* 이 현재 데이터베이스 구성 요소 파일의 논리적 이름과 일치하지 않으면 `FILE_ID`는 `NULL`을 반환합니다.
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 전체 텍스트 카탈로그에 할당되는 파일 ID 번호는 32767보다 큽니다. `FILE_ID` 함수는 **smallint** 반환 형식이므로 `FILE_ID`는 전체 텍스트 파일을 지원하지 않습니다. 대신 [FILE_IDEX](../../t-sql/functions/file-idex-transact-sql.md)를 사용하십시오.  
  
## <a name="examples"></a>예제  
이 예에서는 `ADVENTUREWORKS2012` 데이터베이스의 구성 요소 파일인 `AdventureWorks_Data` 파일의 파일 ID 값을 반환합니다.  

```sql  
USE AdventureWorks2012;  
GO  
SELECT FILE_ID('AdventureWorks2012_Data')AS 'File ID';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
File ID   
-------   
1  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 2016 이후에는 지원되지 않는 데이터베이스 엔진 기능](../../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)   
 [FILE_NAME&#40;Transact-SQL&#41;](../../t-sql/functions/file-name-transact-sql.md)   
 [메타데이터 함수&#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sys.database_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  
