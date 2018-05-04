---
title: ConnectPromptEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ConnectPromptEnum
helpviewer_keywords:
- ConnectPromptEnum enumeration [ADO]
ms.assetid: 21026e24-62b7-4cc9-8aef-62c1fc6cba75
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b8f01de20cabf1ec5d7cefdb645fb1fc08b69d31
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="connectpromptenum"></a>ConnectPromptEnum
데이터 원본에 대 한 연결을 열 때 누락 된 매개 변수를 요구 하는 대화 상자를 표시할지 여부를 지정 합니다.  
  
|상수|Value|Description|  
|--------------|-----------|-----------------|  
|**adPromptAlways**|1.|항상 메시지를 표시합니다.|  
|**adPromptComplete**|2|자세한 정보가 필요한 경우 메시지를 표시 합니다.|  
|**adPromptCompleteRequired**|3|자세한 정보가 필요 하지만 선택적 매개 변수를 사용할 수 없습니다 경우 메시지를 표시 합니다.|  
|**adPromptNever**|4|표시 하지 않습니다.|  
  
## <a name="adowfc-equivalent"></a>해당 하는 ADO/WFC  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.ConnectPrompt.ALWAYS|  
|AdoEnums.ConnectPrompt.COMPLETE|  
|AdoEnums.ConnectPrompt.COMPLETEREQUIRED|  
|AdoEnums.ConnectPrompt.NEVER|  
  
## <a name="applies-to"></a>적용 대상  
 [Prompt 속성-동적(ADO)](../../../ado/reference/ado-api/prompt-property-dynamic-ado.md)
