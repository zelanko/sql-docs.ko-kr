---
title: "Z (geometry 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 08/03/2017
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
- Z (geometry Data Type)
- Z_(geometry_Data_Type)_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Z (geometry Data Type)
ms.assetid: a62ed736-44df-4591-9109-ce90e1df9bd3
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8a490bed46d662a6bf73a5428a42019b893cfd4f
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="z-geometry-data-type"></a>Z(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

인스턴스의 Z(높이) 값입니다. 높이 값의 의미 체계는 사용자가 정의합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.Z  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]형식: **float**  
  
 CLR 형식: **SqlDouble**  
  
## <a name="remarks"></a>주의  
 이 속성의 값 geometry 인스턴스는 지점 없으면 null이 됩니다 모든 **가리킨** 인스턴스에 대해 설정 되지 않은입니다.  
  
 이 속성은 읽기 전용입니다.  
  
 Z 좌표는 어떠한 라이브러리 계산에도 사용되지 않으며 어떠한 라이브러리 계산을 통해서도 얻을 수 없습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 Z(높이) 값과 M(측정값) 값이 있는 `Point` 인스턴스를 만들고 `Z`를 사용하여 인스턴스의 Z값을 인출합니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(1 2 3 4)', 0);  
SELECT @g.Z;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [M &#40; geometry 데이터 형식 &#41;](../../t-sql/spatial-geometry/m-geometry-data-type.md)   
 [Astextzm&#40; geometry 데이터 형식 &#41;](../../t-sql/spatial-geometry/astextzm-geometry-data-type.md)   
 [geometry 인스턴스의 확장 메서드](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

