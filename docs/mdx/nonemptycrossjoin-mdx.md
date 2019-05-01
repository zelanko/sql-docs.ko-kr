---
title: NonEmptyCrossjoin (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7da56ac658f57d6eb664762f9dd94351df39fe0f
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63456572"
---
# <a name="nonemptycrossjoin-mdx"></a>NonEmptyCrossjoin(MDX)


  하나 이상의 집합에 대한 교차곱을 포함하는 한 개의 집합을 반환합니다. 빈 튜플과 관련 팩트 테이블 데이터가 없는 튜플은 제외됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
NonEmptyCrossjoin(Set_Expression1 [ ,Set_Expression2,...] [,Count ] )  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression1*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Set_Expression2*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *개수*  
 반환할 집합 수를 지정하는 유효한 숫자 식입니다.  
  
## <a name="remarks"></a>Remarks  
 합니다 **NonEmptyCrossjoin** 빈 튜플과 기본 팩트 테이블이 제공 하는 데이터가 없는 튜플은 제외 집합으로 두 개 이상 집합의 교차곱을 반환 합니다. 방식 때문 **NonEmptyCrossjoin** 함수의 작동 모든 계산 멤버가 자동으로 제외 됩니다.  
  
 하는 경우 *개수* 지정 하지 않으면 함수 간 지정 된 모든 집합을 조인 하 고 결과 집합에서 빈 멤버를 제외 합니다. 집합 수가 지정된 경우 이 함수는 지정된 첫 번째 집합부터 시작하여 지정된 집합 수만큼 크로스 조인합니다. 합니다 **NonEmptyCrossjoin** 함수는 지정 된 다음 집합에서 지정 되어 있지만 조인 되지 않은 교차 멤버 크로스 조인된 집합에서 비어 있지 않은 것으로 간주 됩니다 확인 하려면 나머지 집합을 사용 합니다. **NonEmptyCrossjoin** 측면 함수는 **NON_EMPTY_BEHAVIOR** 계산 측정값을 설정 합니다.  
  
> [!IMPORTANT]  
>  이 함수는 더 이상 사용되지 않으며 이전 버전과의 호환성을 위해서만 유지되어 있습니다. 이 함수 대신 대신 사용 해야 합니다 [Exists (MDX)](../mdx/exists-mdx.md) 측정값 그룹 이름 인수를 사용 하 여 함수 또는 [NonEmpty (MDX)](../mdx/nonempty-mdx.md) 함수입니다.  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
