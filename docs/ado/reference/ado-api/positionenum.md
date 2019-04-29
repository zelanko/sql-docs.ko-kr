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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 21a2ea98ea4592d9900cd9623502a8d918b34c9b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63027846"
---
# <a name="positionenum"></a>PositionEnum
내에서 레코드 포인터의 현재 위치를 지정 된 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adPosBOF**|-2|현재 레코드 포인터 BOF 임을 나타냅니다 (즉, 합니다 [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 속성은 **True**).|  
|**adPosEOF**|-3|EOF에 현재 레코드 포인터 임을 나타냅니다 (즉, 합니다 [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 속성은 **True**).|  
|**adPosUnknown**|-1|나타내는 합니다 **레코드 집합** 는 빈, 현재 위치가 알 수 없는, 또는 공급자를 지원 하지 않습니다는 [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) 또는 [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) 속성입니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 해당  
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
