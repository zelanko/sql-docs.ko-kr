---
title: FILEGROUP_NAME(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- FILEGROUP_NAME_TSQL
- FILEGROUP_NAME
dev_langs:
- TSQL
helpviewer_keywords:
- displaying filegroup names
- identification numbers [SQL Server], filegroups
- filegroups [SQL Server], IDs
- IDs [SQL Server], filegroups
- FILEGROUP_NAME function
- filegroups [SQL Server], names
- names [SQL Server], filegroups
- viewing filegroup names
ms.assetid: 26add1c0-56e5-47a8-b489-ae56784a7ee9
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 877969369a9b18cd7b13db556078a5773b89c947
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="filegroupname-transact-sql"></a>FILEGROUP_NAME(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정한 파일 그룹 ID에 해당하는 파일 그룹 이름을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
FILEGROUP_NAME ( filegroup_id )   
```  
  
## <a name="arguments"></a>인수  
 *filegroup_id*  
 파일 그룹 이름을 반환할 파일 그룹 ID입니다. *filegroup_id*은 **smallint**입니다.  
  
## <a name="return-types"></a>반환 형식  
 **nvarchar(128)**  
  
## <a name="remarks"></a>Remarks  
 *filegroup_id*는 **sys.filegroups** 카탈로그 뷰의 **data_space_id** 열에 해당합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `1` 데이터베이스에서 파일 그룹 ID [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]에 해당하는 파일 그룹 이름을 반환합니다.  
  
```  
  
SELECT FILEGROUP_NAME(1) AS [Filegroup Name];  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Filegroup Name   
-----------------------  
PRIMARY  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>참고 항목  
 [메타데이터 함수&#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [sys.filegroups&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)  
  
  
