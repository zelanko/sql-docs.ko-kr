---
title: STIsClosed(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STIsClosed (geography Data Type)
- STIsClosed_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STIsClosed method
ms.assetid: eba1643f-07c4-4500-8643-b7e90f908147
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7e9fd864ae5688e1d3540f54db54454ec1ff41db
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47663471"
---
# <a name="stisclosed-geography-data-type"></a>STIsClosed(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  주어진 **geography** 인스턴스의 시작점 및 끝점이 동일하면 1을 반환합니다. 포함된 각 **geography** 인스턴스가 닫혀 있으면 **geography** 컬렉션 형식에 대해 1을 반환합니다. 인스턴스가 닫혀 있지 않으면 0을 반환합니다.  
  
 이 **geography** 데이터 형식 메서드는 **FullGlobe** 인스턴스 또는 반구보다 큰 공간 인스턴스를 지원합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STIsClosed ( )  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **bit**  
  
 CLR 반환 형식: **SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 이 메서드는 **geography** 인스턴스의 도형이 점이거나 인스턴스가 비어 있으면 0을 반환합니다.  
  
 이 메서드는 **FullGlobe** 인스턴스가 또는 **Polygon** 또는 다른 유형의 인스턴스인 경우 True를 반환합니다.  
  
 모든 **Polygon** 인스턴스는 닫혀 있다고 간주됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Polygon` 인스턴스를 만들고 `STIsClosed()`를 사용하여 `Polygon`이 닫혀 있는지 테스트합니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SELECT @g.STIsClosed();  
```  
  
## <a name="see-also"></a>참고 항목  
 [지리 인스턴스의 OGC 메서드](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
