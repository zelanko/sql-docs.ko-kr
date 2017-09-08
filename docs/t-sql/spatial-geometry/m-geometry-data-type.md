---
title: "M (geometry 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- M (geometry Data Type)
- M_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- M (geometry Data Type)
ms.assetid: 443ae2ea-739b-41ef-96cc-ac5dfd65e10b
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0946bc24abaee28973f8afd409ac68d04a428c8d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="m-geometry-data-type"></a>M(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  **M** (측정값) 값은 **geometry** 인스턴스. 측정값의 의미 체계는 사용자가 정의합니다.  

## <a name="syntax"></a>구문  
  
```  
  
.M  
```  
  
## <a name="arguments"></a>인수  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]형식: **float**  
  
 CLR 형식: **SqlDouble**  
  
## <a name="remarks"></a>주의  
 이 속성의 값이 null 경우는 **기 하 도형** 인스턴스가 않습니다는 **지점**뿐만 아니라 모든 **지점** 인스턴스 설정 되지 않은에 대 한 합니다.  
  
 이 속성은 읽기 전용입니다.  
  
 **M** 값 어떠한 라이브러리 계산에 사용 되지 않는, 어떠한 라이브러리 계산을 통해 수행 되지 것입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 Z(높이) 값과 M(측정값) 값이 있는 `Point` 인스턴스를 만들고 `M`을 사용하여 인스턴스의 M 값을 인출합니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(1 2 3 4)', 0);  
SELECT @g.M;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Geometry 인스턴스의 확장된 메서드](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [Z &#40; geometry 데이터 형식 &#41;](../../t-sql/spatial-geometry/z-geometry-data-type.md)   
 [AsTextZM&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/astextzm-geometry-data-type.md)  
  
  


