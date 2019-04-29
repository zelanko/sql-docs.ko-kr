---
title: MONTH(SSIS 식) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- dates [Integration Services], MONTH
- MONTH function
ms.assetid: b5a47a11-c2ef-49bd-bd70-235632ff7bf6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2f5e997f40f5af0a9f1c5cd0de4114714a1db8b2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62897530"
---
# <a name="month-ssis-expression"></a>MONTH(SSIS 식)
  날짜의 월 부분을 나타내는 정수를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
MONTH(date)  
```  
  
## <a name="arguments"></a>인수  
 *date*  
 임의의 날짜 형식을 갖는 날짜입니다.  
  
## <a name="result-types"></a>결과 형식  
 DT_I4  
  
## <a name="remarks"></a>Remarks  
 인수가 Null이면 MONTH 결과도 Null입니다.  
  
 날짜 리터럴은 다음의 날짜 데이터 형식 중 하나로 명시적 캐스팅되어야 합니다. 자세한 내용은 [Integration Services Data Types](../data-flow/integration-services-data-types.md)을 참조하세요.  
  
> [!NOTE]  
>  식은 리터럴 날짜 이러한 날짜 데이터 형식 중 하나로 명시적 캐스팅 되 면 유효성을 검사 하는 실패 합니다. DT_DBTIMESTAMPOFFSET 및 DT_DBTIMESTAMP2 합니다.  
  
 MONTH 함수는 DATEPART("Month", date) 함수보다 간단하지만 동일한 결과를 반환합니다.  
  
## <a name="expression-examples"></a>식 예  
 이 예에서는 날짜 리터럴의 월을 반환합니다. 날짜 형식이 "mm/dd/yyyy"이면 11이 반환됩니다.  
  
```  
MONTH((DT_DBTIMESTAMP)"11/23/2002")  
```  
  
 이 예에서는 **ModifiedDate** 열의 월을 나타내는 정수를 반환합니다.  
  
```  
MONTH(ModifiedDate)  
```  
  
 이 예에서는 현재 날짜의 월을 나타내는 정수를 반환합니다.  
  
```  
MONTH(GETDATE())  
```  
  
## <a name="see-also"></a>관련 항목  
 [DATEADD&#40;SSIS 식&#41;](dateadd-ssis-expression.md)   
 [DATEDIFF&#40;SSIS 식&#41;](datediff-ssis-expression.md)   
 [DATEPART&#40;SSIS 식&#41;](datepart-ssis-expression.md)   
 [DAY&#40;SSIS 식&#41;](day-ssis-expression.md)   
 [YEAR&#40;SSIS 식&#41;](year-ssis-expression.md)   
 [함수&#40;SSIS 식&#41;](functions-ssis-expression.md)  
  
  
