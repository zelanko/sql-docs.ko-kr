---
title: FILEGROUP_ID(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FILEGROUP_ID_TSQL
- FILEGROUP_ID
dev_langs:
- TSQL
helpviewer_keywords:
- FILEGROUP_ID function
- identification numbers [SQL Server], filegroups
- filegroups [SQL Server], IDs
- IDs [SQL Server], filegroups
- names [SQL Server], filegroups
ms.assetid: 852a76d8-9e61-4a31-84ee-c7edb84a061c
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 998a3dad0b974a6084c7624dea09a592473a1d5c
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82826983"
---
# <a name="filegroup_id-transact-sql"></a>FILEGROUP_ID(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

이 함수는 지정된 파일 그룹 이름에 해당하는 파일 그룹 ID를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
FILEGROUP_ID ( 'filegroup_name' )   
```  
  
## <a name="arguments"></a>인수  
*filegroup_name*은 반환될 파일 그룹 ID **를 포함하는 파일 그룹 이름을 나타내는** sysname`FILEGROUP_ID` 형식의 식입니다.  
  
## <a name="return-types"></a>반환 형식  
**int**  
  
## <a name="remarks"></a>설명  
*filegroup_name*은 **sys.filegroups** 카탈로그 뷰의 **name** 열과 일치합니다.  
  
## <a name="examples"></a>예  
이 예에서는 `PRIMARY` 데이터베이스에서 파일 그룹 이름 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]에 해당하는 파일 그룹 ID를 반환합니다.  
  
```  
SELECT FILEGROUP_ID('PRIMARY') AS [Filegroup ID];  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
Filegroup ID  
------------  
1  

(1 row(s) affected)
 ```  
  
## <a name="see-also"></a>참고 항목  
 [FILEGROUP_NAME&#40;Transact-SQL&#41;](../../t-sql/functions/filegroup-name-transact-sql.md)   
 [메타데이터 함수&#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sys.filegroups&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)  
  
  
