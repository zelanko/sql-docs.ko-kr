---
title: RAND (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RAND
- RAND_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- RAND function
- values [SQL Server], random float
- random float value
ms.assetid: 363c84d6-b9fa-49ba-9a75-e44f27535ff6
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 665367907867911d9097fa17d3d05e356a35a014
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="rand-transact-sql"></a>RAND(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  의사 난수를 반환 **float** 0에서 1, 배타적 사이의 값입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
RAND ( [ seed ] )  
```  
  
## <a name="arguments"></a>인수  
 *시드*  
 정수 [식](../../t-sql/language-elements/expressions-transact-sql.md) (**tinyint**, **smallint**, 또는 **int**) 시드 값을 제공 하는 합니다. 경우 *시드* 를 지정 하지 않으면는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 시드 값을 임의로 할당 합니다. 지정된 초기값에 대해 반환된 결과는 항상 동일합니다.  
  
## <a name="return-types"></a>반환 형식  
 **float**  
  
## <a name="remarks"></a>주의  
 동일한 초기값으로 RAND()를 반복 호출하면 동일한 결과를 반환합니다.  
  
 한 연결에 대해 지정된 초기값을 사용해 RAND()를 호출하면 모든 후속 RAND() 호출은 최초 RAND() 호출을 바탕으로 한 결과를 생성합니다. 예를 들어 다음 쿼리는 항상 동일한 순서의 숫자를 반환합니다.  
  
```  
SELECT RAND(100), RAND(), RAND()   
```  
  
## <a name="examples"></a>예  
 다음 예에서는 RAND 함수로 네 가지 서로 다른 난수를 생성합니다.  
  
```  
DECLARE @counter smallint;  
SET @counter = 1;  
WHILE @counter < 5  
   BEGIN  
      SELECT RAND() Random_Number  
      SET @counter = @counter + 1  
   END;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [수치 연산 함수 &#40; Transact SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
  
  
