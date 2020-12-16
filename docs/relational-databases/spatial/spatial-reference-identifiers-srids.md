---
description: SRID(Spatial Reference Identifier)
title: SRID(Spatial Reference Identifier) | Microsoft 문서
ms.date: 03/29/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Spatial Reference Identifiers (SRIDs)
- geodetic spatial data [SQL Server], identifiers
- SRID
ms.assetid: 0612658a-7d1b-4178-bdc2-42b914ea31a7
author: MladjoA
ms.author: mlandzic
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2873242ab181ce3d550c5b4f2274fef368d5c0f8
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97473134"
---
# <a name="spatial-reference-identifiers-srids"></a>SRID(Spatial Reference Identifier)
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]
  각 공간 인스턴스에는 SRID(spatial reference identifier)가 있습니다. SRID는 평면 지구 매핑 또는 둥근 지구 매핑에 사용되는 특정 타원면을 기준으로 하는 공간 참조 시스템에 해당합니다.  
  
 공간 열은 SRID가 다른 개체를 포함할 수 있습니다. 그러나 SRID가 같은 단일 공간 인스턴스만 데이터에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 공간 데이터 메서드를 사용하는 작업을 수행할 때 사용할 수 있습니다. 두 공간 데이터 인스턴스에서 파생되는 모든 공간 메서드의 결과는 이러한 인스턴스에 동일한 SRID가 있을 경우에만 유효합니다. 이 SRID는 인스턴스의 좌표를 결정하는 데 사용되는 동일한 측정 단위, 데이터 및 프로젝션을 기준으로 합니다. 가장 일반적인 SRID의 측정 단위는 미터 또는 제곱미터입니다.  
  
 두 공간 인스턴스의 SRID가 같지 않을 경우 이 인스턴스에서 사용되는 **geometry** 또는 **geography** 데이터 형식 메서드의 결과로 NULL이 반환됩니다. 예를 들어 NULL이 아닌 결과를 반환하는 다음 조건자 조건의 경우 **및** 의 두 `geometry1` geometry `geometry2`인스턴스의 SRID가 같아야 합니다.  
  
 `geometry1.STIntersects(geometry2) = 1`  
  
> [!NOTE]  
>  공간 참조 확인 시스템은 지도 제작, 측량 및 측지 데이터 스토리지를 위해 개발된 표준 집합인 [EPSG(European Petroleum Survey Group)](https://go.microsoft.com/fwlink/?LinkId=99349) 표준에 따라 정의됩니다. 이 표준은 OGP(Oil and Gas Producers) Surveying and Positioning Committee에서 소유하고 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [공간 데이터 형식 개요](../../relational-databases/spatial/spatial-data-types-overview.md)  
  
  
