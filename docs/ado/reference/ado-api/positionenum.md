---
title: PositionEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- PositionEnum
helpviewer_keywords:
- PositionEnum enumeration
ms.assetid: e69af0a5-3405-4b72-9c6e-6b188ff746fd
author: rothja
ms.author: jroth
ms.openlocfilehash: 6a61dae9888628302da3326a1465f4182c49e39c
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243224"
---
# <a name="positionenum"></a>PositionEnum
레코드 [집합](../../../ado/reference/ado-api/recordset-object-ado.md)내에서 레코드 포인터의 현재 위치를 지정 합니다.  
  
|상수|값|설명|  
|--------------|-----------|-----------------|  
|**adPosBOF**|-2|현재 레코드 포인터가 BOF에 있음을 나타냅니다 (즉, [bof](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 속성이 **True**임).|  
|**adPosEOF**|-3|현재 레코드 포인터가 EOF에 있음을 나타냅니다. 즉, [eof](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 속성이 **True**입니다.|  
|**adPosUnknown**|-1|는 **레코드 집합이** 비어 있거나, 현재 위치를 알 수 없거나, 공급자가 [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) 또는 [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) 속성을 지원 하지 않음을 나타냅니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums. 알 수 없음|  
  
## <a name="applies-to"></a>적용 대상  

:::row:::
    :::column:::
        [AbsolutePage 속성(ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)  
    :::column-end:::
    :::column:::
        [AbsolutePosition 속성(ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)  
    :::column-end:::
:::row-end:::
