---
description: ConnectPromptEnum
title: ConnectPromptEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 171cc7706cc00b48c3373a0e40d5de221d4d00ce
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974684"
---
# <a name="connectpromptenum"></a>ConnectPromptEnum
데이터 원본에 대 한 연결을 열 때 누락 된 매개 변수를 확인 하기 위해 대화 상자를 표시할지 여부를 지정 합니다.  
  
|상수|값|설명|  
|--------------|-----------|-----------------|  
|**adPromptAlways**|1|항상를 표시 합니다.|  
|**adPromptComplete**|2|추가 정보가 필요한 경우 메시지를 표시 합니다.|  
|**adPromptCompleteRequired**|3|추가 정보가 필요한 지 여부를 묻는 메시지를 표시 하지만 선택적 매개 변수는 허용 되지 않습니다.|  
|**adPromptNever**|4|메시지를 표시 하지 않습니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.|  
|AdoEnums를 입력 합니다.|  
|AdoEnums. COMPLETEREQUIRED|  
|AdoEnums 프롬프트. NEVER|  
  
## <a name="applies-to"></a>적용 대상  
 [Prompt 속성-동적(ADO)](./prompt-property-dynamic-ado.md)