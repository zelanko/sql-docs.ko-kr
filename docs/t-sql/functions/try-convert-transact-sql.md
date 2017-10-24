---
title: TRY_CONVERT (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TRY_CONVERT_TSQL
- TRY_CONVERT
dev_langs:
- TSQL
helpviewer_keywords:
- TRY_CONVERT function
ms.assetid: 3e6e7825-6482-4cb2-a8c2-9abc99e265a6
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0cb3854ae349b17dcdb0b0528c6415fd41b1e072
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="tryconvert-transact-sql"></a>TRY_CONVERT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  캐스트에 성공하면 지정한 데이터 형식으로 캐스팅된 값을 반환합니다. 그렇지 않으면 Null을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
TRY_CONVERT ( data_type [ ( length ) ], expression [, style ] )  
```  
  
## <a name="arguments"></a>인수  
 *data_type [(길이)]*  
 캐스팅할 데이터 형식 *식*합니다.  
  
 *expression*  
 캐스팅할 값입니다.  
  
 *스타일*  
 지정 하는 선택적 정수 식 방법을 **TRY_CONVERT** 함수 변환 하는 *식*합니다.  
  
 *스타일* 동일한 값을 받아들입니다는 *스타일* 의 매개 변수는 **변환** 함수입니다. 자세한 내용은 [CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)를 참조하세요.  
  
 허용 되는 값의 범위 값에 의해 결정 됩니다 *data_type*합니다. 경우 *스타일* 매개 변수가 null 이면 **TRY_CONVERT** null을 반환 합니다.  
  
## <a name="return-types"></a>반환 형식  
 캐스트에 성공하면 지정한 데이터 형식으로 캐스팅된 값을 반환합니다. 그렇지 않으면 Null을 반환합니다.  
  
## <a name="remarks"></a>주의  
 **TRY_CONVERT** 는 전달 된 값을 사용 하 고 지정 된 변환 하려고 *data_type*합니다. 캐스팅에 성공 하면 **TRY_CONVERT** 지정 된 값을 반환 *data_type*; 오류가 발생 하면 null이 반환 됩니다. 그러나 명시적으로 허용 되지 않는, 다음 변환을 요청 하는 경우 **TRY_CONVERT** 오류가 발생 하면서 실패 합니다.  
  
 **TRY_CONVERT** 110 이상은 호환성 수준에서 예약된 된 키워드입니다.  
  
 이 함수는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상 버전이 설치되어 있는 서버에 대해서는 원격으로 실행할 수 있지만 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이전 버전이 설치되어 있는 서버에 대해서는 원격으로 실행할 수 없습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-tryconvert-returns-null"></a>1. TRY_CONVERT가 Null 반환  
 다음 예에서는 캐스팅을 실패할 때 TRY_CONVERT가 null을 반환하는 것을 보여 줍니다.  
  
```tsql  
SELECT   
    CASE WHEN TRY_CONVERT(float, 'test') IS NULL   
    THEN 'Cast failed'  
    ELSE 'Cast succeeded'  
END AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
------------  
Cast failed  
  
(1 row(s) affected)  
```  
  
 다음 예에서는 식이 해당 형식에 맞아야 한다는 것을 보여 줍니다.  
  
```tsql  
SET DATEFORMAT dmy;  
SELECT TRY_CONVERT(datetime2, '12/31/2010') AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
----------------------  
NULL  
  
(1 row(s) affected)  
```  
  
### <a name="b-tryconvert-fails-with-an-error"></a>2. TRY_CONVERT가 오류와 함께 실패  
 다음 예에서는 캐스팅이 명시적으로 허용되지 않은 경우 TRY_CONVERT가 오류를 반환하는 것을 보여 줍니다.  
  
```tsql  
SELECT TRY_CONVERT(xml, 4) AS Result;  
GO  
```  
  
 정수는 xml 데이터 형식으로 캐스팅될 수 없으므로 이 문을 실행하면 오류가 발생합니다.  
  
```  
Explicit conversion from data type int to xml is not allowed.  
```  
  
### <a name="c-tryconvert-succeeds"></a>3. TRY_CONVERT가 성공  
 이 예에서는 식이 해당 형식에 맞아야 한다는 것을 보여 줍니다.  
  
```  
SET DATEFORMAT mdy;  
SELECT TRY_CONVERT(datetime2, '12/31/2010') AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
----------------------------------  
2010-12-31 00:00:00.0000000  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>관련 항목:  
 [CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  

