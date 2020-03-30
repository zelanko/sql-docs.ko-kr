---
title: '@@CURSOR_ROWS(Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: ec6830916132a87a7beb50a8509f2f46bd2d1d74
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68026276"
---
# <a name="x40x40cursor_rows-transact-sql"></a>&#x40;&#x40;CURSOR_ROWS(Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

이는 현재 연결에 대해 열려 있는 마지막 커서에서 한정하는 행 수를 반환합니다. 성능 향상을 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 큰 키 집합과 정적 커서를 비동기식으로 채울 수 있습니다. `@@CURSOR_ROWS`를 호출하여 @@CURSOR_ROWS 호출 시 커서에 한정하는 행의 수를 검색할 수 있습니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```
@@CURSOR_ROWS  
```  
  
## <a name="return-types"></a>반환 형식
**integer**
  
## <a name="return-value"></a>Return Value  
  
|반환 값|Description|  
|---|---|
|-*m*|커서가 비동기식으로 채워집니다. 반환되는 값(-*m*)은 현재 키 집합에 있는 행의 개수입니다.|  
|-1|동적 커서입니다. 동적 커서는 모든 변경 사항을 반영하므로 커서가 한정하는 행의 수는 계속 변합니다. 커서가 반드시 한정된 모든 행을 검색하는 것은 아닙니다.|  
|0|열린 커서가 없거나 마지막으로 열린 커서에 한정된 행이 없거나 마지막으로 열린 커서가 닫히거나 할당 취소되었습니다.|  
|*n*|커서가 완전히 채워졌습니다. 반환되는 값(*n*)은 커서에 있는 행의 총 개수입니다.|  
  
## <a name="remarks"></a>설명  
`@@CURSOR_ROWS`는 마지막 커서가 비동기적으로 열린 경우 음수를 반환합니다. 키 집합-드라이버 또는 정적 커서는 sp_configure cursor threshold 값이 0보다 크고 커서 결과 집합에 있는 행의 수가 커서 임계값보다 크면 비동기식으로 열립니다.
  
## <a name="examples"></a>예  
이 예에서는 먼저 커서를 선언한 후 `SELECT`를 사용하여 `@@CURSOR_ROWS`의 값을 표시합니다. 커서가 열리기 전에는 설정의 값이 `0`이며 커서가 열리면 커서 키 집합이 비동기식으로 채워졌음을 나타내는 값인 `-1`로 변경됩니다.
  
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
  
```
-----------
0  
```

```
LastName
---------------
Sanchez
```

```
-----------
-1
```  
  
## <a name="see-also"></a>참고 항목
[커서 함수&#40;Transact-SQL&#41;](../../t-sql/functions/cursor-functions-transact-sql.md)  
[OPEN&#40;Transact-SQL&#41;](../../t-sql/language-elements/open-transact-sql.md)
  
  
