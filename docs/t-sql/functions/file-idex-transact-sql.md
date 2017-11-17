---
title: FILE_IDEX (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 9a65a49a1e6d8c23a28b117fc90b0276ce185556
ms.contentlocale: ko-kr
ms.lasthandoff: 10/24/2017

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
 *i l e _*  
 형식의 식 **sysname** 파일 ID를 반환 하려는 파일의 이름을 나타내는  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
 **NULL** 오류 발생 시  
  
## <a name="remarks"></a>주의  
 *file_name* 에 표시 되는 논리적 파일 이름에 해당 하는 **이름** 열에는 [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md) 또는 [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md) 카탈로그 뷰.  
  
 FILE_IDEX는 SELECT 목록, WHERE 절 또는 식이 사용되는 곳은 어디에나 사용될 수 있습니다. 자세한 내용은 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)을 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-retrieving-the-file-id-of-a-specified-file"></a>1. 지정된 파일의 파일 ID 검색  
다음 예에서는 `AdventureWorks_Data` 파일의 파일 ID를 반환합니다.  
  
```tsql  
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
파일 ID를 반환 하는 다음 예제는 `AdventureWorks` 에서 논리적 파일 이름을 선택 하 여 로그 파일의 `sys.database_files` 카탈로그 뷰에서 파일 유형이 같은 `1` (로그).  
  
```tsql  
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
논리적 파일 이름을 선택 하 여 전체 텍스트 파일의 파일 ID를 반환 하는 다음 예제는 `sys.database_files` 카탈로그 뷰에서 파일 유형이 같은 `4` (전체 텍스트)입니다. 이 예에서는 전체 텍스트 카탈로그가 없을 경우 NULL을 반환합니다.  
  
```tsql  
SELECT FILE_IDEX((SELECT name FROM sys.master_files WHERE type = 4))  
AS 'File_ID';  
```  
  
## <a name="see-also"></a>관련 항목:  
 [메타 데이터 함수 &#40; Transact SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sys.database_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  

