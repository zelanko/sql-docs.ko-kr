---
title: ObjectStateEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
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
- ObjectStateEnum
helpviewer_keywords:
- ObjectStateEnum enumeration [ADO]
ms.assetid: 32746558-097b-4749-989e-519aadf7e3f4
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cf7bdb66b8c8de0e45417e85005d7eda90fdc014
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="objectstateenum"></a>ObjectStateEnum
개체 개방 명령을 실행 하거나 데이터를 검색 하는 데이터 원본에 연결 하는지를 지정 합니다.  
  
|상수|Value|Description|  
|--------------|-----------|-----------------|  
|**adStateClosed**|0|개체가 닫혀 나타냅니다.|  
|**adStateOpen**|1.|해당 개체가 열려 임을 나타냅니다.|  
|**adStateConnecting**|2|개체가 연결을 나타냅니다.|  
|**adStateExecuting**|4|개체의 명령을 실행 하 고 나타냅니다.|  
|**adStateFetching**|8|개체의 행이 검색 되 고 있는지를 나타냅니다.|  
  
## <a name="adowfc-equivalent"></a>해당 하는 ADO/WFC  
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
