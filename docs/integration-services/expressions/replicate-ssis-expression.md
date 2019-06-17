---
title: REPLICATE(SSIS 식) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- REPLICATE function
ms.assetid: e7a37b93-6d1d-42d5-9a65-de1790abf6a5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 09c4ff1eaccf529ba30a7bd0d4b9884ae94139ec
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65725040"
---
# <a name="replicate-ssis-expression"></a>REPLICATE(SSIS 식)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  지정한 횟수만큼 복제된 문자 식을 반환합니다. *times* 인수는 정수여야 합니다.  
  
> [!NOTE]  
>  REPLICATE 함수는 긴 문자열을 사용하므로 식 길이에서 4000자 제한에 걸릴 가능성이 큽니다. 식의 평가 결과에 Integration Services 데이터 형식 DT_WSTR 또는 DT_STR이 있는 경우 식이 4000자에서 잘립니다. 하위 식의 결과 유형이 DT_STR 또는 DT_WSTR인 경우 전체 식 결과 유형에 관계없이 해당 하위 식이 4000자로 잘립니다. 잘림 결과가 적절하게 처리될 수 있지만 경고나 오류를 일으킬 수도 있습니다. 자세한 내용은 [구문&#40;SSIS&#41;](../../integration-services/expressions/syntax-ssis.md)을 참조하세요.  
  
## <a name="syntax"></a>구문  
  
```  
  
REPLICATE(character_expression,times)  
```  
  
## <a name="arguments"></a>인수  
 *character_expression*  
 복제할 문자 식입니다.  
  
 *times*  
 *character_expression* 이 복제되는 횟수를 지정하는 정수 식입니다.  
  
## <a name="result-types"></a>결과 형식  
 DT_WSTR  
  
## <a name="remarks"></a>Remarks  
 *times* 가 0이면 빈 문자열이 반환됩니다.  
  
 *times* 가 음수이면 오류가 반환됩니다.  
  
 *times* 인수는 변수와 열을 사용할 수도 있습니다.  
  
 REPLICATE는 DT_WSTR 데이터 형식에서만 실행됩니다. 문자열 리터럴이나 DT_STR 데이터 형식의 데이터 열인 *character_expression* 인수는 REPLICATE가 연산을 수행하기 전에 DT_WSTR 데이터 형식으로 암시적으로 캐스팅됩니다. 다른 데이터 형식은 DT_WSTR 데이터 형식으로 명시적으로 캐스팅되어야 합니다. 자세한 내용은 [Integration Services 데이터 형식](../../integration-services/data-flow/integration-services-data-types.md) 및 [캐스트&#40;SSIS 식&#41;](../../integration-services/expressions/cast-ssis-expression.md)를 참조하세요.  
  
 두 인수 중 하나가 Null이면 REPLICATE 결과도 Null입니다.  
  
## <a name="expression-examples"></a>식 예  
 이 예에서는 문자열 리터럴을 3번 복제합니다. 반환 결과는 "Mountain BikeMountain BikeMountain Bike"입니다.  
  
```  
REPLICATE("Mountain Bike", 3)  
```  
  
 이 예에서는 **Name** 열의 값을 **Times** 변수 값만큼 복제합니다. **Times** 가 3이고 **Name** 이 Touring Front Wheel이면 반환 결과는 Touring Front WheelTouring Front WheelTouring Front Wheel입니다.  
  
```  
REPLICATE(Name, @Times)  
```  
  
 이 예에서는 **Name** 변수 값을 **Times** 열의 값만큼 복제합니다. **Times** 데이터 형식은 정수가 아니고 정수 데이터 형식으로의 명시적 캐스트가 식에 포함되어 있습니다. **Name** 이 Helmet이고 **Times** 가 2이면 반환 결과는 "HelmetHelmet"입니다.  
  
```  
REPLICATE(@Name, (DT_I4(Times))  
```  
  
## <a name="see-also"></a>참고 항목  
 [함수&#40;SSIS 식&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
