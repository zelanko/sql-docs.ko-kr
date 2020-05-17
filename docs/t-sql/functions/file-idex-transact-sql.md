---
title: FILE_IDEX(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 59b44b3356a0f71074543eb35107040ff8c47982
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68071500"
---
# <a name="file_idex-transact-sql"></a>FILE_IDEX(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

이 함수는 현재 데이터베이스의 데이터, 로그 또는 전체 텍스트 파일의 지정된 논리적 이름에 대한 파일 ID를 반환합니다. 
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
FILE_IDEX ( file_name )  
```  
  
## <a name="arguments"></a>인수  
 *file_name*  
파일 이름에 대해 파일 ID 값 ‘FILE_IDEX’를 반환하는 **sysname** 형식의 식입니다. 
  
## <a name="return-types"></a>반환 형식  
**int**  
  
오류 발생 시 **NULL**  
  
## <a name="remarks"></a>설명  
*file_name*은 **sys.master_files** 또는 [sys.database_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md) 카탈로그 뷰의 [name](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md) 열에 표시되는 논리적 파일 이름과 일치합니다.  
  
SELECT 목록, WHERE 절 또는 식 사용을 지원하는 모든 위치에서 `FILE_IDEX`를 사용합니다. 자세한 내용은 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)을 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-retrieving-the-file-id-of-a-specified-file"></a>A. 지정된 파일의 파일 ID 검색  
이 예에서는 `AdventureWorks_Data` 파일의 파일 ID를 반환합니다.  
  
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
  
### <a name="b-retrieving-the-file-id-when-the-file-name-is-not-known"></a>B. 파일 이름이 알려지지 않은 경우 파일 ID 검색  
이 예에서는 `AdventureWorks` 로그 파일의 파일 ID를 반환합니다. T-SQL(Transact-SQL) 코드 조각은 `sys.database_files` 카탈로그 뷰에서 논리적 파일 이름을 선택합니다. 여기서 파일 형식은 `1`(로그)과 같습니다.  
  
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
  
### <a name="c-retrieving-the-file-id-of-a-full-text-catalog-file"></a>C. 전체 텍스트 카탈로그 파일의 파일 ID 검색  
이 예에서는 전체 텍스트 파일의 파일 ID를 반환합니다. T-SQL 코드 조각은 `sys.database_files` 카탈로그 뷰에서 논리적 파일 이름을 선택합니다. 여기서 파일 형식은 `4`(전체 텍스트)와 같습니다. 이 코드는 전체 텍스트 카탈로그가 없을 경우 ‘NULL’을 반환합니다.
  
```sql  
SELECT FILE_IDEX((SELECT name FROM sys.master_files WHERE type = 4))  
AS 'File_ID';  
```  
  
## <a name="see-also"></a>참고 항목  
 [메타데이터 함수&#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sys.database_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  
