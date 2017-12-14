---
title: "? :(조건부)(SSIS 식) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- conditional operator (?:)
- '?: (conditional operator)'
ms.assetid: d38e6890-7338-4ce0-a837-2dbb41823a37
caps.latest.revision: "49"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 91efcc7d11226a240f2f3b46ab1b14f57da3bbab
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="--conditional-ssis-expression"></a>? : (조건부)(SSIS 식)
  부울 식의 계산에 따라 두 식 중 하나를 반환합니다. 부울 식이 TRUE이면 첫 번째 식이 계산되고 반환 결과는 식의 결과입니다. 부울 식이 FALSE이면 두 번째 식이 계산되고 반환 결과는 식의 결과입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
boolean_expression?expression1:expression2  
  
```  
  
## <a name="arguments"></a>인수  
 *boolean_expression*  
 TRUE, FALSE 또는 NULL로 계산되는 임의의 유효한 식입니다.  
  
 *expression1*  
 유효한 식입니다.  
  
 *expression2*  
 유효한 식입니다.  
  
## <a name="result-types"></a>결과 형식  
 *expression1* 또는 *expression2*의 데이터 형식입니다.  
  
## <a name="remarks"></a>주의  
 *boolean_expression* 이 NULL이면 식 결과도 NULL입니다. *expression1* 또는 *expression2* 중에서 선택한 식이 NULL이면 결과도 NULL입니다. 선택한 식은 NULL이 아니지만 선택하지 않은 식이 NULL이면 결과는 선택한 식의 값입니다.  
  
 *expression1* 및 *expression2* 의 데이터 형식이 같으면 결과도 해당 데이터 형식이 됩니다. 다음은 결과 형식에 적용되는 추가 규칙입니다.  
  
-   DT_TEXT 데이터 형식은 *expression1* 및 *expression2* 의 코드 페이지가 같아야 합니다.  
  
-   DT_BYTES 데이터 형식의 결과 길이는 둘 중에서 긴 인수의 길이입니다.  
  
 식 집합 *expression1* 및 *expression2*는 유효한 데이터 형식으로 계산되고 다음 규칙 중 하나를 따라야 합니다.  
  
-   **Numeric**   *expression1* 및 *expression2* 모두 숫자 데이터 형식이어야 합니다. 데이터 형식의 교집합은 식 계산기가 수행하는 암시적 숫자 변환에 대한 규칙에 지정된 대로 숫자 데이터 형식이어야 합니다. 두 숫자 데이터 형식의 교집합은 Null일 수 없습니다. 자세한 내용은 [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md)을 참조하세요.  
  
-   **String** *expression1* 및 *expression2* 모두 문자열 데이터 형식(DT_STR 또는 DT_WSTR)이어야 합니다. 두 식이 서로 다른 문자열 데이터 형식으로 계산될 수 있습니다. 결과는 DT_WSTR 데이터 형식으로 둘 중에서 긴 인수의 길이입니다.  
  
-   **Date, Time 또는 Date/Time** *expression1* 및 *expression2* 모두는 DT_DBDATE, DT_DATE, DT_DBTIME, DT_DBTIME2, DT_DBTIMESTAMP, DT_DBTIMESTAMP2, DT_DBTIMESTAPMOFFSET 또는 DT_FILETIME 데이터 형식 중 하나로 계산되어야 합니다.  
  
    > [!NOTE]  
    >  시간 데이터 형식으로 계산되는 식과 날짜 또는 날짜/시간 데이터 형식 중 하나로 계산되는 식 사이의 비교는 지원되지 않습니다. 시스템에서 오류가 발생합니다.  
  
     식을 비교하는 경우 시스템은 다음 변환 규칙을 나열된 순서대로 적용합니다.  
  
    -   두 식이 같은 데이터 형식으로 계산되는 경우 해당 데이터 형식의 비교가 수행됩니다.  
  
    -   하나의 식이 DT_DBTIMESTAMPOFFSET 데이터 형식인 경우 다른 식은 DT_DBTIMESTAMPOFFSET으로 암시적으로 변환되며 DT_DBTIMESTAMPOFFSET 비교가 수행됩니다. 자세한 내용은 [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md)을 참조하세요.  
  
    -   하나의 식이 DT_DBTIMESTAMP2 데이터 형식인 경우 다른 식은 DT_DBTIMESTAMP2로 암시적으로 변환되며 DT_DBTIMESTAMP2 비교가 수행됩니다.  
  
    -   하나의 식이 DT_DBTIME2 데이터 형식인 경우 다른 식은 DT_DBTIME2로 암시적으로 변환되며 DT_DBTIME2 비교가 수행됩니다.  
  
    -   하나의 식이 DT_DBTIMESTAMPOFFSET, DT_DBTIMESTAMP2 또는 DT_DBTIME2 이외의 형식인 경우 다른 식은 DT_DBTIMESTAMP 데이터 형식으로 변환되어 비교됩니다.  
  
     식을 비교할 때 시스템에서는 다음과 같이 가정합니다.  
  
    -   각 식이 소수 자릿수 초를 포함하는 데이터 형식인 경우 시스템은 소수 자릿수 초의 자릿수가 가장 적은 데이터 형식의 나머지 자릿수를 0으로 가정합니다.  
  
    -   각 식이 날짜 데이터 형식이고 이 중 하나에만 표준 시간대 오프셋이 있는 경우 시스템은 표준 시간대 오프셋이 없는 날짜 데이터 형식을 UTC(Coordinated Universal Time)로 가정합니다.  
  
 데이터 형식에 대한 자세한 내용은 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.  
  
## <a name="expression-examples"></a>식 예  
 이 예에서는 조건에 따라 `savannah` 또는 `unknown`으로 계산되는 식을 보여 줍니다.  
  
```  
@AnimalName == "Elephant"? "savannah": "unknown"  
```  
  
 이 예에서는 **ListPrice** 열을 참조하는 식을 보여 줍니다. **ListPrice** 는 DT_CY 데이터 형식입니다. 이 식은 조건에 따라 **ListPrice** 에 .2 또는 .1을 곱합니다.  
  
```  
ListPrice < 350.00 ? ListPrice * .2 : ListPrice * .1  
```  
  
## <a name="see-also"></a>관련 항목:  
 [연산자 우선 순위 및 계산 방향](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [연산자&#40;SSIS 식&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
