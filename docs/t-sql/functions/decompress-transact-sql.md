---
title: "압축 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 11/30/2015
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
- DECOMPRESS
- DECOMPRESS_TSQL
helpviewer_keywords:
- DECOMPRESS function
ms.assetid: 738d56be-3870-4774-b112-3dce27becc11
caps.latest.revision: 8
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7918a9bce5afcd7ce59551a60fc7e3f2f318f492
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="decompress-transact-sql"></a>압축 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  입력된 식이 GZIP 알고리즘을 사용 하 여 압축을 풉니다. 압축 결과 바이트 배열 (varbinary (max) 유형).  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
DECOMPRESS ( expression )  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 이 **varbinary (***n***)**, **varbinary (max)**, 또는 **이진 (** *n***)**. 자세한 내용은 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)을 참조하세요.  
  
## <a name="return-types"></a>반환 형식  
 데이터 형식을 반환 **varbinary (max)** 유형입니다. 입력된 인수 ZIP 알고리즘을 사용 하 여 압축 됩니다. 필요한 경우 사용자와 대상 유형의 결과 캐스팅 명시적으로 해야 합니다.  
  
## <a name="remarks"></a>주의  
  
## <a name="examples"></a>예  
  
### <a name="a-decompress-data-at-query-time"></a>1. 쿼리 시간에 데이터를 압축 해제  
 다음 예에서는 테이블에서 압축 데이터를 표시 하는 방법을 보여 줍니다.  
  
```  
SELECT _id, name, surname, datemodified,  
             CAST(DECOMPRESS(info) AS NVARCHAR(MAX)) AS info  
FROM player;  
```  
  
### <a name="b-display-compressed-data-using-computed-column"></a>2. 계산된 열을 사용 하 여 압축 된 데이터를 표시 합니다.  
 다음 예제에서는 압축 푼된 데이터를 저장할 테이블을 만드는 방법을 보여 줍니다.  
  
```  
CREATE TABLE (  
    _id int primary key identity,  
    name nvarchar(max),  
    surname nvarchar(max),  
    info varbinary(max),  
    info_json as CAST(decompress(info) as nvarchar(max))  
);  
```  
  
## <a name="see-also"></a>관련 항목:  
 [문자열 함수 &#40; Transact SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [Compress&#40; Transact SQL &#41;](../../t-sql/functions/compress-transact-sql.md)  
  
  

