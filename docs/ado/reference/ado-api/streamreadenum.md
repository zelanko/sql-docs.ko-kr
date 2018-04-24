---
title: StreamReadEnum | Microsoft Docs
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
- StreamReadEnum
helpviewer_keywords:
- StreamReadEnum enumeration [ADO]
ms.assetid: cfa1b416-003a-436f-a21b-bd2397e54db3
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 32b606d6f960dc77f8d90257b8c18d19703620d9
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="streamreadenum"></a>StreamReadEnum
전체 스트림을 또는 다음 줄에서 읽을 수 있는지 여부를 지정 된 [스트림](../../../ado/reference/ado-api/stream-object-ado.md) 개체입니다.  
  
|상수|Value|Description|  
|--------------|-----------|-----------------|  
|**adReadAll**|-1|기본. 부터 현재 위치에서 스트림에서 모든 바이트를 읽고는 [EOS](../../../ado/reference/ado-api/eos-property.md) 표식입니다. 이 값만 유효 **StreamReadEnum** 이진 스트림 값 ([형식](../../../ado/reference/ado-api/type-property-ado-stream.md) 은 **adTypeBinary**).|  
|**adReadLine**|-2|스트림에서 다음 줄을 읽습니다 (지정 된는 [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) 속성).|  
  
## <a name="adowfc-equivalent"></a>해당 하는 ADO/WFC  
 이러한 상수는 ADO/wfc 필요가 없습니다.  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[Read 메서드](../../../ado/reference/ado-api/read-method.md)|[ReadText 메서드](../../../ado/reference/ado-api/readtext-method.md)|
