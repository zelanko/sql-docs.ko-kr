---
title: "Z (geography 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Z (geography Data Type)
- Z_(geography_Data_Type)_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Z method
ms.assetid: 9abc79c5-43c9-4cc2-b37f-d2ecdec7c234
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f185da3a7aeabb751f0d871d6ad2c0132830d9d7
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="z-geography-data-type"></a>Z(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  인스턴스의 Z(높이) 값입니다. 높이 값의 의미 체계는 사용자가 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.Z  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]형식: **float**  
  
 CLR 형식: **SqlDouble**  
  
## <a name="remarks"></a>주의  
 이 속성의 값이 null 경우는 **geography** 인스턴스가 점이 아닌,도 모든 **가리킨** 인스턴스 설정 되지 않은에 대 한 합니다.  
  
 이 속성은 읽기 전용입니다.  
  
 Z 좌표는 어떠한 라이브러리 계산에도 사용되지 않으며 어떠한 라이브러리 계산을 통해서도 얻을 수 없습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 Z(높이) 값과 M(측정값) 값이 있는 `Point` 인스턴스를 만들고 `Z`를 사용하여 인스턴스의 Z값을 인출합니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100 10.3 12)', 4326);  
SELECT @g.Z;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Geography 인스턴스의 확장된 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [M &#40; geography 데이터 형식 &#41;](../../t-sql/spatial-geography/m-geography-data-type.md)   
 [AsTextZM&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/astextzm-geography-data-type.md)  
  
  
