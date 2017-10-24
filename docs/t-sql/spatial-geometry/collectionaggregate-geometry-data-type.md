---
title: "CollectionAggregate (geometry 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- CollectionAggregate method (geometry)
ms.assetid: b7c85d59-c841-4b7f-9d46-8b4b7f2a3afe
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2acf5b0fe7f3b6833f56f5264844e4dc9870155f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="collectionaggregate-geometry-data-type"></a>CollectionAggregate(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

만듭니다는 **GeometryCollection** 집합에서 인스턴스 **geometry** 형식입니다.
  
## <a name="syntax"></a>구문  
  
```  
  
CollectionAggregate ( geometry_operand )  
```  
  
## <a name="arguments"></a>인수  
 *geometry_operand*  
 한 **기 하 도형** 형식 테이블 열 집합을 나타내는 **기 하 도형** 개체에는 **GeometryCollection** 인스턴스.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **기 하 도형**  
  
## <a name="exceptions"></a>예외  
 유효하지 않은 입력 값이 있는 경우 `FormatException`을 발생시킵니다. 참조 [STIsValid &#40; geometry 데이터 형식 &#41;](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)  
  
## <a name="remarks"></a>주의  
 메서드 반환 **null** 경우 입력이 비어 있거나 입력에 다른 srid가 있습니다. 참조 [Spatial Reference Identifier &#40; Srid &#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)  
  
 메서드는 무시 **null** 입력 합니다.  
  
> [!NOTE]  
>  메서드 반환 **null** 경우는 모든 입력 값 **null**합니다.  
  
## <a name="examples"></a>예  
 다음 예는 `GeometryCollection` 및 `CurvePolygon`을 포함하는 `Polygon` 인스턴스를 반환합니다.  
  
 ```
 -- Setup table variable for CollectionAggregate example  
 DECLARE @Geom TABLE  
 (  
 shape geometry,  
 shapeType nvarchar(50)  
 )  
 INSERT INTO @Geom(shape,shapeType) VALUES('CURVEPOLYGON(CIRCULARSTRING(2 3, 4 1, 6 3, 4 5, 2 3))', 'Circle'),  
 ('POLYGON((1 1, 4 1, 4 5, 1 5, 1 1))', 'Rectangle');  
 -- Perform CollectionAggregate on @Geom.shape column  
 SELECT geometry::CollectionAggregate(shape).ToString()  
 FROM @Geom;
 ```  
  
## <a name="see-also"></a>관련 항목:  
 [확장 정적 기 하 도형 메서드](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  


