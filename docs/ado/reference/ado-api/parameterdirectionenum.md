---
title: ParameterDirectionEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ParameterDirectionEnum
helpviewer_keywords:
- ParameterDirectionEnum enumeration [ADO]
ms.assetid: c66aa6e6-d4f0-4f0f-9640-e08ae6cfdef3
author: rothja
ms.author: jroth
ms.openlocfilehash: 88754f7dbd0064c765314d88b0fcc0d06f05bbb2
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763404"
---
# <a name="parameterdirectionenum"></a>ParameterDirectionEnum
[매개 변수가](../../../ado/reference/ado-api/parameter-object.md) 입력 매개 변수, 출력 매개 변수, 입력 및 출력 매개 변수 또는 저장 프로시저의 반환 값을 나타내는지 여부를 지정 합니다.  
  
|상수|값|설명|  
|--------------|-----------|-----------------|  
|**adParamInput**|1|기본값 매개 변수가 입력 매개 변수를 나타내는지 여부를 나타냅니다.|  
|**adParamInputOutput**|3|매개 변수가 입력 매개 변수 및 출력 매개 변수를 모두 나타내도록 지정 합니다.|  
|**adParamOutput**|2|매개 변수가 출력 매개 변수를 나타내는지 여부를 나타냅니다.|  
|**adParamReturnValue**|4|매개 변수가 반환 값 임을 나타냅니다.|  
|**adParamUnknown**|0|매개 변수 방향을 알 수 없음을 나타냅니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums. ParameterDirection|  
|AdoEnums. ParameterDirection 출력|  
|AdoEnums. ParameterDirection|  
|AdoEnums. ParameterDirection. RETURNVALUE|  
|AdoEnums. ParameterDirection|  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[CreateParameter 메서드(ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)|[Direction 속성](../../../ado/reference/ado-api/direction-property.md)|
