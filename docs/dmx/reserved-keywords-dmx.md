---
title: 예약 된 키워드 (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7af060203d044435e364803ace67d35711eb63ea
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2018
ms.locfileid: "34841816"
---
# <a name="reserved-keywords-dmx"></a>예약어(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)] 배타적으로 사용할 특정 키워드를 예약합니다. 예약어는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]의 DMX 언어 참조에서 정의한 위치가 아닌 다른 DMX(Data Mining Extensions) 문 위치에서는 사용할 수 없습니다. 이러한 제한된 DMX 키워드에는 다음 멤버가 포함됩니다.  
  
-   항목에 나열 된 모든 데이터 정의 문 [DMX 데이터 정의 문](../dmx/dmx-statements-data-definition.md)합니다.  
  
-   모든 데이터 마이닝 쿼리 함수는 항목에 나열 된 [DMX 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)합니다.  
  
-   항목에 나열 된 모든 연산자 [DMX 연산자 참조](../dmx/data-mining-extensions-dmx-operator-reference.md)합니다.  
  
-   MDX(Multidimensional Expressions) 쿼리 언어에 정의되어 있고 DMX 문의 일부로 포함된 키워드  
  
-   데이터 마이닝용 OLE DB 사양에 정의되어 있고 DMX 문의 일부로 포함된 키워드  
  
 데이터베이스의 개체 이름을 지정하는 경우에는 예약어 사용을 배제한 명명 규칙을 사용하는 것이 좋습니다.  
  
 데이터베이스에 예약어와 이름이 동일한 개체가 있는 경우 이 개체를 참조할 때는 구분 식별자를 사용해야 합니다. 자세한 내용은 참조 [식별자 &#40;DMX&#41;](../dmx/identifiers-dmx.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Data Mining Extensions &#40;DMX&#41; 참조](../dmx/data-mining-extensions-dmx-reference.md)   
 [Data Mining Extensions &#40;DMX&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)   
 [Data Mining Extensions &#40;DMX&#41; 구문 표기 규칙](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Data Mining Extensions &#40;DMX&#41; 구문 요소](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [DMX Select 문 이해](../dmx/understanding-the-dmx-select-statement.md)  
  
  
