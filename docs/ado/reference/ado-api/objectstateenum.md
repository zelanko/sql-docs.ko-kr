---
title: ObjectStateEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: ObjectStateEnum
helpviewer_keywords: ObjectStateEnum enumeration [ADO]
ms.assetid: 32746558-097b-4749-989e-519aadf7e3f4
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: aa1236357042126f60b27f4c6f943ae3c2198bb0
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="objectstateenum"></a>ObjectStateEnum
개체 개방 명령을 실행 하거나 데이터를 검색 하는 데이터 원본에 연결 하는지를 지정 합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adStateClosed**|0|개체가 닫혀 나타냅니다.|  
|**adStateOpen**|1.|해당 개체가 열려 임을 나타냅니다.|  
|**adStateConnecting**|2|개체가 연결을 나타냅니다.|  
|**adStateExecuting**|4|개체의 명령을 실행 하 고 나타냅니다.|  
|**adStateFetching**|8|개체의 행이 검색 되 고 있는지를 나타냅니다.|  
  
## <a name="adowfc-equivalent"></a>해당 하는 ADO/WFC  
 패키지에 대 한 **com.ms.wfc.data**  
  
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
