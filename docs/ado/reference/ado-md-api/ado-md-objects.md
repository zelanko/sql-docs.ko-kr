---
title: ADO MD 개체 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO MD, objects
- objects [ADO MD]
ms.assetid: 2a32e873-3282-4520-a7ed-89493f1da80e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 42b0aed3c63b1303e4d8743ea441348c351be822
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63062663"
---
# <a name="ado-md-objects"></a>ADO MD 개체

|||  
|-|-|  
|[Axis](../../../ado/reference/ado-md-api/axis-object-ado-md.md)|하나 이상의 차원 선택한 멤버를 포함 하는 셀 집합의 필터 축을 또는 위치를 나타냅니다.|  
|[Catalog](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)|다차원 스키마 정보 (큐브 기본 차원, 계층, 수준 및 멤버)는 다차원 데이터 (MDP 공급자)를 포함합니다.|  
|[Cell](../../../ado/reference/ado-md-api/cell-object-ado-md.md)|셀 집합에 포함 된 축 좌표의 교집합에서 데이터를 나타냅니다.|  
|[Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)|다차원 쿼리 결과를 나타냅니다. 큐브 또는 기타 셀 집합에서 선택 된 셀의 컬렉션입니다.|  
|[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)|관련된 차원 집합이 포함 된 다차원 스키마에서 큐브를 나타냅니다.|  
|[Dimension](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)|멤버 하나 이상의 계층 구조를 포함 하는 다차원 큐브의 차원 중 하나를 나타냅니다.|  
|[Hierarchy](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)|한 가지 방식을 있는 차원의 멤버를 집계 하거나 수 "롤업 합니다." 차원 하나 이상의 계층 구조에 따라 집계할 수 있습니다.|  
|[Level](../../../ado/reference/ado-md-api/level-object-ado-md.md)|계층에서 순위가 동일한 멤버 집합이 포함 되어 있습니다.|  
|[멤버](../../../ado/reference/ado-md-api/member-object-ado-md.md)|셀 집합의 축 따라 위치 멤버나 수준의 멤버의 자식을 큐브의 수준의 멤버를 나타냅니다.|  
|[위치](../../../ado/reference/ado-md-api/position-object-ado-md.md)|축 따라 점을 정의 하는 하나 이상의 다른 차원 멤버의 집합을 나타냅니다.|  
  
 또한 합니다 **카탈로그** ADO 개체를 연결할 **연결** 표준 ADO 라이브러리에 포함 된 개체:  
  
|Object|Description|  
|------------|-----------------|  
|[연결](../../../ado/reference/ado-api/connection-object-ado.md)|데이터 원본에 대해 열린 연결을 나타냅니다.|  
  
 이러한 개체 간의 관계에 설명 되어 있습니다 합니다 [ADO MD 개체 모델](../../../ado/reference/ado-md-api/ado-md-object-model.md)합니다.  
  
 ADO MD 개체의 수는 해당 컬렉션에 포함할 수 있습니다. 예를 들어를 [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) 개체에 포함 될 수는 [CubeDefs](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md) 의 컬렉션을 **카탈로그**합니다. 자세한 내용은 [ADO MD 컬렉션](../../../ado/reference/ado-md-api/ado-md-collections.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ADO MD API 참조](../../../ado/reference/ado-md-api/ado-md-api-reference.md)   
 [ADO MD 코드 예제](../../../ado/reference/ado-md-api/ado-md-code-examples.md)   
 [ADO MD 컬렉션](../../../ado/reference/ado-md-api/ado-md-collections.md)   
 [ADO MD 열거 상수](../../../ado/reference/ado-md-api/ado-md-enumerated-constants.md)   
 [ADO MD 메서드](../../../ado/reference/ado-md-api/ado-md-methods.md)   
 [ADO MD 개체 모델](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO MD 속성](../../../ado/reference/ado-md-api/ado-md-properties.md)
