---
title: "+ (연결)(SSIS 식) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- concatenation [Integration Services]
- + (concatenate operator)
- concatenate operator (+)
ms.assetid: 0fed6334-7a4f-42dc-a611-191fcaa0e443
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f139fd9f1d1f5e3cfb3e24ca34d90372ea27efb7
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="-concatenate-ssis-expression"></a>+(연결)(SSIS 식)
  두 식을 하나의 식으로 연결합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
character_expression1 + character_expression2  
  
```  
  
## <a name="arguments"></a>인수  
 *expression1, expression2*  
 DT_STR, DT_WSTR, DT_TEXT, DT_NTEXT 또는 DT_IMAGE 데이터 형식의 유효한 식입니다.  
  
## <a name="result-types"></a>결과 형식  
 DT_WSTR  
  
## <a name="remarks"></a>Remarks  
 식은 DT_STR 및 DT_WSTR 데이터 형식 중 하나 또는 둘 다를 사용할 수 있습니다.  
  
 DT_STR 및 DT_WSTR 데이터 형식을 연결하면 DT_WSTR 형식의 결과가 반환됩니다. 문자열 길이는 문자로 표시된 원래 문자열 길이의 합계입니다.  
  
 문자열 데이터 형식 DT_STR 및 DT_WSTR나 BLOB(Binary Large Object Block) 데이터 형식 DT_TEXT, DT_NTEXT 및 DT_IMAGE의 데이터만 연결할 수 있습니다. 기타 데이터 형식은 연결을 수행하기 전에 명시적으로 이러한 데이터 형식 중 하나로 변환해야 합니다. 데이터 형식 간 올바른 캐스트에 대한 자세한 내용은 [캐스트&#40;SSIS 식&#41;](../../integration-services/expressions/cast-ssis-expression.md)를 참조하세요.  
  
 두 식이 모두 동일한 데이터 형식으로 되어 있거나 식 하나가 암시적으로 또 다른 식의 데이터 형식으로 변환될 수 있어야 합니다. 예를 들어 "Order date is " 문자열과 **OrderDate** 열을 연결하면 **OrderDate** 값이 암시적으로 문자열 데이터 형식으로 변환됩니다. 두 개의 숫자 값을 연결하려면 두 숫자 값을 모두 명시적으로 문자열 데이터 형식으로 캐스팅해야 합니다.  
  
 연결은 BLOB 데이터 형식인 DT_TEXT, DT_NTEXT 또는 DT_IMAGE 중 하나만 사용할 수 있습니다.  
  
 두 요소 중 하나가 Null이면 결과도 Null입니다.  
  
 문자열 리터럴은 따옴표로 묶어야 합니다.  
  
## <a name="expression-examples"></a>식 예  
 다음 예에서는 **FirstName** 및 **LastName** 열의 값을 연결하고 사이에 공백을 넣습니다.  
  
```  
FirstName + ' ' + LastName  
```  
  
 다음 예에서는 변수 **ZIPCode** 와 **ZIPCode+4**를 연결합니다. 두 변수는 모두 문자열 데이터 형식입니다. **ZIPCode+4** 는 변수 이름에 + 문자가 포함되어 있으므로 대괄호로 묶어야 합니다.  
  
```  
@ZIPCcode + "-" + @[ZipCode+4]  
```  
  
## <a name="see-also"></a>참고 항목  
 [연산자 우선 순위 및 계산 방향](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [연산자&#40;SSIS 식&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
