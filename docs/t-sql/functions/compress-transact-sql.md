---
title: COMPRESS(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- COMPRESS
- COMPRESS_TSQL
helpviewer_keywords:
- COMPRESS function
ms.assetid: c2bfe9b8-57a4-48b4-b028-e1a3ed5ece88
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 51324f00da71597a8a2dd37d8f0077c4b3bc8b55
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="compress-transact-sql"></a>COMPRESS(Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

GZIP 알고리즘을 사용하여 입력된 식을 압축합니다. 압축 결과는 **varbinary(max)** 형식의 바이트 배열입니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
COMPRESS ( expression )  
```  
  
## <a name="arguments"></a>인수  
*expression*  
**nvarchar(***n***)**, **nvarchar(max)**, **varchar(***n***)**, **varchar(max)**, **varbinary(***n***)**, **varbinary(max)**, **char(***n***)**, **nchar(***n***)** 또는 **binary(***n***)** 식입니다. 자세한 내용은 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)을 참조하세요.
  
## <a name="return-types"></a>반환 형식
압축된 입력 콘텐츠를 나타내는 **varbinary(max)** 의 데이터 형식을 반환합니다.
  
## <a name="remarks"></a>Remarks  
압축된 데이터를 인덱싱할 수 없습니다.
  
COMPRESS 함수는 입력된 식으로 제공되는 데이터를 압축하여 압축할 데이터의 각 섹션에 대해 호출해야 합니다. 저장 시 행 또는 페이지 수준의 자동 압축에 대한 자세한 내용은 [데이터 압축](../../relational-databases/data-compression/data-compression.md)을 참조하세요.
  
## <a name="examples"></a>예  
  
### <a name="a-compress-data-during-the-table-insert"></a>1. 테이블 삽입 중에 데이터 압축   
다음 예에서는 테이블에 삽입된 데이터를 압축하는 방법을 보여줍니다.
  
```sql
INSERT INTO player (name, surname, info )  
VALUES (N'Ovidiu', N'Cracium',   
        COMPRESS(N'{"sport":"Tennis","age": 28,"rank":1,"points":15258, turn":17}'));  
  
INSERT INTO player (name, surname, info )  
VALUES (N'Michael', N'Raheem', compress(@info));  
```  
  
### <a name="b-archive-compressed-version-of-deleted-rows"></a>2. 삭제된 행의 압축된 버전 보관  
다음 문은 `player` 테이블에서 오래된 플레이어 레코드를 삭제하고, 공간을 절약하기 위해 `inactivePlayer` 테이블의 레코드를 압축된 형식으로 저장합니다.
  
```sql
DELETE player  
WHERE datemodified < @startOfYear  
OUTPUT id, name, surname datemodifier, COMPRESS(info)   
INTO dbo.inactivePlayers ;  
```  
  
## <a name="see-also"></a>관련 항목:
[문자열 함수&#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
[DECOMPRESS&#40;Transact-SQL&#41;](../../t-sql/functions/decompress-transact-sql.md)
  
  
