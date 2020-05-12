---
title: FILE_NAME(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FILE_NAME_TSQL
- FILE_NAME
dev_langs:
- TSQL
helpviewer_keywords:
- viewing file names
- file names [SQL Server], FILE_NAME
- IDs [SQL Server], files
- file IDs [SQL Server]
- names [SQL Server], files
- displaying file names
- identification numbers [SQL Server], files
- FILE_NAME function
- logical file names [SQL Server]
ms.assetid: 68b298aa-ce47-4af5-b59f-9a1b46d48326
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: fbdd246f7d8758f23bb809500da10c8164ceb034
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82826987"
---
# <a name="file_name-transact-sql"></a>FILE_NAME(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

이 함수는 지정한 파일 ID 번호에 해당하는 논리적 파일 이름을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
FILE_NAME ( file_id )   
```  
  
## <a name="arguments"></a>인수  
*file_id*  
반환될 파일 이름 `FILE_NAME`이 포함된 파일 ID 번호입니다. *file_id*는 **int** 데이터 형식입니다.  
  
## <a name="return-types"></a>반환 형식  
**nvarchar(128)**  
  
## <a name="remarks"></a>설명  
*file_ID*는 sys.master_files 또는 sys.database_files 카탈로그 뷰의 file_id 열과 일치합니다.  
  
## <a name="examples"></a>예  
이 예에서는 `file_ID 1` 데이터베이스에서 `file_ID` 및 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]에 대한 파일 이름을 반환합니다.  
  
```sql  
SELECT FILE_NAME(1) AS 'File Name 1', FILE_NAME(2) AS 'File Name 2';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
File Name 1                File Name 2  
-------------------------  ------------------------  
AdventureWorks2012_Data    AdventureWorks2012_Log  

(1 row(s) affected)
``` 
  
## <a name="see-also"></a>참고 항목  
 [FILE_IDEX&#40;Transact-SQL&#41;](../../t-sql/functions/file-idex-transact-sql.md)   
 [메타데이터 함수&#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sys.database_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
