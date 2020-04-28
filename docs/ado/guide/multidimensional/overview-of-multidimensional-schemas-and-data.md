---
title: 다차원 스키마 및 데이터 개요 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- multidimensional schemas and data
ms.assetid: ce37fa06-c581-4d80-9a9b-c3aa66408909
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2e4681bb9e1fd1028ee1ddc2bd7f72efc03fb6c7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67923185"
---
# <a name="overview-of-multidimensional-schemas-and-data"></a>다차원 스키마 및 데이터 개요
## <a name="understanding-multidimensional-schemas"></a>다차원 스키마 이해  
 ADO MD의 중앙 메타 데이터 개체는 관련 차원, 계층, 수준 및 멤버의 구조화 된 집합으로 구성 된 *큐브입니다*.  
  
 *차원은* 비즈니스 엔터티에서 파생 된 다차원 데이터베이스의 독립적인 데이터 범주입니다. 일반적으로 차원에는 데이터베이스의 측정값에 대 한 쿼리 조건으로 사용할 항목이 포함 되어 있습니다.  
  
 *계층* 은 차원의 집계 경로입니다. 차원에는 부모-자식 관계가 있는 여러 수준의 세분성이 있을 수 있습니다. 계층은 이러한 수준 간의 관계를 정의 합니다.  
  
 *수준* 은 계층의 집계 단계입니다. 여러 계층의 정보를 포함 하는 차원의 경우 각 계층은 수준입니다.  
  
 *멤버* 는 차원의 데이터 항목입니다. 일반적으로 캡션을 만들거나 멤버를 사용 하 여 데이터베이스의 측정값을 설명 합니다.  
  
 큐브는 ADO MD [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) 개체로 표현 됩니다. 차원, 계층, 수준 및 멤버는 해당 ADO MD 개체 ( [차원](../../../ado/reference/ado-md-api/dimension-object-ado-md.md), [계층](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md), [수준](../../../ado/reference/ado-md-api/level-object-ado-md.md)및 [멤버](../../../ado/reference/ado-md-api/member-object-ado-md.md))로도 표시 됩니다.  
  
### <a name="dimensions"></a>차원  
 큐브의 차원은 데이터베이스에서 모델링할 비즈니스 엔터티와 데이터 유형에 따라 달라 집니다. 일반적으로 각 차원은 데이터를 선택 하기 위한 독립적인 진입점 또는 메커니즘입니다.  
  
 예를 들어 판매 데이터를 포함 하는 큐브에는 판매 직원, 지리, 시간, 제품 및 측정값과 같은 5 개의 차원이 있습니다. 측정값 차원은 실제 판매 데이터 값을 포함 하는 반면 다른 차원은 판매 데이터 값을 범주화 하 고 그룹화 하는 방법을 나타냅니다.  
  
 Geography 차원에는 다음과 같은 멤버 집합이 있습니다.  
  
```console
{All, North America, Europe, Canada, USA, UK, Germany, Canada-West,  
Canada-East, USA-NW, USA-SW, USA-NE, USA-SE, England, Scotland,   
Wales,Ireland, Germany-North, Germany-South, Ottawa, Toronto,   
Vancouver, Calgary, Seattle, Boise, Los Angeles, Houston,   
Shreveport, Miami, Boston, New York, London, Dover, Glasgow,   
Edinburgh, Cardiff, Pembroke, Belfast, Derry, Berlin,   
Hamburg, Munich, Stuttgart}  
```  
  
### <a name="hierarchies"></a>계층 구조  
 계층은 차원 수준을 "롤업" 하거나 그룹화 하는 방법을 정의 합니다. 차원에 둘 이상의 계층이 있을 수 있습니다. Geography 차원에는 자연 계층이 있습니다.  
  
### <a name="levels"></a>Levels  
 위의 그림에 나온 예제 Geography 차원에서 각 상자는 계층의 수준을 나타냅니다.  
  
 각 수준에는 다음과 같은 멤버 집합이 있습니다.  
  
-   전 세계`= {All}`  
  
-   대륙`= {North America, Europe}`  
  
-   서양`= {Canada, USA, UK, Germany}`  
  
-   영역만`= {Canada-East, Canada-West, USA-NE, USA-NW, USA-SE, USA-SW, England, Ireland, Scotland, Wales, Germany-North, Germany-South}`  
  
-   건설`= {Ottawa, Toronto, Vancouver, Calgary, Seattle, Boise, Los Angeles, Houston, Shreveport, Miami, Boston, New York, London, Dover, Glasgow, Edinburgh, Cardiff, Pembroke, Belfast, Derry, Berlin, Hamburg, Munich, Stuttgart}`  
  
### <a name="members"></a>멤버  
 계층의 리프 수준에 있는 멤버에는 자식이 없고 루트 수준의 멤버에는 부모가 없습니다. 다른 모든 멤버는 하나 이상의 부모 및 하나 이상의 자식을 가집니다. 예를 들어 Geography 차원에서 계층 트리의 부분 순회는 다음과 같은 부모-자식 관계를 생성 합니다.  
  
-   `{All} (parent of) {Europe, North America}`  
  
-   `{North America} (parent of) {Canada, USA}`  
  
-   `{USA} (parent of) {USA-NE, USA-NW, USA-SE, USA-SW}`  
  
-   `{USA-NW} (parent of) {Boise, Seattle}`  
  
 차원 마다 하나 이상의 계층 구조를 따라 멤버를 통합할 수 있습니다. 일 수준에서 Year 수준으로 롤업 하는 방법에는 두 가지가 있습니다.  
  
 또한이 예제에서는 다른 특징을 보여 줍니다. Year 계층의 주 수준 멤버가 Year-Quarter 계층의 수준에 표시 되지 않습니다. 따라서 계층 구조는 차원의 모든 멤버를 포함할 필요가 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [ADO MD 개체 모델](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO (다차원) (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [ADO MD를 사용한 프로그래밍](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [ADO MD와 함께 ADO 사용](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)   
 [다차원 데이터 작업](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)
