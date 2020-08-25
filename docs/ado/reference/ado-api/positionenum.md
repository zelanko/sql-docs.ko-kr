---
description: PositionEnum
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
ms.openlocfilehash: 2d7b443e94f3bea5977aeaf953e84c66c826daeb
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88773172"
---
# <a name="positionenum"></a>PositionEnum
레코드 [집합](./recordset-object-ado.md)내에서 레코드 포인터의 현재 위치를 지정 합니다.  
  
|상수|값|설명|  
|--------------|-----------|-----------------|  
|**adPosBOF**|-2|현재 레코드 포인터가 BOF에 있음을 나타냅니다 (즉, [bof](./bof-eof-properties-ado.md) 속성이 **True**임).|  
|**adPosEOF**|-3|현재 레코드 포인터가 EOF에 있음을 나타냅니다. 즉, [eof](./bof-eof-properties-ado.md) 속성이 **True**입니다.|  
|**adPosUnknown**|-1|는 **레코드 집합이** 비어 있거나, 현재 위치를 알 수 없거나, 공급자가 [AbsolutePage](./absolutepage-property-ado.md) 또는 [AbsolutePosition](./absoluteposition-property-ado.md) 속성을 지원 하지 않음을 나타냅니다.|  
  
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
        [AbsolutePage 속성(ADO)](./absolutepage-property-ado.md)  
    :::column-end:::
    :::column:::
        [AbsolutePosition 속성(ADO)](./absoluteposition-property-ado.md)  
    :::column-end:::
:::row-end:::