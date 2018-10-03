---
title: 다차원 스키마 및 데이터에 대 한 개요 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- multidimensional schemas and data
ms.assetid: ce37fa06-c581-4d80-9a9b-c3aa66408909
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 70bd6f1867d48a9c96f5759d95c2a08a22714d8a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47811161"
---
# <a name="overview-of-multidimensional-schemas-and-data"></a>다차원 스키마 및 데이터 개요
## <a name="understanding-multidimensional-schemas"></a>다차원 스키마 이해  
 ADO MD에서 중앙 메타 데이터 개체를 *큐브*, 관련된 차원, 계층, 수준 및 멤버의 구조화 된 집합 구성 합니다.  
  
 A *차원* 은 비즈니스 엔터티에서 파생 된 다차원 데이터베이스에서 데이터의 개별 범주로 합니다. 일반적으로 차원 데이터베이스의 측정값에 대 한 쿼리 조건으로 사용할 항목을 포함 합니다.  
  
 A *계층* 차원의 집계의 경로입니다. 차원에 부모-자식 관계를 포함 하는 세분성의 여러 수준 있을 수 있습니다. 계층이 수준 간의 관계를 정의 합니다.  
  
 A *수준* 계층 구조의 집계의 단계입니다. 여러 계층의 정보를 사용 하 여 차원에 대 한 각 계층 수준입니다.  
  
 A *멤버* 차원 데이터 항목입니다. 일반적으로 캡션을 만들거나 멤버를 사용 하 여 데이터베이스의 측정값에 설명 합니다.  
  
 큐브에 표시 됩니다 [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) ADO MD.의 개체 차원, 계층, 수준 및 멤버의 해당 ADO MD 개체도 표시 됩니다. [차원](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)를 [계층](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)를 [수준](../../../ado/reference/ado-md-api/level-object-ado-md.md), 및 [ 멤버](../../../ado/reference/ado-md-api/member-object-ado-md.md)합니다.  
  
### <a name="dimensions"></a>차원  
 큐브 차원의 비즈니스 엔터티 및 데이터베이스에서 모델링 하는 데이터 형식에 따라 달라 집니다. 일반적으로 각 차원에는 독립적인 진입점 또는 데이터를 선택 하는 메커니즘입니다.  
  
 예를 들어 판매 데이터를 포함 하는 큐브에 다음과 같은 5 개의 차원을: 영업, Geography, 시간, 제품 및 측정값입니다. Measures 차원의 다른 차원과 분류 하 고 판매 데이터 값을 그룹화 하는 방법을 나타내는 동안 실제 판매 데이터 값을 포함 합니다.  
  
 Geography 차원에는 다음 멤버 집합에 있습니다.  
  
```  
{All, North America, Europe, Canada, USA, UK, Germany, Canada-West,  
Canada-East, USA-NW, USA-SW, USA-NE, USA-SE, England, Scotland,   
Wales,Ireland, Germany-North, Germany-South, Ottawa, Toronto,   
Vancouver, Calgary, Seattle, Boise, Los Angeles, Houston,   
Shreveport, Miami, Boston, New York, London, Dover, Glasgow,   
Edinburgh, Cardiff, Pembroke, Belfast, Derry, Berlin,   
Hamburg, Munich, Stuttgart}  
```  
  
### <a name="hierarchies"></a>계층 구조  
 계층에 있는 차원의 수준 수 될 "롤업" 또는 그룹화 방법을 정의 합니다. 차원에 둘 이상의 계층이 있을 수 있습니다. Geography 차원의 자연 계층을 있습니다.  
  
### <a name="levels"></a>Levels  
 이전 그림에 나온 예제에서는 Geography 차원에 각 상자에는 계층의 수준을 나타냅니다.  
  
 각 수준에는 다음과 같은 멤버를 집합:  
  
-   전 세계 `= {All}`  
  
-   대륙 `= {North America, Europe}`  
  
-   국가 `= {Canada, USA, UK, Germany}`  
  
-   지역 `= {Canada-East, Canada-West, USA-NE, USA-NW, USA-SE, USA-SW, England, Ireland, Scotland, Wales, Germany-North, Germany-South}`  
  
-   도시 `= {Ottawa, Toronto, Vancouver, Calgary, Seattle, Boise, Los Angeles, Houston, Shreveport, Miami, Boston, New York, London, Dover, Glasgow, Edinburgh, Cardiff, Pembroke, Belfast, Derry, Berlin, Hamburg, Munich, Stuttgart}`  
  
### <a name="members"></a>멤버  
 멤버를 계층의 리프 수준에 자식이 없는 및 루트 수준의 멤버는 부모가 없습니다. 다른 모든 멤버에 하나 이상의 부모 있고 자식이 하나 이상 있습니다. 예를 들어 Geography 차원에 계층 구조 트리의 부분 탐색은 다음과 같은 부모-자식 관계를 생성합니다.  
  
-   `{All} (parent of) {Europe, North America}`  
  
-   `{North America} (parent of) {Canada, USA}`  
  
-   `{USA} (parent of) {USA-NE, USA-NW, USA-SE, USA-SW}`  
  
-   `{USA-NW} (parent of) {Boise, Seattle}`  
  
 차원당 여러 계층 구조에 따라 멤버를 통합할 수 있습니다. 시간 차원 고려 일 수준에서 Year 수준으로 롤업 하는 방법은 두 가지 경우:  
  
 이 예제에서는 또한 다른 특징을 보여 줍니다: 주 수준의 년 주 계층의 일부 구성원이 연도 분기 계층 구조의 모든 수준에 표시 되지 않습니다. 따라서 계층을 차원의 모든 멤버 포함할 필요는 없습니다.  
  
## <a name="see-also"></a>관련 항목  
 [ADO MD 개체 모델](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO (다차원) (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [ADO MD를 사용한 프로그래밍](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [ADO MD를 사용 하 여 ADO를 사용 하 여](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)   
 [다차원 데이터 작업](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)
