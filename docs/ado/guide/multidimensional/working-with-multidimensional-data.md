---
title: "다차원 데이터 작업 | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- multidimensional data [ADO]
ms.assetid: 84387746-aa3e-44fd-ad6c-a8214a6966dc
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6e14c59fd0620129486408d33339e80624743f02
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="working-with-multidimensional-data"></a>다차원 데이터 작업
A *cellset* 은 다차원 데이터에 대 한 쿼리의 결과입니다. 축, 일반적으로 4 개 이하의 축 및 보통 두 또는 세 컬렉션을 구성 됩니다. *축* 은 찾거나 큐브에서 특정 값을 필터링 하는 데 사용 되는 하나 이상의 차원에서 멤버의 컬렉션입니다.  
  
 A *위치* 축의 위치가 있습니다. 1 차원으로 구성 된 한 축에 대 한 이러한 위치는 차원 멤버의 하위 집합입니다. 둘 이상의 차원을의 구성 요소 경우 각 위치에는 복합 엔터티는 * n * where 부분 * n * 방향이 해당 축에 따라 차원 수는 있습니다. 위치의 각 부분에는 하나의 구성 차원에서 멤버입니다.  
  
 예를 들어, Geography 및 Product 차원에서 판매 데이터를 포함 하는 큐브에 셀 집합의 x 축을 따라 지향적 이며,이 축 따라 위치 포함 될 수 있습니다 "미국"와 "Computers". 멤버 이 예제에서는 x 축 위치를 결정 하려면 각 차원의 멤버를에서 축 방향 됩니다 필요 합니다.  
  
 A *셀* 은 지점 축 좌표의 교집합에 있는 개체입니다. 각 셀에 여러 가지 데이터 자체, 서식이 지정 된 문자열 (셀 데이터의 표시할 수 있는 형태)으로 및 셀 서 수 값을 포함 하 여 관련 된 정보입니다. (각 셀에는 셀 집합에는 고유한 서 수 값입니다. 셀 집합에서 첫 번째 셀의 서 수 값은 0, 8 개 열이 있는 열 집합의 두 번째 행의 가장 왼쪽 셀은 8의 서 수 값을 보유 하는 것입니다.)  
  
 예를 들어 큐브에 다음과 같은 6 개의 차원 (이 큐브 스키마에 제공 된 예제에서 약간 다릅니다 [개 및 데이터](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)):  
  
-   판매 직원  
  
-   Geography (자연 계층)-대륙, 국가, 상태 및 등  
  
-   분기-분기, 월, 일  
  
-   Years  
  
-   측정값-PercentChange, 판매, BudgetedSales  
  
-   제품  
  
 다음은 셀 집합 1991 모든 제품에 대 한 판매량을 나타냅니다.  
  
> [!NOTE]
>  여기서는 첫 번째 숫자 나타냅니다는 x 축 위치와 두 번째 자리 y 축 위치 축 위치 서 수의 정렬 된 쌍으로 예제에서 셀 값을 볼 수 있습니다.  
  
 이 셀 집합의 특징은 다음과 같습니다.  
  
-   축 차원의: 분기, 영업 사원, 지리적 위치  
  
-   차원을 필터링: 측정값, 년, 제품  
  
-   두 개의 축: 열 (x, 또는 축 0) 및 행 (y, 또는 축 1)  
  
-   x 축: 두 중첩 된 판매 직원 및 지리 차원  
  
-   y 축: 분기 차원  
  
 X 축에 두 개의 중첩된 차원은: 판매 직원 및 지리 합니다. 지역에서 4 명의 구성원을 선택: 시애틀, 보스턴, Japan 및 미국 남부, 합니다. 영업 사원에서 두 명의 멤버 선택: 여덟 합니다. 이 축 (2 * 8 = 4)에 대해 8 개 위치 만큼의 합계를 생성합니다.  
  
 각 좌표는 멤버 2 개 위치도 표시 됩니다.-영업 직원 차원과 Geography 차원에서 다른에서:  
  
```  
(Valentine, Seattle), (Valentine, Boston), (Valentine, USA_North),  
(Valentine, Japan), (Nash, Seattle), (Nash, Boston), (Nash, USA_North),  
(Nash, Japan)  
```  
  
 Y 축에는 다음 8 개 위치 만큼 포함 된 차원이 하나만:  
  
```  
Jan, Feb, Mar, Qtr2, Qtr3, Oct, Nov, Dec  
```  
  
 셀 집합, 셀, 축 및 위치를 모두 표시 ADO MD에서 해당 개체에 의해: [셀 집합](../../../ado/reference/ado-md-api/cellset-object-ado-md.md), [셀](../../../ado/reference/ado-md-api/cell-object-ado-md.md), [축](../../../ado/reference/ado-md-api/axis-object-ado-md.md), 및 [위치](../../../ado/reference/ado-md-api/position-object-ado-md.md).  
  
## <a name="see-also"></a>관련 항목:  
 [ADO MD 개체 모델](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO (다차원) ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [다차원 스키마 및 데이터 개요](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [ADO MD를 사용한 프로그래밍](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [ADO MD로 ADO 사용](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)
