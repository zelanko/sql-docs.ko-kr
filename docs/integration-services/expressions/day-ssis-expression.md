---
description: DAY(SSIS 식)
title: DAY(SSIS 식) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- DAY function
- dates [Integration Services], DAY
ms.assetid: d8447187-49df-45b7-a98e-142ad44fd3e2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: dff99f077b9260f6bb41fe39661ad831404b4f65
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88495636"
---
# <a name="day-ssis-expression"></a>DAY(SSIS 식)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


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
  
## <a name="remarks"></a>설명  
 인수가 Null이면 DAY 결과도 Null입니다.  
  
 날짜 리터럴은 다음의 날짜 데이터 형식 중 하나로 명시적 캐스팅되어야 합니다. 자세한 내용은 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.  
  
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
 [DATEADD&#40;SSIS 식&#41;](../../integration-services/expressions/dateadd-ssis-expression.md)   
 [DATEDIFF&#40;SSIS 식&#41;](../../integration-services/expressions/datediff-ssis-expression.md)   
 [DATEPART&#40;SSIS 식&#41;](../../integration-services/expressions/datepart-ssis-expression.md)   
 [MONTH&#40;SSIS 식&#41;](../../integration-services/expressions/month-ssis-expression.md)   
 [YEAR&#40;SSIS 식&#41;](../../integration-services/expressions/year-ssis-expression.md)   
 [함수&#40;SSIS 식&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
