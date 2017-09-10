---
title: FILE_NAME (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 35
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a2ca12bf5c6f5cfa3e9a7b44300119d5e55e57da
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="filename-transact-sql"></a>FILE_NAME(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정한 파일 ID에 해당하는 논리적 파일 이름을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
FILE_NAME ( file_id )   
```  
  
## <a name="arguments"></a>인수  
 *file_id*  
 파일 이름을 반환할 해당 파일 ID입니다. *file_id* 은 **int**합니다.  
  
## <a name="return-types"></a>반환 형식  
 **nvarchar (128)**  
  
## <a name="remarks"></a>주의  
 *file_ID* sys.master_files 또는 sys.database_files 카탈로그 뷰의 file_id 열에 해당 합니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 파일 이름을 반환 `file`_`ID 1` 및 `file` \_ `ID` 에 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스입니다.  
  
```tsql  
  
SELECT FILE_NAME(1) AS 'File Name 1', FILE_NAME(2) AS 'File Name 2';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `File Name 1           File Name 2`  
  
 `----------------      ------------------------`  
  
 `AdventureWorks2012_Data   AdventureWorks2012_Log`  
  
 `(1 row(s) affected)`  
  
## <a name="see-also"></a>관련 항목:  
 [FILE_IDEX &#40; Transact SQL &#41;](../../t-sql/functions/file-idex-transact-sql.md)   
 [메타 데이터 함수 &#40; Transact SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sys.database_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  
