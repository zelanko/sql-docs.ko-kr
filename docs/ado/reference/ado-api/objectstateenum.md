---
title: ObjectStateEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ObjectStateEnum
helpviewer_keywords:
- ObjectStateEnum enumeration [ADO]
ms.assetid: 32746558-097b-4749-989e-519aadf7e3f4
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 41b72647af357bc73eb3e9a2f8c3063f2275f6a6
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66707183"
---
# <a name="objectstateenum"></a>ObjectStateEnum
개체는 명령을 실행 하거나 데이터를 검색 하는 데이터 원본에 연결 하는 개방 인지 여부를 지정 합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adStateClosed**|0|개체가 닫혀 있는지를 나타냅니다.|  
|**adStateOpen**|1|개체가 열려 있는지를 나타냅니다.|  
|**adStateConnecting**|2|개체는 연결 되어 있음을 나타냅니다.|  
|**adStateExecuting**|4|개체의 명령을 실행 하 고 나타냅니다.|  
|**adStateFetching**|8|개체의 행을 검색 되는 것을 나타냅니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 해당  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.ObjectState.CLOSED|  
|AdoEnums.ObjectState.OPEN|  
|AdoEnums.ObjectState.CONNECTING|  
|AdoEnums.ObjectState.EXECUTING|  
|AdoEnums.ObjectState.FETCHING|  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[State 속성(ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)|[State 속성(ADO)](../../../ado/reference/ado-api/state-property-ado.md)|
