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
ms.openlocfilehash: 708d146aaa40d873e0a519c860a047d4b1f93161
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931924"
---
# <a name="objectstateenum"></a>ObjectStateEnum
개체는 명령을 실행 하거나 데이터를 검색 하는 데이터 원본에 연결 하는 개방 인지 여부를 지정 합니다.  
  
|상수|값|설명|  
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
