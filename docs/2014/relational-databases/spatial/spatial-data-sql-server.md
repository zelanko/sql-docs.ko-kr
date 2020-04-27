---
title: 공간 데이터(SQL Server) | Microsoft 문서
ms.date: 06/14/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 7bd529f67f9184f86d4a9ec704e9cf7af972f3f3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66014062"
---
# <a name="spatial-data-sql-server"></a>공간 데이터(SQL Server)
  공간 데이터는 기하학적 개체의 물리적 위치 및 모양 정보를 나타냅니다. 이러한 개체는 지점 위치이거나 국가, 도로 또는 호수와 같은 더 복잡한 개체일 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는: the `geometry` 데이터 형식 및 `geography` 데이터 형식의 두 가지 공간 데이터 형식을 지원합니다.  
  
-   `geometry` 유형은 유클리드(평면) 좌표계의 데이터를 나타냅니다.  
  
-   `geography` 형식은 둥근 표면 좌표 시스템의 데이터를 나타냅니다.  
  
 두 가지 데이터 형식 모두 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 .NET CLR(공용 언어 런타임) 데이터 형식으로 구현됩니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]의 새로운 공간 기능에 대한 자세한 설명 및 예제를 보려면 [SQL Server 2012의 새로운 공간 기능](https://go.microsoft.com/fwlink/?LinkId=226407)백서를 다운로드하세요.  
  
##  <a name="related-tasks"></a><a name="reltasks"></a> 관련 작업  
 [geometry 인스턴스 만들기, 구성 및 쿼리](create-construct-and-query-geometry-instances.md)  
 geometry 데이터 형식의 인스턴스를 사용하는 방법에 대해 설명합니다.  
  
 [geography 인스턴스 만들기, 구성 및 쿼리](create-construct-and-query-geography-instances.md)  
 geography 데이터 형식의 인스턴스를 사용하는 방법에 대해 설명합니다.  
  
 [가장 인접한 항목의 공간 데이터 쿼리](query-spatial-data-for-nearest-neighbor.md)  
 특정 공간 개체에 가장 가까운 공간 개체를 찾는 데 사용되는 일반 쿼리 패턴에 대해 설명합니다.  
  
 [공간 인덱스 만들기, 수정 및 삭제](create-modify-and-drop-spatial-indexes.md)  
 공간 인덱스를 생성, 변경 및 삭제하는 방법에 대해 설명합니다.  
  
## <a name="related-content"></a>관련 내용  
 [공간 데이터 형식 개요](spatial-data-types-overview.md)  
 공간 데이터 형식을 소개합니다.  
  
-   [Point](point.md)  
  
-   [LineString](linestring.md)  
  
-   [CircularString](circularstring.md)  
  
-   [CompoundCurve](compoundcurve.md)  
  
-   [Polygon](polygon.md)  
  
-   [CurvePolygon](curvepolygon.md)  
  
-   [MultiPoint](multipoint.md)  
  
-   [MultiLineString](multilinestring.md)  
  
-   [MultiPolygon](multipolygon.md)  
  
-   [GeometryCollection](geometrycollection.md)  
  
 [공간 인덱스 개요](spatial-indexes-overview.md)  
 공간 인덱스를 소개하고 공간 분할 및 공간 분할 구성표에 대해 설명합니다.  
  
  
