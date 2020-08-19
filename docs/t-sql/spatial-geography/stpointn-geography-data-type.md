---
description: STPointN(geography 데이터 형식)
title: STPointN (geography Data Type) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STPointN_TSQL
- STPointN (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STPointN method
ms.assetid: 47670feb-b9e0-4b4b-af83-b9bba7da66ac
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 00604f3066c746057e1ffaaefc0cffb00244d57b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88459005"
---
# <a name="stpointn-geography-data-type"></a>STPointN(geography 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  **geography** 인스턴스의 지정된 지점을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STPointN ( expression )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *expression*  
 1과 **geography** 인스턴스에 있는 곡선의 개수 사이의 **int** 식입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
 OGC(Open Geospatial Consortium) 형식: **Point**  
  
## <a name="remarks"></a>설명  
 사용자가 **geography** 인스턴스를 만든 경우 STPointN()는 *expression*을 통해 지정된 점을 원래 입력된 순서대로 정렬하여 반환합니다.  
  
 시스템에서 **geography** 인스턴스를 생성한 경우 STPointN()은 *식*을 통해 지정한 점을 모두 출력 순서와 동일하게 **geography** 인스턴스, 이 인스턴스 내의 링(해당되는 경우), 이 링 내의 점 순서로 정렬하여 반환합니다. 이 순서는 결정적입니다.  
  
 1보다 작은 값을 사용하여 이 메서드를 호출하면 이 메서드는 **ArgumentOutOfRangeException**을 throw합니다.  
  
 인스턴스에 있는 점 개수보다 큰 값을 사용하여 이 메서드를 호출하면 이 메서드는 Null을 반환합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `LineString` 인스턴스를 만들고 `STPointN()`을 사용하여 인스턴스의 설명에 있는 두 번째 점을 검색합니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STPointN(2).ToString();  
```  
  
## <a name="see-also"></a>참고 항목  
 [Geography 인스턴스의 OGC 메서드](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
