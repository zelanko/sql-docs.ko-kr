---
title: ADCPROP_AUTORECALC_ENUM | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADCPROP_AUTORECALC_ENUM
helpviewer_keywords:
- ADCPROP_AUTORECALC_ENUM [ADO]
ms.assetid: ded4f087-87b9-4efa-8026-bde53d3e9e8a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 738f4cece8cf2355c12c0de4ac42314152c6370a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67921449"
---
# <a name="adcprop_autorecalc_enum"></a>ADCPROP_AUTORECALC_ENUM
[MSDataShape](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) 공급자가 계층적 레코드 집합에서 집계 열과 계산 된 열을 다시 계산 하는 시기를 지정 합니다.  
  
 이러한 상수는 **MSDataShape** 공급자 및 **레코드 집합** "**자동**다시 계산" 동적 속성에만 사용 됩니다 .이 속성은 [ADO 동적 속성 인덱스](../../../ado/reference/ado-api/ado-dynamic-property-index.md) 에서 참조 되며 [Microsoft Cursor service for OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) 또는 [microsoft Data 셰이핑 service for OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) 설명서에 설명 되어 있습니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adRecalcAlways**|1|기본값 **MSDataShape** 공급자가 계산 된 열에 종속 된 값이 변경 될 때마다 다시 계산 합니다.|  
|**adRecalcUpFront**|0|계층 구조 **레코드 집합**을 처음 만들 때만 계산 합니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 이러한 상수에는 ADO/WFC 해당 항목이 없습니다.
