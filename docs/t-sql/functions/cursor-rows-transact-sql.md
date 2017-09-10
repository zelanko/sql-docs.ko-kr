---
title: '@@CURSOR_ROWS (Transact SQL) | Microsoft Docs'
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@CURSOR_ROWS'
- '@@CURSOR_ROWS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@CURSOR_ROWS function'
- cursors [SQL Server], last-opened
- last-opened cursor
- asynchronous cursors [SQL Server]
ms.assetid: 31bd7a97-7f28-42a8-ba24-24d16d22973d
caps.latest.revision: 36
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0e3251891dfaa079933ea79c76154f76f7c2e148
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="cursorrows-transact-sql"></a>@@CURSOR_ROWS (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

현재 연결에 대해 열려 있는 마지막 커서에서 한정하는 행 수를 반환합니다. 성능 향상을 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 큰 키 집합과 정적 커서를 비동기식으로 채울 수 있습니다. @@CURSOR_ROWS 커서를 한 정하는 행 수가 @ 시간에 검색 됩니다 확인 하기 위해 호출할 수@CURSOR_ROWS 호출 됩니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
@@CURSOR_ROWS  
```  
  
## <a name="return-types"></a>반환 형식
**integer**
  
## <a name="return-value"></a>반환 값  
  
|반환 값|Description|  
|---|---|
|-*m*|커서가 비동기식으로 채워집니다. 반환 되는 값 (-*m*)는 키 집합에 있는 현재 행의 수입니다.|  
|-1|동적 커서입니다. 동적 커서는 모든 변경 사항을 반영하므로 커서가 한정하는 행의 수는 계속 변합니다. 따라서 한정된 모든 행이 검색되었다고 확실하게 말할 수는 없습니다.|  
|0|열린 커서가 없거나 마지막으로 열린 커서에 한정된 행이 없거나 마지막으로 열린 커서가 닫히거나 할당 취소되었습니다.|  
|*n*|커서가 완전히 채워졌습니다. 반환 되는 값 (*n*) 커서에서 행의 총 수입니다.|  
  
## <a name="remarks"></a>주의  
반환한 번호@CURSOR_ROWS 마지막 커서가 비동기식으로 열렸을 경우 음수입니다. Sp_configure cursor threshold 값이 0 보다 큰 경우 커서 결과 집합의 행 수가 커서 임계값 보다 크면 키 집합-드라이버 또는 정적 커서가 비동기적으로 열린 됩니다.
  
## <a name="examples"></a>예  
다음 예에서는 커서를 선언하고 `SELECT`를 사용하여 `@@CURSOR_ROWS`의 값을 표시합니다. 커서가 열리기 전에는 설정의 값이 `0`이며 커서가 열리면 커서 키 집합이 비동기식으로 채워졌음을 나타내는 값인 `-1`로 변경됩니다.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT @@CURSOR_ROWS;  
DECLARE Name_Cursor CURSOR FOR  
SELECT LastName ,@@CURSOR_ROWS FROM Person.Person;  
OPEN Name_Cursor;  
FETCH NEXT FROM Name_Cursor;  
SELECT @@CURSOR_ROWS;  
CLOSE Name_Cursor;  
DEALLOCATE Name_Cursor;  
GO             
```  
  
결과 집합은 다음과 같습니다.
  
`-----------`
  
 `0`  
  
`LastName`
  
`---------------`
  
`Sanchez`
  
`-----------`
  
 `-1`  
  
## <a name="see-also"></a>참고 항목
[커서 함수 &#40; Transact SQL &#41;](../../t-sql/functions/cursor-functions-transact-sql.md)  
[열기 &#40; Transact SQL &#41;](../../t-sql/language-elements/open-transact-sql.md)
  
  

