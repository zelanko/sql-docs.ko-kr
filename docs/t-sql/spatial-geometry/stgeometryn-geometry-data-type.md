---
title: STGeometryN(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STGeometryN_TSQL
- STGeometryN (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STGeometryN (geometry Data Type)
ms.assetid: 348c7047-3442-4590-8879-fe841e79058c
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 8eb3644652d826744b50b6980b0dbe0a42ae2d55
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67950204"
---
# <a name="stgeometryn-geometry-data-type"></a>STGeometryN(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

**기하 도형 컬렉션**에서 지정된 기하 도형을 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.STGeometryN ( expression )  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 1과 **geometrycollection**에 있는 **geometry** 인스턴스 수 사이의 **int** 식입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geometry**  
  
 CLR 반환 형식: **SqlGeometry**  
  
## <a name="remarks"></a>Remarks  
 이 메서드는 매개 변수가 `STNumGeometries()`의 결과보다 크면 **null**을 반환하고 *expression* 매개 변수가 1보다 작으면 **ArgumentOutOfRangeException**을 throw합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `MultiPoint``geometry collection`을 만들고 `STGeometryN()`을 사용하여 컬렉션의 두 번째 `geometry` 인스턴스를 찾습니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('MULTIPOINT(0 0, 13.5 2, 7 19)', 0);  
SELECT @g.STGeometryN(2).ToString();  
```  
  
## <a name="see-also"></a>참고 항목  
 [geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

