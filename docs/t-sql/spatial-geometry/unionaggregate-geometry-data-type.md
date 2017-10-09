---
title: "UnionAggregate (geometry 데이터 형식) | Microsoft Docs"
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
- UnionAggregate method (geometry)
ms.assetid: dc7929cc-55ca-4a2c-a4b9-f5452f95bde8
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 65759e7e4d7701b36d79b8ce27bb5bfe176ba3e3
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="unionaggregate-geometry-data-type"></a>UnionAggregate(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

geometry 개체 집합에서 통합 연산을 수행합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
UnionAggregate ( geometry_operand )  
```  
  
## <a name="arguments"></a>인수  
 *geometry_operand*  
 이 **기 하 도형** 의 집합을 보유 하는 형식 테이블 열 **기 하 도형** 통합 연산을 수행할 개체입니다.  
  
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
 집합의 합집합을 반환 하는 다음 예제에서는 **geometry** 테이블 변수에 개체입니다.  
 ```
 -- Setup table variable for UnionAggregate example 
 DECLARE @Geom TABLE 
 ( 
 shape geometry, 
 shapeType nvarchar(50) 
 ); 
 INSERT INTO @Geom(shape,shapeType) 
 VALUES('CURVEPOLYGON(CIRCULARSTRING(2 3, 4 1, 6 3, 4 5, 2 3))', 'Circle'), 
 ('POLYGON((1 1, 4 1, 4 5, 1 5, 1 1))', 'Rectangle'); 
 -- Perform UnionAggregate on @Geom.shape column 
 SELECT geometry::UnionAggregate(shape).ToString() 
 FROM @Geom;
``` 
  
## <a name="see-also"></a>관련 항목:  
 [확장 정적 기 하 도형 메서드](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  


