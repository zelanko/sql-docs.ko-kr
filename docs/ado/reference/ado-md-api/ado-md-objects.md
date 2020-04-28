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
ms.openlocfilehash: d568ca20cca6c12a04c0f3d54a2c134d59a0d7fc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67930571"
---
# <a name="ado-md-objects"></a>ADO MD 개체

|||  
|-|-|  
|[축](../../../ado/reference/ado-md-api/axis-object-ado-md.md)|하나 이상의 차원에서 선택한 멤버를 포함 하는 셀 집합의 위치 또는 필터 축을 나타냅니다.|  
|[카탈로그](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)|.MDP (multidimensional data provider)와 관련 된 다차원 스키마 정보 (즉, 큐브 및 기본 차원, 계층, 수준 및 멤버)를 포함 합니다.|  
|[Cell](../../../ado/reference/ado-md-api/cell-object-ado-md.md)|셀 집합에 포함 된 축 좌표와 교차 하는 데이터를 나타냅니다.|  
|[Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)|다차원 쿼리 결과를 나타냅니다. 큐브 또는 다른 셀 집합에서 선택 된 셀의 컬렉션입니다.|  
|[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)|관련 차원 집합을 포함 하는 다차원 스키마의 큐브를 나타냅니다.|  
|[차원](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)|하나 이상의 멤버 계층을 포함 하는 다차원 큐브의 차원 중 하나를 나타냅니다.|  
|[계층](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)|차원의 멤버를 집계 하거나 "롤업" 할 수 있는 한 가지 방법을 나타냅니다. 하나 이상의 계층 구조를 따라 차원을 집계할 수 있습니다.|  
|[Level](../../../ado/reference/ado-md-api/level-object-ado-md.md)|에는 계층 구조 내에서 순위가 동일한 멤버 집합이 포함 되어 있습니다.|  
|[멤버](../../../ado/reference/ado-md-api/member-object-ado-md.md)|큐브의 수준 멤버, 수준 멤버의 자식 또는 셀 집합의 축에 있는 위치의 멤버를 나타냅니다.|  
|[놓을](../../../ado/reference/ado-md-api/position-object-ado-md.md)|축의 한 지점을 정의 하는 여러 차원의 멤버 집합을 나타냅니다.|  
  
 또한 **카탈로그** 개체는 표준 ado 라이브러리에 포함 된 ado **연결** 개체에 연결 됩니다.  
  
|Object|Description|  
|------------|-----------------|  
|[연결](../../../ado/reference/ado-api/connection-object-ado.md)|데이터 소스에 대해 열려 있는 연결을 나타냅니다.|  
  
 이러한 개체 간의 관계는 [ADO MD 개체 모델](../../../ado/reference/ado-md-api/ado-md-object-model.md)에 나와 있습니다.  
  
 많은 ADO MD 개체를 해당 컬렉션에 포함할 수 있습니다. 예를 들어 [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) 개체는 **카탈로그**의 [CubeDefs](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md) 컬렉션에 포함 될 수 있습니다. 자세한 내용은 [ADO MD 컬렉션](../../../ado/reference/ado-md-api/ado-md-collections.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [ADO MD API 참조](../../../ado/reference/ado-md-api/ado-md-api-reference.md)   
 [ADO MD 코드 예제](../../../ado/reference/ado-md-api/ado-md-code-examples.md)   
 [ADO MD 컬렉션](../../../ado/reference/ado-md-api/ado-md-collections.md)   
 [ADO MD 열거 상수](../../../ado/reference/ado-md-api/ado-md-enumerated-constants.md)   
 [ADO MD 메서드](../../../ado/reference/ado-md-api/ado-md-methods.md)   
 [ADO MD 개체 모델](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO MD 속성](../../../ado/reference/ado-md-api/ado-md-properties.md)
