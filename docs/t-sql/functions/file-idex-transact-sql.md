---
title: FILE_IDEX(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- FILE_IDEX
- FILE_IDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- FILE_IDEX function
- IDs [SQL Server], files
- file IDs [SQL Server]
- names [SQL Server], files
- identification numbers [SQL Server], files
- file names [SQL Server], FILE_IDEX
ms.assetid: 7532fea5-ee5e-4edd-b98b-111a7ba56c8e
caps.latest.revision: 35
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 54224c2b6f977f21764553ceddfb7e7be5fd10c7
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/04/2018
ms.locfileid: "37788364"
---
# <a name="fileidex-transact-sql"></a>FILE_IDEX(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

현재 데이터베이스의 데이터, 로그 또는 전체 텍스트 파일에 지정된 논리적 파일 이름에 대한 파일 ID를 반환합니다.  
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
FILE_IDEX ( file_name )  
```  
  
## <a name="arguments"></a>인수  
 *file_name*  
 파일 ID를 반환할 파일의 이름을 나타내는 **sysname** 형식의 식입니다.  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
 오류 발생 시 **NULL**  
  
## <a name="remarks"></a>Remarks  
 *file_name*은 [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md) 또는 [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md) 카탈로그 뷰의 **name** 열에 표시되는 논리적 파일 이름과 일치합니다.  
  
 FILE_IDEX는 SELECT 목록, WHERE 절 또는 식이 사용되는 곳은 어디에나 사용될 수 있습니다. 자세한 내용은 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)을 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-retrieving-the-file-id-of-a-specified-file"></a>1. 지정된 파일의 파일 ID 검색  
다음 예에서는 `AdventureWorks_Data` 파일의 파일 ID를 반환합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT FILE_IDEX('AdventureWorks2012_Data') AS 'File ID';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
File ID   
-------   
1  
(1 row(s) affected)  
```  
  
### <a name="b-retrieving-the-file-id-when-the-file-name-is-not-known"></a>2. 파일 이름이 알려지지 않은 경우 파일 ID 검색  
다음 예에서는 `sys.database_files` 카탈로그 뷰에서 파일 형식이 `1`(로그)인 논리적 파일 이름을 선택하여 `AdventureWorks` 로그 파일의 파일 ID를 반환합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT FILE_IDEX((SELECT TOP (1) name FROM sys.database_files WHERE type = 1)) AS 'File ID';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
File ID   
-------   
2  
```  
  
### <a name="c-retrieving-the-file-id-of-a-full-text-catalog-file"></a>3. 전체 텍스트 카탈로그 파일의 파일 ID 검색  
다음 예에서는 `sys.database_files` 카탈로그 뷰에서 파일 형식이 `4`(전체 텍스트)인 논리적 파일 이름을 선택하여 전체 텍스트 파일의 파일 ID를 반환합니다. 이 예에서는 전체 텍스트 카탈로그가 없을 경우 NULL을 반환합니다.  
  
```sql  
SELECT FILE_IDEX((SELECT name FROM sys.master_files WHERE type = 4))  
AS 'File_ID';  
```  
  
## <a name="see-also"></a>참고 항목  
 [메타데이터 함수&#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sys.database_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  
