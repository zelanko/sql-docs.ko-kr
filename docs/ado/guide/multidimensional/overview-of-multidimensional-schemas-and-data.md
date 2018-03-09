---
title: "다차원 스키마 및 데이터 개요 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- multidimensional schemas and data
ms.assetid: ce37fa06-c581-4d80-9a9b-c3aa66408909
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 518cb68ec75fb998ee2a53500db0dc096a38d678
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="overview-of-multidimensional-schemas-and-data"></a>다차원 스키마 및 데이터 개요
## <a name="understanding-multidimensional-schemas"></a>다차원 스키마 이해  
 ADO MD에서 중앙 메타 데이터 개체는는 *큐브*, 서로 관련 된 차원, 계층, 수준 및 멤버의 구조화 된 집합으로 구성 된 합니다.  
  
 A *차원* 은 다차원 데이터베이스, 비즈니스 엔터티에서 파생 된 데이터의 개별 범주로 합니다. 차원에는 일반적으로 데이터베이스의 측정값에 대 한 쿼리 조건으로 사용할 항목이 포함 됩니다.  
  
 A *계층* 차원의 집계의 경로입니다. 차원에는 부모-자식 관계를 포함 하는 여러 세분성 수준이 있을 수 있습니다. 계층이 수준 간의 관계를 정의 합니다.  
  
 A *수준* 계층 구조의 집계의 단계입니다. 여러 계층의 정보를 차원에 대 한 각 계층 수준입니다.  
  
 A *멤버* 은 차원에서 데이터 항목입니다. 일반적으로 캡션이 생성 하거나 멤버를 사용 하 여 데이터베이스의 측정값에 설명 합니다.  
  
 큐브가으로 표시 되는 [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) ADO MD.의 개체 차원, 계층, 수준 및 멤버의 해당 ADO MD 개체도 표시 됩니다: [차원](../../../ado/reference/ado-md-api/dimension-object-ado-md.md), [계층](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md), [수준](../../../ado/reference/ado-md-api/level-object-ado-md.md), 및 [ 멤버](../../../ado/reference/ado-md-api/member-object-ado-md.md)합니다.  
  
### <a name="dimensions"></a>차원  
 큐브의 차원 비즈니스 엔터티와 유형의 데이터를 데이터베이스에서 모델링에 따라 달라 집니다. 일반적으로 각 차원의 개별 진입점 또는 데이터를 선택 하는 메커니즘입니다.  
  
 예를 들어 판매 데이터를 포함 하는 큐브에 다음과 같은 5 개의 차원이: 영업 사원, Geography, 시간, 제품 및 측정값입니다. 측정값 차원 반면 다른 차원의 분류 및 판매 데이터 값을 그룹화 하는 방법을 나타냅니다 실제 판매 데이터 값을 포함 합니다.  
  
 Geography 차원에는 다음과 같은 멤버 집합이 있습니다.  
  
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
 계층 구조는 차원 수준 "롤업" 하거나 수 그룹화 방법을 정의 합니다. 차원에 둘 이상의 계층이 있을 수 있습니다. Geography 차원의 자연 계층이 있습니다.  
  
### <a name="levels"></a>Levels  
 위의 그림에 나온 예제에서는 Geography 차원에 각 상자에는 계층의 수준을 나타냅니다.  
  
 각 수준에는 다음과 같이 멤버 집합이:  
  
-   전 세계`= {All}`  
  
-   대륙`= {North America, Europe}`  
  
-   국가`= {Canada, USA, UK, Germany}`  
  
-   영역`= {Canada-East, Canada-West, USA-NE, USA-NW, USA-SE, USA-SW, England, Ireland, Scotland, Wales, Germany-North, Germany-South}`  
  
-   도시`= {Ottawa, Toronto, Vancouver, Calgary, Seattle, Boise, Los Angeles, Houston, Shreveport, Miami, Boston, New York, London, Dover, Glasgow, Edinburgh, Cardiff, Pembroke, Belfast, Derry, Berlin, Hamburg, Munich, Stuttgart}`  
  
### <a name="members"></a>멤버  
 멤버는 계층의 리프 수준에 자식이 없습니다. 있고 루트 수준에서 멤버는 부모가 없습니다. 다른 모든 멤버에 하나 이상의 부모 있고 자식이 하나 이상 있습니다. 예를 들어 Geography 차원에서 계층 구조 부분 탐색에는 다음과 같은 부모-자식 관계 생성 됩니다.  
  
-   `{All} (parent of) {Europe, North America}`  
  
-   `{North America} (parent of) {Canada, USA}`  
  
-   `{USA} (parent of) {USA-NE, USA-NW, USA-SE, USA-SW}`  
  
-   `{USA-NW} (parent of) {Boise, Seattle}`  
  
 차원당 하나 이상의 계층 구조에 따라 멤버를 통합할 수 있습니다. 시간 차원의 생각해 볼 수 있는 두 가지 방법으로 일 수준에서 연도 수준까지 이르는 수:  
  
 이 예제에서는 또한 또 다른 특성을 설명 합니다: 주 수준의 년 주 계층의 일부 구성원이 연도 분기 계층 구조의 모든 수준에 표시 되지 않습니다. 따라서 계층 차원의 모든 멤버를 포함 하지 않아야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ADO MD 개체 모델](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO (다차원) ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [ADO MD를 사용한 프로그래밍](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [ADO MD와 함께 ADO 사용](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)   
 [다차원 데이터 작업](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)
