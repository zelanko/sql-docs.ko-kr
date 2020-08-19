---
description: COMPRESS(Transact SQL)
title: COMPRESS(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/11/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: reference
f1_keywords:
- COMPRESS
- COMPRESS_TSQL
helpviewer_keywords:
- COMPRESS function
ms.assetid: c2bfe9b8-57a4-48b4-b028-e1a3ed5ece88
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 51cf2e37ae548383d7c02b3ba4028b9327857928
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88468192"
---
# <a name="compress-transact-sql"></a>COMPRESS(Transact SQL)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

이 함수는 GZIP 알고리즘을 사용하여 입력된 식을 압축합니다. 이 함수는 **varbinary(max)** 유형의 바이트 배열을 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
COMPRESS ( expression )  
```  
  
## <a name="arguments"></a>인수
*expression*  
A

* **binary(***n***)**
* **char(***n***)**
* **nchar(***n***)**
* **nvarchar(max)**
* **nvarchar(***n***)**
* **varbinary(max)**
* **varbinary(***n***)**
* **varchar(max)**

또는

* **varchar(***n***)**

expression. 자세한 내용은 [식 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)을 참조하세요.
  
## <a name="return-types"></a>반환 형식
**varbinary(max)** 는 입력의 압축 내용을 나타냅니다.
  
## <a name="remarks"></a>설명  
압축된 데이터를 인덱싱할 수 없습니다.
  
`COMPRESS` 함수는 입력된 식 데이터를 압축합니다. 압축하려면 각 데이터 섹션에 대해 이 함수를 호출해야 합니다. 행 또는 페이지 레벨에서 스토리지 중 자동 데이터 압축에 대한 자세한 정보는 [데이터 압축](../../relational-databases/data-compression/data-compression.md)을 참조하세요.
  
## <a name="examples"></a>예제  
  
### <a name="a-compress-data-during-the-table-insert"></a>A. 테이블 삽입 중에 데이터 압축  
이 예에서는 테이블에 삽입된 데이터를 압축하는 방법을 보여줍니다.
  
```sql
INSERT INTO player (name, surname, info )  
VALUES (N'Ovidiu', N'Cracium',   
        COMPRESS(N'{"sport":"Tennis","age": 28,"rank":1,"points":15258, turn":17}'));  
  
INSERT INTO player (name, surname, info )  
VALUES (N'Michael', N'Raheem', compress(@info));  
```  
  
### <a name="b-archive-compressed-version-of-deleted-rows"></a>B. 삭제된 행의 압축된 버전 보관  
이 명령문은 `player` 테이블에서 오래된 플레이어 레코드를 먼저 삭제합니다. 공간을 절약하기 위해 레코드를 `inactivePlayer` 테이블에 압축 형식으로 저장합니다.
  
```sql
DELETE FROM player  
OUTPUT deleted.id, deleted.name, deleted.surname, deleted.datemodifier, COMPRESS(deleted.info)   
INTO dbo.inactivePlayers
WHERE datemodified < @startOfYear; 
```  
  
## <a name="see-also"></a>참고 항목
[문자열 함수&#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
[DECOMPRESS&#40;Transact-SQL&#41;](../../t-sql/functions/decompress-transact-sql.md)
  
  
