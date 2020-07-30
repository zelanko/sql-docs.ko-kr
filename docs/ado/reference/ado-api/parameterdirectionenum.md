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
ms.openlocfilehash: c109ea1c44fc44a4cdbb585e2c612ebf8c9b2909
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242609"
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

:::row:::
    :::column:::
        [CreateParameter 메서드(ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)  
    :::column-end:::
    :::column:::
        [Direction 속성](../../../ado/reference/ado-api/direction-property.md)  
    :::column-end:::
:::row-end:::
