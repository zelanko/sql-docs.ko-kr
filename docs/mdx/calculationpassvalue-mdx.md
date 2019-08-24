---
title: CalculationPassValue (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ae667d2cecb65f2525aaf855d3d1b70d40a59b21
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68016869"
---
# <a name="calculationpassvalue-mdx"></a>CalculationPassValue(MDX)


  지정한 큐브의 계산 패스에 대해 계산된 MDX 식의 숫자 또는 문자열 값을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
      Numeric syntax  
CalculationPassValue(Numeric_Expression,Pass_Value [, ABSOLUTE | RELATIVE [,ALL]])  
String syntax  
CalculationPassValue(String_Expression ,Pass_Value [, ABSOLUTE | RELATIVE [,ALL]])  
```  
  
## <a name="arguments"></a>인수  
 *Numeric_Expression*  
 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
 *String_Expression*  
 문자열로 표현된 숫자를 반환하는 셀 좌표의 유효한 문자열 식으로서, 일반적으로 유효한 MDX 식입니다.  
  
 *Pass_Value*  
 계산 패스 번호를 지정하는 유효한 숫자 식입니다.  
  
 ABSOLUTE  
 지정 하는 액세스 플래그 값을 *Pass_Value* 매개 변수는 계산 패스의 인덱스를 포함 합니다. 액세스 플래그 값이 지정되지 않은 경우 ABSOLUTE가 기본 액세스 플래그 값입니다.  
  
 RELATIVE  
 지정 하는 액세스 플래그 값을 *Pass_Value* 매개 변수를 트리거하는 계산의 계산 패스에서 상대 오프셋을 포함 합니다. 해당 오프셋이 0보다 작은 계산 패스 인덱스로 확인되면 계산 패스 0이 사용되고 오류는 발생하지 않습니다.  
  
 ALL  
 이 플래그가 설정되면 스토리지 엔진에서 로드되는 값을 제외하고 모든 값이 Null입니다. 이 플래그가 설정되지 않으면 계산이 적용되지 않고 값이 집계됩니다.  
  
## <a name="remarks"></a>설명  
 숫자 식이 지정된 경우 이 함수는 지정된 계산 패스에서 특정 MDX 숫자 식을 계산하여 숫자 값을 반환합니다. 선택적으로 액세스 플래그 및 액세스 플래그 한정자에 의해 계산 패스가 한정될 수도 있습니다.  
  
 문자열 식이 지정 된 함수 지정한 계산 패스에서 특정된 MDX 문자열 식을 계산 하 여 문자열 값을 반환 하 고 선택적으로 액세스 플래그 및 액세스 플래그 한정자에 의해 수정*합니다.*  
  
 자동 재귀 해결 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)],이 함수는 실제로 거의 사용 되지 않습니다.  
  
> [!NOTE]  
>  관리자만 사용할 수는 **CalculationPassValue** MDX 스크립트 내의 함수입니다. 이 함수가 포함된 MDX 스크립트가 관리자 권한이 없는 작업의 컨텍스트로 실행되면 오류가 발생합니다.  
  
## <a name="see-also"></a>관련 항목  
 [CalculationCurrentPass & #40; Mdx& #41;](../mdx/calculationcurrentpass-mdx.md)   
 [IIf &#40;MDX&#41;](../mdx/iif-mdx.md)   
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
