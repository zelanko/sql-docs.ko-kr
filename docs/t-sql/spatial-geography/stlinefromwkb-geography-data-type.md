---
description: STLineFromWKB(geography 데이터 형식)
title: STLineFromWKB(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STLineFromWKB (geography Data Type)
- STLineFromWKB_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STLineFromWKB method
ms.assetid: 8ac2b772-6673-4ba1-a7ab-3b4b5841560b
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: e90b8b95cfeee90bc6e582dc5a587d49ca313d40
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88445223"
---
# <a name="stlinefromwkb-geography-data-type"></a>STLineFromWKB(geography 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

OGC(Open Geospatial Consortium) WKB(Well-Known Binary) 표현의 **LineString geography** 인스턴스를 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
STLineFromWKB ( 'WKB_linestring' , SRID )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *WKB_linestring*  
 반환하려는 **LineString geography** 인스턴스의 WKB 표현입니다. *WKB_linestring* 은 **varbinary(max)** 식입니다.  
  
 *SRID*  
 반환할 **LineString geography** 인스턴스의 SRID(Spatial Reference ID)를 나타내는 **int** 식입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
 OGC 형식: **LineString**  
  
## <a name="remarks"></a>설명  
 이 메서드는 입력이 잘못된 경우 **FormatException** 을 throw합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `STLineFromWKB()`를 사용하여 `geography` 인스턴스를 만듭니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STLineFromWKB(0x010200000002000000D7A3703D0A975EC08716D9CEF7D34740CBA145B6F3955EC08716D9CEF7D34740, 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>참고 항목  
 [OGC 정적 지리 메서드](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  
