---
title: STGeomFromWKB(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STGeomFromWKB_TSQL
- STGeomFromWKB (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STGeomFromWKB method
ms.assetid: 79d39d88-5440-49a7-9247-190eafce3f4f
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 72bf7a6921f486ff202d73cf3678072b5ddb9039
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86555384"
---
# <a name="stgeomfromwkb-geography-data-type"></a>STGeomFromWKB(geography 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

OGN(Open Geospatial Consortium) WKB(WELL-KNOWN Binary) 표현에서 **geography** 인스턴스를 반환합니다.
  
이 **geography** 데이터 형식 메서드는 **FullGlobe** 인스턴스 또는 반구보다 큰 공간 인스턴스를 지원합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
STGeomFromWKB ( 'WKB_geography' , SRID )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *WKB_geography*  
 반환할 **geography** 인스턴스의 WKB 표현입니다. *WKB_geography*은 **varbinary(max)** 식입니다.  
  
 *SRID*  
 반환할 **geography** 인스턴스의 SRID(Spatial Reference ID)를 나타내는 **int** 식입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
## <a name="remarks"></a>설명  
 `STGeomFromText()`에 의해 반환되는 **geography** 인스턴스의 OGC 형식은 해당 WKB 입력으로 설정됩니다.  
  
 이 메서드는 입력이 잘못된 경우 **FormatException**을 throw합니다.  
  
 이 메서드는 입력에 대척점 끝이 있을 경우 **ArgumentException**을 throw합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `STGeomFromWKB()`를 사용하여 `geography` 인스턴스를 만듭니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromWKB(0x010200000002000000D7A3703D0A975EC08716D9CEF7D34740CBA145B6F3955EC08716D9CEF7D34740, 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>참고 항목  
 [OGC 정적 지리 메서드](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  
