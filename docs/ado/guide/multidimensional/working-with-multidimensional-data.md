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
ms.openlocfilehash: 61f3e34af2a9331118b41657cf958021b972b04a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67923137"
---
# <a name="working-with-multidimensional-data"></a>다차원 데이터 작업
*셀 집합* 은 다차원 데이터에 대 한 쿼리의 결과입니다. 이는 축 컬렉션으로 구성 됩니다. 일반적으로 축은 4 개 이하로, 일반적으로는 2 개 또는 3 개만 있습니다. *축은* 큐브에서 특정 값을 찾거나 필터링 하는 데 사용 되는 하나 이상의 차원에서 가져온 멤버의 컬렉션입니다.  
  
 *위치* 는 축 상의 점입니다. 단일 차원으로 구성 된 축의 경우 이러한 위치는 차원 멤버의 하위 집합입니다. 축이 둘 이상의 차원으로 구성 된 경우 각 위치는 *n* 개 부분이 있는 복합 엔터티입니다. 여기서 *n* 은 해당 축을 따라 측정 되는 차원의 수입니다. 위치의 각 부분은 한 구성 차원의 멤버입니다.  
  
 예를 들어 판매 데이터를 포함 하는 큐브의 Geography 및 Product 차원이 셀 집합의 x 축을 따라 되는 경우이 축의 위치에는 "USA" 및 "Computers" 멤버가 포함 될 수 있습니다. 이 예제에서 x 축을 따라 위치를 결정 하려면 각 차원의 멤버가 축을 따라 방향으로 되어 있어야 합니다.  
  
 *셀* 은 축 좌표가 교차 하는 위치에 있는 개체입니다. 각 셀에는 데이터 자체, 서식이 지정 된 문자열 (표시 가능한 셀 데이터 형식) 및 셀 서 수 값을 포함 하 여 관련 된 여러 가지 정보가 있습니다. 각 셀은 셀 집합의 고유한 서 수 값입니다. 셀 집합에 있는 첫 번째 셀의 서 수 값은 0이 고, 열이 8 개인 셀의 두 번째 행에 있는 맨 왼쪽 셀의 서 수 값은 8입니다.  
  
 예를 들어 큐브에는 다음과 같은 6 개의 차원이 있습니다 .이 큐브 스키마는 [다차원 스키마 및 데이터 개요](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)에 제공 된 예와 약간 다릅니다.  
  
-   영업 사원  
  
-   지리 (자연 계층)-대륙, 국가, 주 등  
  
-   분기-분기, 월, 일  
  
-   Years  
  
-   측정값-Sales, PercentChange, BudgetedSales  
  
-   Products  
  
 다음 셀 집합은 모든 제품의 1991 판매를 나타냅니다.  
  
> [!NOTE]
>  예제의 셀 값은 축 위치 서 수의 정렬 된 쌍으로 볼 수 있습니다. 여기서 첫 번째 숫자는 x 축 위치를 나타내고 두 번째 숫자는 y 축 위치입니다.  
  
 이 셀 집합의 특성은 다음과 같습니다.  
  
-   축 차원: 분기, 영업 사원, 지리  
  
-   필터 차원: 측정값, 연도, 제품  
  
-   두 축: 열 (x, 축 0) 및 행 (y, 축 1)  
  
-   x 축: 두 개의 중첩 된 차원, 영업 사원 및 지리  
  
-   y 축: 사분기 차원  
  
 X 축에는 영업 사원 및 지리 라는 두 개의 중첩 된 차원이 있습니다. 지리에서 시애틀, 보스턴, USA-남부 및 일본의 네 가지 멤버가 선택 됩니다. 판매 직원: 발렌타인 및 Nash의 두 멤버를 선택 합니다. 이 축에는 총 8 개 위치가 생성 됩니다 (8 = 4 * 2).  
  
 각 좌표는 두 개의 멤버가 있는 위치로 표시 됩니다. 즉, 영업 사원의 차원에서 하나, 다른 하나는 Geography 차원에 있습니다.  
  
```console
(Valentine, Seattle), (Valentine, Boston), (Valentine, USA_North),  
(Valentine, Japan), (Nash, Seattle), (Nash, Boston), (Nash, USA_North),  
(Nash, Japan)  
```  
  
 Y 축에는 다음 8 개 위치를 포함 하는 하나의 차원만 있습니다.  
  
```console
Jan, Feb, Mar, Qtr2, Qtr3, Oct, Nov, Dec  
```  
  
 셀 집합, 셀, 축 및 위치는 모두 해당 개체 (셀 [집합](../../../ado/reference/ado-md-api/cellset-object-ado-md.md), [셀](../../../ado/reference/ado-md-api/cell-object-ado-md.md), [축](../../../ado/reference/ado-md-api/axis-object-ado-md.md)및 [위치](../../../ado/reference/ado-md-api/position-object-ado-md.md))로 ADO MD 표시 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [ADO MD 개체 모델](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO (다차원) (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [다차원 스키마 및 데이터 개요](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [ADO MD를 사용한 프로그래밍](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [ADO MD에서 ADO 사용](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)
