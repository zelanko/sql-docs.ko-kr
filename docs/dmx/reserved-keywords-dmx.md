---
title: 예약 키워드 (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: fa17a4fb673ad6508fbfc70d5bab39e398d6c3aa
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67928455"
---
# <a name="reserved-keywords-dmx"></a>예약어(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)] 는 단독 사용을 위해 특정 키워드를 예약 합니다. 예약어는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]의 DMX 언어 참조에서 정의한 위치가 아닌 다른 DMX(Data Mining Extensions) 문 위치에서는 사용할 수 없습니다. 이러한 제한된 DMX 키워드에는 다음 멤버가 포함됩니다.  
  
-   모든 데이터 정의 문은 [DMX 데이터 정의 문](../dmx/dmx-statements-data-definition.md)항목에 나와 있습니다.  
  
-   [DMX 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)항목에 나열 된 모든 데이터 마이닝 쿼리 함수  
  
-   [DMX 연산자 참조](../dmx/data-mining-extensions-dmx-operator-reference.md)항목에 나열 된 모든 연산자  
  
-   MDX(Multidimensional Expressions) 쿼리 언어에 정의되어 있고 DMX 문의 일부로 포함된 키워드  
  
-   데이터 마이닝용 OLE DB 사양에 정의되어 있고 DMX 문의 일부로 포함된 키워드  
  
 데이터베이스의 개체 이름을 지정하는 경우에는 예약어 사용을 배제한 명명 규칙을 사용하는 것이 좋습니다.  
  
 데이터베이스에 예약어와 이름이 동일한 개체가 있는 경우 이 개체를 참조할 때는 구분 식별자를 사용해야 합니다. 자세한 내용은 [id &#40;DMX&#41;](../dmx/identifiers-dmx.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [DMX&#41; 참조 &#40;데이터 마이닝 확장](../dmx/data-mining-extensions-dmx-reference.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 구문 규칙](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 구문 요소](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [DMX Select 문 이해](../dmx/understanding-the-dmx-select-statement.md)  
  
  
