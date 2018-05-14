---
title: DECOMPRESS(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/30/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DECOMPRESS
- DECOMPRESS_TSQL
helpviewer_keywords:
- DECOMPRESS function
ms.assetid: 738d56be-3870-4774-b112-3dce27becc11
caps.latest.revision: 8
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 2d2b965d3177be06b46bb51b8f5238f5a4b21dee
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="decompress-transact-sql"></a>DECOMPRESS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  GZIP 알고리즘을 사용하여 입력된 식의 압축을 풉니다. 압축 결과는 바이트 배열(VARBINARY(MAX) 형식)입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
DECOMPRESS ( expression )  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 **varbinary(***n***)**, **varbinary(max)** 또는 **binary(***n***)** 입니다. 자세한 내용은 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)을 참조하세요.  
  
## <a name="return-types"></a>반환 형식  
 **varbinary (max)** 형식의 데이터 형식을 반환합니다. 입력된 인수는 ZIP 알고리즘을 사용하여 압축을 풉니다. 필요한 경우 사용자가 명시적으로 결과를 대상 유형으로 캐스팅해야 합니다.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="examples"></a>예  
  
### <a name="a-decompress-data-at-query-time"></a>1. 쿼리 시간에 데이터 압축 해제  
 다음 예에서는 테이블에서 압축 데이터를 표시하는 방법을 보여줍니다.  
  
```  
SELECT _id, name, surname, datemodified,  
             CAST(DECOMPRESS(info) AS NVARCHAR(MAX)) AS info  
FROM player;  
```  
  
### <a name="b-display-compressed-data-using-computed-column"></a>2. 계산 열을 사용하여 압축된 데이터 표시   
 다음 예에서는 압축 해제된 데이터를 저장하기 위한 테이블을 만드는 방법을 보여줍니다.  
  
```  
CREATE TABLE (  
    _id int primary key identity,  
    name nvarchar(max),  
    surname nvarchar(max),  
    info varbinary(max),  
    info_json as CAST(decompress(info) as nvarchar(max))  
);  
```  
  
## <a name="see-also"></a>참고 항목  
 [문자열 함수&#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [COMPRESS&#40;Transact-SQL&#41;](../../t-sql/functions/compress-transact-sql.md)  
  
  
