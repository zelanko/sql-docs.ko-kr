---
title: ConnectPromptEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ConnectPromptEnum
helpviewer_keywords:
- ConnectPromptEnum enumeration [ADO]
ms.assetid: 21026e24-62b7-4cc9-8aef-62c1fc6cba75
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 40ce74748e15a2715de26e813007e00be0c33729
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66698594"
---
# <a name="connectpromptenum"></a>ConnectPromptEnum
데이터 원본에 연결을 열 때 누락 된 매개 변수를 묻는 대화 상자를 표시할지 여부를 지정 합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adPromptAlways**|1|항상 표시합니다.|  
|**adPromptComplete**|2|자세한 정보가 필요한 경우 메시지 표시 합니다.|  
|**adPromptCompleteRequired**|3|자세한 내용은 필요 하지만 선택적 매개 변수는 허용 되지 않습니다 하는 경우 메시지를 표시 합니다.|  
|**adPromptNever**|4|표시 하지 않습니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 해당  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.ConnectPrompt.ALWAYS|  
|AdoEnums.ConnectPrompt.COMPLETE|  
|AdoEnums.ConnectPrompt.COMPLETEREQUIRED|  
|AdoEnums.ConnectPrompt.NEVER|  
  
## <a name="applies-to"></a>적용 대상  
 [Prompt 속성-동적(ADO)](../../../ado/reference/ado-api/prompt-property-dynamic-ado.md)
