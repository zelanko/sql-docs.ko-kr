---
title: '@@TEXTSIZE (Transact SQL) | Microsoft Docs'
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@TEXTSIZE'
- '@@TEXTSIZE_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- SET statement, TEXTSIZE option
- SELECT statement [SQL Server], text size returned
- TEXTSIZE option
- '@@TEXTSIZE function'
- text size returned [SQL Server]
ms.assetid: 4308a7b9-8e8f-49e9-8246-8224e32f4953
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: f3585a043d8bab53ccf9060502edc4a93806f58c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40textsize-transact-sql"></a>& #x 40; & #x 40; TEXTSIZE (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  현재 값을 반환 된 [TEXTSIZE](../../t-sql/statements/set-textsize-transact-sql.md) 옵션입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
@@TEXTSIZE  
```  
  
## <a name="return-types"></a>반환 형식  
 **integer**  
  
## <a name="examples"></a>예  
 다음 예제에서는 `SELECT` 표시 하는 `@@TEXTSIZE` 전후와 변경 된 값은 `SET``TEXTSIZE` 문.  
  
```  
-- Set the TEXTSIZE option to the default size of 4096 bytes.  
SET TEXTSIZE 0  
SELECT @@TEXTSIZE AS 'Text Size'  
SET TEXTSIZE 2048  
SELECT @@TEXTSIZE AS 'Text Size'  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Text Size
-----------
4096
Text Size
-----------
2048
 ```  
  
## <a name="see-also"></a>관련 항목:  
 [구성 함수&#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [SET TEXTSIZE &#40; Transact SQL &#41;](../../t-sql/statements/set-textsize-transact-sql.md)  
  
  

