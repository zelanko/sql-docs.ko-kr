---
title: FILE_ID (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f1b2025ee9fdc5ca0aaf4967305db40cb65d038c
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/02/2018
---
# <a name="fileid-transact-sql"></a>FILE_ID(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 데이터베이스 내에서 지정된 논리적 파일 이름의 파일 ID를 반환합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]사용 하 여 [FILE_IDEX](../../t-sql/functions/file-idex-transact-sql.md) 대신 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
FILE_ID ( file_name )  
```  
  
## <a name="arguments"></a>인수  
 *i l e _*  
 형식의 식 **sysname** 파일 ID를 반환 하려는 파일의 이름을 나타내는  
  
## <a name="return-types"></a>반환 형식  
 **smallint**  
  
## <a name="remarks"></a>주의  
 *file_name* sys.master_files 또는 sys.database_files 카탈로그 뷰의 name 열에 표시 되는 논리적 파일 이름에 해당 합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 전체 텍스트 카탈로그에 할당되는 파일 ID는 32767보다 큽니다. FILE_ID 함수의 반환 형식이 **smallint**, 전체 텍스트 파일에이 함수를 사용할 수 없습니다. 사용 하 여 [FILE_IDEX](../../t-sql/functions/file-idex-transact-sql.md) 대신 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `AdventureWorks_Data` 파일의 파일 ID를 반환합니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server 2016 이후에는 지원되지 않는 데이터베이스 엔진 기능](../../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)   
 [I l e _ &#40; Transact SQL &#41;](../../t-sql/functions/file-name-transact-sql.md)   
 [메타 데이터 함수 &#40; Transact SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sys.database_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  
