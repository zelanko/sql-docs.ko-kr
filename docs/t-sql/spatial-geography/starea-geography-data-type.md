---
title: "STArea (geography 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STArea (geography Data Type)
- STArea_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STArea method
ms.assetid: cfc0b0e0-7fde-431a-863f-d13f3b1b1bef
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2082c36f483e1ebe6d532abb6d3335db127b21b1
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="starea-geography-data-type"></a>STArea(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  전체 표면적 반환는 **geography** 인스턴스. Spatial reference identifier에 사용 되는 측정 단위의 제곱 STArea()에 대 한 결과가 반환 될는 **geography** 인스턴스; 예를 들어 인스턴스의 SRID 4326 이면 STArea() 결과 반환 제곱 미터입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STArea ( )  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **float**  
  
 CLR 반환 형식: **SqlDouble**  
  
## <a name="remarks"></a>주의  
 STArea() 경우 0을 반환 합니다는 **geography** 인스턴스가 0 및 1 차원 도형만 포함 하거나 비어 있는 경우.  
  
> [!NOTE]  
>  에 대 한 메서드는 **geography** 데이터 입력을 생성 하는 메트릭 반환 값은 메서드에서 사용 되는 인스턴스의 SRID에 따라 다른 결과 갖게 됩니다. Srid에 대 한 자세한 내용은 참조 하세요. [Spatial Reference Identifier &#40; Srid &#41; ](../../relational-databases/spatial/spatial-reference-identifiers-srids.md).  
  
## <a name="examples"></a>예  
 다음 예제에서는 `STArea()` 만들려는 `Polygon``geography` 인스턴스 선택한 다각형의 면적을 계산 합니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SELECT @g.STArea();  
```  
  
## <a name="see-also"></a>관련 항목:  
 [지리 인스턴스의 OGC 메서드](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
