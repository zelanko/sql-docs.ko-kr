---
title: ConnectPromptEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- ConnectPromptEnum
helpviewer_keywords:
- ConnectPromptEnum enumeration [ADO]
ms.assetid: 21026e24-62b7-4cc9-8aef-62c1fc6cba75
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8ae0c2179e321e521a86fdc76e5f8978ab4ab747
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="connectpromptenum"></a>ConnectPromptEnum
데이터 원본에 대 한 연결을 열 때 누락 된 매개 변수를 요구 하는 대화 상자를 표시할지 여부를 지정 합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adPromptAlways**|1.|항상 메시지를 표시합니다.|  
|**adPromptComplete**|2|자세한 정보가 필요한 경우 메시지를 표시 합니다.|  
|**adPromptCompleteRequired**|3|자세한 정보가 필요 하지만 선택적 매개 변수를 사용할 수 없습니다 경우 메시지를 표시 합니다.|  
|**adPromptNever**|4|표시 하지 않습니다.|  
  
## <a name="adowfc-equivalent"></a>해당 하는 ADO/WFC  
 패키지에 대 한 **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.ConnectPrompt.ALWAYS|  
|AdoEnums.ConnectPrompt.COMPLETE|  
|AdoEnums.ConnectPrompt.COMPLETEREQUIRED|  
|AdoEnums.ConnectPrompt.NEVER|  
  
## <a name="applies-to"></a>적용 대상  
 [Prompt 속성-동적(ADO)](../../../ado/reference/ado-api/prompt-property-dynamic-ado.md)

