---
title: M(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d7304d3ab7af6673170c8228395300476457704e
ms.sourcegitcommit: a6596c62f607041c4402f7d5b41a232fca257c14
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36239683"
---
# <a name="m-geometry-data-type"></a>M(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  **geometry** 인스턴스의 **M**(측정값) 값입니다. 측정값의 의미 체계는 사용자가 정의합니다.  

## <a name="syntax"></a>구문  
  
```  
  
.M  
```  
  
## <a name="arguments"></a>인수  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 형식: **float**  
  
 CLR 형식: **SqlDouble**  
  
## <a name="remarks"></a>Remarks  
 **geometry** 인스턴스가 **Point**이 아닌 경우 및 해당 값이 설정되지 않은 모든 **Point** 인스턴스의 경우 이 속성의 값은 Null입니다.  
  
 이 속성은 읽기 전용입니다.  
  
 **M** 값은 어떠한 라이브러리 계산에도 사용되지 않으며 어떠한 라이브러리 계산을 통해서도 얻을 수 없습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 Z(높이) 값과 M(측정값) 값이 있는 `Point` 인스턴스를 만들고 `M`을 사용하여 인스턴스의 M 값을 인출합니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(1 2 3 4)', 0);  
SELECT @g.M;  
```  
  
## <a name="see-also"></a>참고 항목  
 [Geometry 인스턴스의 확장 메서드](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [Z&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/z-geometry-data-type.md)   
 [AsTextZM&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/astextzm-geometry-data-type.md)  
  
  

