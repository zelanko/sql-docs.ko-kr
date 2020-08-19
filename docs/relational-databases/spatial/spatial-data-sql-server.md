---
description: 공간 데이터(SQL Server)
title: 공간 데이터(SQL Server) | Microsoft 문서
ms.date: 10/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- geography data type [SQL Server], spatial storage design
- planar spatial data [SQL Server], designing
- spatial data types [SQL Server]
- geodetic spatial data [SQL Server]
- geometry data type [SQL Server], spatial storage design
- spatial storage [SQL Server]
- geodetic spatial data [SQL Server], designing
ms.assetid: 41a132a1-09e2-4426-b9df-225270cb8e15
author: MladjoA
ms.author: mlandzic
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 38df38923b69bf24432cf4d5d162187c0962fcfc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88403349"
---
# <a name="spatial-data-sql-server"></a>공간 데이터(SQL Server)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  공간 데이터는 기하학적 개체의 물리적 위치 및 모양 정보를 나타냅니다. 이러한 개체는 지점 위치이거나 국가, 도로 또는 호수와 같은 더 복잡한 개체일 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 **geometry** 데이터 형식 및 **geography** 데이터 형식의 두 가지 공간 데이터 형식을 지원합니다.  
  
-   **geometry** 형식은 유클리드(평면) 좌표계의 데이터를 나타냅니다.  
  
-   **geography** 형식은 둥근 표면 좌표계의 데이터를 나타냅니다.  
  
 두 가지 데이터 형식 모두 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 .NET CLR(공용 언어 런타임) 데이터 형식으로 구현됩니다.  
  
##  <a name="related-tasks"></a><a name="reltasks"></a> 관련 작업  
 [geometry 인스턴스 만들기, 구성 및 쿼리](../../relational-databases/spatial/create-construct-and-query-geometry-instances.md)  
 geometry 데이터 형식의 인스턴스를 사용하는 방법에 대해 설명합니다.  
  
 [geography 인스턴스 만들기, 구성 및 쿼리](../../relational-databases/spatial/create-construct-and-query-geography-instances.md)  
 geography 데이터 형식의 인스턴스를 사용하는 방법에 대해 설명합니다.  
  
 [가장 인접한 항목의 공간 데이터 쿼리](../../relational-databases/spatial/query-spatial-data-for-nearest-neighbor.md)  
 특정 공간 개체에 가장 가까운 공간 개체를 찾는 데 사용되는 일반 쿼리 패턴에 대해 설명합니다.  
  
 [공간 인덱스 만들기, 수정 및 삭제](../../relational-databases/spatial/create-modify-and-drop-spatial-indexes.md)  
 공간 인덱스를 생성, 변경 및 삭제하는 방법에 대해 설명합니다.  
  
## <a name="related-content"></a>관련 내용  
 [공간 데이터 형식 개요](../../relational-databases/spatial/spatial-data-types-overview.md)  
 공간 데이터 형식을 소개합니다.  
  
-   [Point](../../relational-databases/spatial/point.md)  
  
-   [LineString](../../relational-databases/spatial/linestring.md)  
  
-   [CircularString](../../relational-databases/spatial/circularstring.md)  
  
-   [CompoundCurve](../../relational-databases/spatial/compoundcurve.md)  
  
-   [Polygon](../../relational-databases/spatial/polygon.md)  
  
-   [CurvePolygon](../../relational-databases/spatial/curvepolygon.md)  
  
-   [MultiPoint](../../relational-databases/spatial/multipoint.md)  
  
-   [MultiLineString](../../relational-databases/spatial/multilinestring.md)  
  
-   [MultiPolygon](../../relational-databases/spatial/multipolygon.md)  
  
-   [GeometryCollection](../../relational-databases/spatial/geometrycollection.md)  
  
 [공간 인덱스 개요](../../relational-databases/spatial/spatial-indexes-overview.md)  
 공간 인덱스를 소개하고 공간 분할 및 공간 분할 구성표에 대해 설명합니다.  
  
  
