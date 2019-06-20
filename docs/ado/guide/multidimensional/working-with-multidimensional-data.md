---
title: 다차원 데이터 작업 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- multidimensional data [ADO]
ms.assetid: 84387746-aa3e-44fd-ad6c-a8214a6966dc
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: afe8ff8c788a740ca98eca385146ecc71b6e1e95
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704398"
---
# <a name="working-with-multidimensional-data"></a>다차원 데이터 작업
A *cellset* 다차원 데이터에 대 한 쿼리의 결과입니다. 축, 일반적으로 최대 네 개의 축 및 일반적으로 2 또는 3의 컬렉션인 이루어져 있습니다. *축* 찾기 또는 큐브의 특정 값을 필터링 하는 데 사용 되는 하나 이상의 차원에서 멤버의 컬렉션입니다.  
  
 A *위치* 축의 점이 합니다. 1 차원으로 구성 된 축에 대 한 이러한 위치는 차원 멤버의 하위 집합입니다. 둘 이상의 차원을 이루어져 있습니다 축 경우 각 위치가 있는 복합 엔터티를 *n* where 파트 *n* 해당 축을 따라 지향 차원입니다. 위치의 각 부분은 하나의 구성 요소 차원의 멤버입니다.  
  
 예를 들어 판매 데이터가 포함 된 큐브의 Geography 및 Product 차원 셀 집합의 축 방향으로, 하는 경우이 축 따라 위치 멤버를 포함할 수는 "USA"와 "Computers"로 지정 합니다. 이 예제에서는 x 축 따라 위치를 확인 하려면 각 차원에서 멤버 축 방향으로 필요 합니다.  
  
 A *셀* 개체인 축 좌표의 교집합에 위치 합니다. 각 셀에 여러 가지 관련 정보를 데이터 자체, 서식이 지정된 된 문자열 (셀 데이터의 표시 가능한 형식) 및 셀 서 수 값을 포함 합니다. (각 셀은 셀 집합에서 고유한 서 수 값이 하는 데 사용 합니다. 셀 집합에서 첫 번째 셀의 서 수 값은 0 8 개의 열이 포함 된 셀 집합의 두 번째 행의 가장 왼쪽 셀 8의 서 수 값을 해야 하는 동안.)  
  
 예를 들어 큐브에 다음과 같은 6 개의 차원이 (이 큐브 스키마 제공 된 예제에서 약간 다릅니다 [다차원 스키마의 개요 및 데이터](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)):  
  
-   판매 직원  
  
-   Geography (자연 계층)-대륙, 국가, 상태 및 등  
  
-   분기-분기, 월, 일  
  
-   Years  
  
-   측정값-PercentChange, Sales BudgetedSales  
  
-   제품  
  
 다음은 셀 집합 1991 모든 제품에 대 한 판매량을 나타냅니다.  
  
> [!NOTE]
>  첫 번째 숫자 x 축 위치를 나타내고 두 번째 숫자 y 축 좌표를 축 위치 서 수의 정렬 된 쌍으로 예제의 셀 값을 볼 수 있습니다.  
  
 이 셀 집합의 특징은 다음과 같습니다.  
  
-   축 크기: 분기를 영업 지역  
  
-   차원을 필터: 측정값을 년 제품  
  
-   두 개의 축: (X, 또는 축 0) 하는 열 및 행 (y, 또는 축 1)  
  
-   x 축: 두 중첩 된 판매 직원 및 지리 차원  
  
-   y 축: 분기 차원  
  
 X 축에는 두 중첩 된 차원에 있습니다. 판매 직원 및 지리입니다. Geography에서 네 가지 멤버 선택 되어 있습니다. 시애틀, 보스턴, 미국 남부 및 일본입니다. 두 멤버는 판매 직원에서 선택 되어 있습니다. 발렌타인 데이 고 Nash 합니다. 총 8 개 위치 (2 * 8 = 4)이이 축에 대해 같은 결과가 산출 됩니다.  
  
 각 좌표는 멤버가 두-영업 직원 차원에서 및 Geography 차원에서 다른 위치로 표시 됩니다.  
  
```console
(Valentine, Seattle), (Valentine, Boston), (Valentine, USA_North),  
(Valentine, Japan), (Nash, Seattle), (Nash, Boston), (Nash, USA_North),  
(Nash, Japan)  
```  
  
 Y 축에는 다음 8 개 위치에 포함 된 하나의 차원만 있습니다.  
  
```console
Jan, Feb, Mar, Qtr2, Qtr3, Oct, Nov, Dec  
```  
  
 셀, 셀, 축 및 위치는 모두 표시 ADO MD에서 해당 개체에서: [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md), [셀](../../../ado/reference/ado-md-api/cell-object-ado-md.md)를 [축](../../../ado/reference/ado-md-api/axis-object-ado-md.md), 및 [위치](../../../ado/reference/ado-md-api/position-object-ado-md.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ADO MD 개체 모델](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO (다차원) (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [다차원 스키마 및 데이터 개요](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [ADO MD를 사용한 프로그래밍](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [ADO MD로 ADO 사용](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)
