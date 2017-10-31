---
title: "압축 (Transact SQL) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c30cb5f351d9a84beec608483380edb94b8c7844
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="compress-transact-sql"></a>압축 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

GZIP 알고리즘을 사용 하 여 입력된 식을 압축 합니다. 압축 결과 바이트 배열 형식의 **varbinary (max)**합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
COMPRESS ( expression )  
```  
  
## <a name="arguments"></a>인수  
*expression*  
이 **nvarchar (***n***)**, **nvarchar (max)**, **varchar (**  *n*  **)**, **varchar (max)**, **varbinary (**  *n*  **)**, **varbinary (max)**, **char (***n***)**, **nchar (**   *n*  **)**, 또는 **이진 (***n***)** 식입니다. 자세한 내용은 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)을 참조하세요.
  
## <a name="return-types"></a>반환 형식
데이터 형식을 반환 **varbinary (max)** 입력의 압축된 된 콘텐츠를 나타내는입니다.
  
## <a name="remarks"></a>주의  
압축 된 데이터를 인덱싱할 수 없습니다.
  
COMPRESS 함수는 입력된 식으로 제공 되는 데이터를 압축 및 압축 데이터의 각 섹션에 대 한 호출 되어야 합니다. 저장 하는 동안 행 또는 페이지 수준에서 자동 압축에 대 한 참조 [데이터 압축](../../relational-databases/data-compression/data-compression.md)합니다.
  
## <a name="examples"></a>예  
  
### <a name="a-compress-data-during-the-table-insert"></a>1. 테이블 삽입 하는 동안 데이터를 압축 합니다.  
다음 예에서는 테이블에 삽입 된 데이터를 압축 하는 방법을 보여 줍니다.
  
```sql
INSERT INTO player (name, surname, info )  
VALUES (N'Ovidiu', N'Cracium',   
        COMPRESS(N'{"sport":"Tennis","age": 28,"rank":1,"points":15258, turn":17}'));  
  
INSERT INTO player (name, surname, info )  
VALUES (N'Michael', N'Raheem', compress(@info));  
```  
  
### <a name="b-archive-compressed-version-of-deleted-rows"></a>2. 삭제 된 행의 보관 압축된 버전  
다음 문은에서 오래 된 플레이어 레코드 삭제는 `player` 테이블의 레코드를 저장 합니다는 `inactivePlayer` 공간 절약을 위해 압축된 된 형식으로 테이블입니다.
  
```sql
DELETE player  
WHERE datemodified < @startOfYear  
OUTPUT id, name, surname datemodifier, COMPRESS(info)   
INTO dbo.inactivePlayers ;  
```  
  
## <a name="see-also"></a>참고 항목
[문자열 함수 &#40; Transact SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
[압축 해제 &#40; Transact SQL &#41;](../../t-sql/functions/decompress-transact-sql.md)
  
  

