---
title: DATEADD(SSIS 식) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- dates [Integration Services], DATEADD
- dates [Integration Services]
- DATEADD function
ms.assetid: fa5c37b1-2ddc-4857-8f8e-f6d5643b654f
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: ade2a78dd95ad26f9560bb992a6da3a4811b4583
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36078842"
---
# <a name="dateadd-ssis-expression"></a>DATEADD(SSIS 식)
  날짜에서 지정한 날짜 부분에 날짜 또는 시간 간격을 나타내는 숫자를 더한 후 새로운 DT_DBTIMESTAMP 값을 반환합니다. 숫자 매개 변수는 정수로 계산되고 날짜 매개 변수는 유효한 날짜여야 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DATEADD(datepart, number, date)  
```  
  
## <a name="arguments"></a>인수  
 *datepart*  
 숫자를 더할 날짜 부분을 지정하는 매개 변수입니다.  
  
 *number*  
 *datepart*에 더해지는 값입니다. 값은 식을 구문 분석할 때 알려진 정수 값이어야 합니다.  
  
 *date*  
 유효한 날짜 또는 날짜 형식의 문자열을 반환하는 식입니다.  
  
## <a name="result-types"></a>결과 형식  
 DT_DBTIMESTAMP  
  
## <a name="remarks"></a>Remarks  
 다음 표에서는 식 계산기가 인식하는 날짜 부분 및 약어를 나열합니다. 날짜 부분 이름은 대/소문자를 구분하지 않습니다.  
  
|날짜 부분|약어|  
|--------------|-------------------|  
|Year|yy, yyyy|  
|Quarter|qq, q|  
|Month|mm, m|  
|Dayofyear|dy, y|  
|Day|dd, d|  
|Week|wk, ww|  
|Weekday|dw, w|  
|Hour|Hh|  
|Minute|mi, n|  
|둘째|ss, s|  
|Millisecond|Ms|  
  
 식을 구문 분석할 때 *number* 인수를 사용할 수 있어야 합니다. 인수는 상수 또는 변수일 수 있습니다. 식을 구문 분석할 때 값을 알 수 없으므로 열 값을 사용할 수 없습니다.  
  
 *datepart* 인수는 따옴표로 묶어야 합니다.  
  
 날짜 리터럴은 다음의 날짜 데이터 형식 중 하나로 명시적 캐스팅되어야 합니다. 자세한 내용은 [Integration Services Data Types](../data-flow/integration-services-data-types.md)을 참조하세요.  
  
 인수가 Null이면 DATEADD 결과도 Null입니다.  
  
 날짜가 잘못되었거나 날짜 또는 시간 단위가 문자열이 아니거나 증분이 고정 정수가 아니면 오류가 발생합니다.  
  
## <a name="ssis-expression-examples"></a>SSIS 식 예  
 이 예에서는 현재 날짜에 1개월을 더합니다.  
  
```  
DATEADD("Month", 1,GETDATE())  
```  
  
 이 예에서는 **ModifiedDate** 열의 날짜에 21일을 더합니다.  
  
```  
DATEADD("day", 21, ModifiedDate)  
```  
  
 이 예에서는 리터럴 날짜에 2년을 더합니다.  
  
```  
DATEADD("yyyy", 2, (DT_DBTIMESTAMP)"8/6/2003")  
```  
  
## <a name="see-also"></a>관련 항목  
 [DATEDIFF &#40;SSIS 식&#41;](datediff-ssis-expression.md)   
 [DATEPART&#40;SSIS 식&#41;](datepart-ssis-expression.md)   
 [DAY&#40;SSIS 식&#41;](day-ssis-expression.md)   
 [MONTH&#40;SSIS 식&#41;](month-ssis-expression.md)   
 [YEAR&#40;SSIS 식&#41;](year-ssis-expression.md)   
 [함수 &#40;SSIS 식&#41;](functions-ssis-expression.md)  
  
  