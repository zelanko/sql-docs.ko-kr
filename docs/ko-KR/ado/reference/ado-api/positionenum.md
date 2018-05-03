---
title: PositionEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- PositionEnum
helpviewer_keywords:
- PositionEnum enumeration
ms.assetid: e69af0a5-3405-4b72-9c6e-6b188ff746fd
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7c44bea1a7294b12992a7f2f76abac932f0921cf
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="positionenum"></a>PositionEnum
내에서 레코드 포인터의 현재 위치를 지정 된 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)합니다.  
  
|상수|Value|Description|  
|--------------|-----------|-----------------|  
|**adPosBOF**|-2|BOF에 현재 레코드 포인터 임을 나타냅니다 (즉,는 [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 속성은 **True**).|  
|**adPosEOF**|-3|EOF에 현재 레코드 포인터 임을 나타냅니다 (즉,는 [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 속성은 **True**).|  
|**adPosUnknown**|-1|나타냅니다는 **레코드 집합** 가 비어 있는 경우 현재 위치를 알 수 없습니다, 또는 공급자가 지원 하지는 [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) 또는 [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) 속성입니다.|  
  
## <a name="adowfc-equivalent"></a>해당 하는 ADO/WFC  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.Position.BOF|  
|AdoEnums.Position.EOF|  
|AdoEnums.Position.UNKNOWN|  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[AbsolutePage 속성(ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)|[AbsolutePosition 속성(ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|
