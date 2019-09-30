---
title: LEFT(SSIS 식) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5634dbfb-740d-4c93-8fd5-2854cc741327
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c35024df0f34f1a66a64bc587aa928cb0daf4475
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71289389"
---
# <a name="left-ssis-expression"></a>LEFT(SSIS 식)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  지정한 문자 식의 왼쪽부터 지정한 개수의 문자를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
LEFT(character_expression,number)  
```  
  
## <a name="arguments"></a>인수  
 *character_expression*  
 문자를 추출할 문자 식입니다.  
  
 *number*  
 반환할 문자 수를 나타내는 정수 식입니다.  
  
## <a name="result-types"></a>결과 형식  
 DT_WSTR  
  
## <a name="remarks"></a>Remarks  
 *number* 가 *character_expression*의 길이보다 큰 경우 함수는 *character_expression*을 반환합니다.  
  
 *number* 가 0이면 함수는 길이가 0인 문자열을 반환합니다.  
  
 *number* 가 음수이면 오류가 반환됩니다.  
  
 *number* 인수는 변수와 열을 사용할 수 있습니다.  
  
 LEFT는 DT_WSTR 데이터 형식에서만 실행됩니다. 문자열 리터럴이나 DT_STR 데이터 형식의 데이터 열인 *character_expression* 인수는 LEFT가 연산을 수행하기 전에 DT_WSTR 데이터 형식으로 암시적으로 캐스팅됩니다. 다른 데이터 형식은 DT_WSTR 데이터 형식으로 명시적으로 캐스팅되어야 합니다. 자세한 내용은 [Integration Services 데이터 형식](../../integration-services/data-flow/integration-services-data-types.md) 및 [캐스트&#40;SSIS 식&#41;](../../integration-services/expressions/cast-ssis-expression.md)를 참조하세요.  
  
 두 인수 중 하나가 Null이면 LEFT 결과도 Null입니다.  
  
## <a name="expression-examples"></a>식 예  
 다음 예에서는 문자열 리터럴을 사용합니다. 반환 결과는 `"Mountain"`입니다.  
  
```  
LEFT("Mountain Bike", 8)  
```  
  
## <a name="see-also"></a>참고 항목  
 [RIGHT&#40;SSIS 식&#41;](../../integration-services/expressions/right-ssis-expression.md)   
 [함수&#40;SSIS 식&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
