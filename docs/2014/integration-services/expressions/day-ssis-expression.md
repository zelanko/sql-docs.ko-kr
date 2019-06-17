---
title: DAY(SSIS 식) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- DAY function
- dates [Integration Services], DAY
ms.assetid: d8447187-49df-45b7-a98e-142ad44fd3e2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 47140db35618143522ad217f5eda2aa3d4b7507b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62898416"
---
# <a name="day-ssis-expression"></a>DAY(SSIS 식)
  날짜의 일 부분을 나타내는 정수를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DAY(date)  
```  
  
## <a name="arguments"></a>인수  
 *date*  
 유효한 날짜 또는 날짜 형식의 문자열을 반환하는 식입니다.  
  
## <a name="result-types"></a>결과 형식  
 DT_I4  
  
## <a name="remarks"></a>Remarks  
 인수가 Null이면 DAY 결과도 Null입니다.  
  
 날짜 리터럴은 다음의 날짜 데이터 형식 중 하나로 명시적 캐스팅되어야 합니다. 자세한 내용은 [Integration Services Data Types](../data-flow/integration-services-data-types.md)을 참조하세요.  
  
> [!NOTE]  
>  날짜 리터럴이 DT_DBTIMESTAMPOFFSET 및 DT_DBTIMESTAMP2 날짜 데이터 형식 중 하나로 명시적 캐스팅되면 식의 유효성 검사가 실패합니다.  
  
 DAY 함수는 DATEPART("Day", date) 함수보다 간단하지만 동일한 결과를 반환합니다.  
  
## <a name="expression-examples"></a>식 예  
 이 예에서는 날짜 리터럴의 일 수를 반환합니다. 날짜 형식이 "mm/dd/yyyy"이면 23이 반환됩니다.  
  
```  
DAY((DT_DBTIMESTAMP)"11/23/2002")  
```  
  
 이 예에서는 **ModifiedDate** 열의 일 부분을 나타내는 정수를 반환합니다.  
  
```  
DAY(ModifiedDate)  
```  
  
 이 예에서는 현재 날짜의 일을 나타내는 정수를 반환합니다.  
  
```  
DAY(GETDATE())  
```  
  
## <a name="see-also"></a>관련 항목  
 [DATEADD&#40;SSIS 식&#41;](dateadd-ssis-expression.md)   
 [DATEDIFF&#40;SSIS 식&#41;](datediff-ssis-expression.md)   
 [DATEPART&#40;SSIS 식&#41;](datepart-ssis-expression.md)   
 [MONTH&#40;SSIS 식&#41;](month-ssis-expression.md)   
 [YEAR&#40;SSIS 식&#41;](year-ssis-expression.md)   
 [함수&#40;SSIS 식&#41;](functions-ssis-expression.md)  
  
  
