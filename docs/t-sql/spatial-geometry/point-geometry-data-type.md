---
title: "지점 (geometry 데이터 형식) | Microsoft Docs"
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
- Point
- Point_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Point (geometry Data Type)
ms.assetid: 7a2e593a-4d4c-4214-b0c5-02d1ac46bc66
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e153b3bbaf18e6c4b69171e56f2fdae6965396a7
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="point-geometry-data-type"></a>Point(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

생성 된 **기 하 도형** 인스턴스를 나타내는 **지점** 해당 X 및 Y 값 및 SRID에서 인스턴스.
  
## <a name="syntax"></a>구문  
  
```  
  
Point ( X, Y, SRID )  
```  
  
## <a name="arguments"></a>인수  
 *X*  
 이 **float** 의 X 좌표를 나타내는 식은 **지점** 생성 되 고 합니다.  
  
 *Y*  
 이 **float** 의 Y 좌표를 나타내는 식은 **지점** 생성 되 고 합니다.  
  
 *SRID*  
 이 **int** spatial 나타내는 식 참조의 ID (SRID)는 **geometry** 반환할 인스턴스.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **기 하 도형**  
  
 CLR 반환 형식: **SqlGeometry**  
  
## <a name="remarks"></a>주의  
  
## <a name="examples"></a>예  
 다음 예에서는 `Point()`를 사용하여 `geometry` 인스턴스를 만듭니다.  
  
```  
DECLARE @g geometry;   
SET @g = geometry::Point(1, 10, 0);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>관련 항목:  
 [확장 정적 기 하 도형 메서드](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  


