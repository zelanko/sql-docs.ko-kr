---
title: "UPPER (SSIS 식) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- UPPER function
- converting lowercase to uppercase
- uppercase characters [Integration Services]
- lowercase characters
ms.assetid: d33985f7-1048-4023-83e4-274090acda78
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1764b39b0242ce7e23d56c9c74f7b953f45009b2
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="upper-ssis-expression"></a>UPPER(SSIS 식)
  소문자를 대문자로 변환한 후에 문자 식을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
UPPER(character_expression)  
```  
  
## <a name="arguments"></a>인수  
 *character_expression*  
 대문자로 변환할 문자 식입니다.  
  
## <a name="result-types"></a>결과 형식  
 DT_WSTR  
  
## <a name="remarks"></a>주의  
 UPPER는 DT_WSTR 데이터 형식에서만 실행됩니다. 문자열 리터럴이나 DT_STR 데이터 형식의 데이터 열인 *character_expression* 인수는 UPPER이 연산을 수행하기 전에 DT_WSTR 데이터 형식으로 암시적으로 캐스팅됩니다. 다른 데이터 형식은 DT_WSTR 데이터 형식으로 명시적으로 캐스팅되어야 합니다. 자세한 내용은 [Integration Services 데이터 형식](../../integration-services/data-flow/integration-services-data-types.md) 및 [캐스트&#40;SSIS 식&#41;](../../integration-services/expressions/cast-ssis-expression.md)를 참조하세요.  
  
 인수가 Null이면 UPPER 결과도 Null입니다.  
  
## <a name="expression-examples"></a>식 예  
 이 예에서는 문자열 리터럴을 대문자로 변환합니다. 반환 결과는 "HELLO"입니다.  
  
```  
UPPER("hello")  
```  
  
 이 예에서는 **FirstName** 열의 첫 문자를 대문자로 변환합니다. **FirstName** 이 anna이면 반환 결과는 "A"입니다. 자세한 내용은 [SUBSTRING&#40;SSIS 식&#41;](../../integration-services/expressions/substring-ssis-expression.md)을 참조하세요.  
  
```  
UPPER(SUBSTRING(FirstName, 1, 1))  
```  
  
 이 예에서는 **PostalCode** 변수 값을 대문자로 변환합니다. **PostalCode** 이 k4b1s2이면 반환 결과는 "K4B1S2"입니다.  
  
```  
UPPER(@PostalCode)  
```  
  
## <a name="see-also"></a>관련 항목:  
 [아래 &#40; SSIS 식 &#41;](../../integration-services/expressions/lower-ssis-expression.md)   
 [함수 &#40; SSIS 식 &#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  

