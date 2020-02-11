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
ms.openlocfilehash: d5f7ca47177a953313ff983bb25f9178b73b4930
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67917601"
---
# <a name="positionenum"></a>PositionEnum
레코드 [집합](../../../ado/reference/ado-api/recordset-object-ado.md)내에서 레코드 포인터의 현재 위치를 지정 합니다.  
  
|지속적임|값|Description|  
|--------------|-----------|-----------------|  
|**adPosBOF**|-2|현재 레코드 포인터가 BOF에 있음을 나타냅니다 (즉, [bof](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 속성이 **True**임).|  
|**adPosEOF**|-3|현재 레코드 포인터가 EOF에 있음을 나타냅니다. 즉, [eof](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 속성이 **True**입니다.|  
|**adPosUnknown**|-1|는 **레코드 집합이** 비어 있거나, 현재 위치를 알 수 없거나, 공급자가 [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) 또는 [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) 속성을 지원 하지 않음을 나타냅니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 Package: **com.ms.wfc.data**  
  
|지속적임|  
|--------------|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums. 알 수 없음|  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[AbsolutePage 속성(ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)|[AbsolutePosition 속성(ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|
