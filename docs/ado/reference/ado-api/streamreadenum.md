---
title: StreamReadEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StreamReadEnum
helpviewer_keywords:
- StreamReadEnum enumeration [ADO]
ms.assetid: cfa1b416-003a-436f-a21b-bd2397e54db3
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 37d2ba0834d2a4469d97a36f39677f407a5e61be
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66710680"
---
# <a name="streamreadenum"></a>StreamReadEnum
전체 스트림을 또는 다음 줄에서 읽을 수 있는지 여부를 지정 된 [Stream](../../../ado/reference/ado-api/stream-object-ado.md) 개체입니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adReadAll**|-1|기본. 이상에 현재 위치에서 스트림에서 모든 바이트를 읽습니다 합니다 [EOS](../../../ado/reference/ado-api/eos-property.md) 표식입니다. 이 값만 유효 **StreamReadEnum** 이진 스트림 값 ([형식](../../../ado/reference/ado-api/type-property-ado-stream.md) 됩니다 **adTypeBinary**).|  
|**adReadLine**|-2|스트림에서 다음 줄을 읽습니다 (으로 지정 합니다 [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) 속성).|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 해당  
 이러한 상수는 ADO/wfc 필요가 없습니다.  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[Read 메서드](../../../ado/reference/ado-api/read-method.md)|[ReadText 메서드](../../../ado/reference/ado-api/readtext-method.md)|
