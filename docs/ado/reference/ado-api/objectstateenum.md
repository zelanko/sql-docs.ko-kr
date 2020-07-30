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
author: rothja
ms.author: jroth
ms.openlocfilehash: e0b69deb64cc4ea04c007fd3d3328cb4154cc3e8
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242620"
---
# <a name="objectstateenum"></a>ObjectStateEnum
개체가 열려 있는지 또는 닫혀 있는지, 데이터 원본에 연결 하 고, 명령을 실행 하거나, 데이터를 검색할지를 지정 합니다.  
  
|상수|값|설명|  
|--------------|-----------|-----------------|  
|**adStateClosed**|0|개체가 닫혀 있음을 나타냅니다.|  
|**Adstateopen then**|1|개체가 열려 있음을 나타냅니다.|  
|**adStateConnecting**|2|개체가 연결 중임을 나타냅니다.|  
|**adStateExecuting**|4|개체가 명령을 실행 중임을 나타냅니다.|  
|**adStateFetching**|8|개체의 행이 검색 되 고 있음을 나타냅니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums. ObjectState|  
|AdoEnums|  
|AdoEnums 상태입니다. 연결 중|  
|AdoEnums.ObjectState.EXE가공선|  
|AdoEnums|  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|||

:::row:::
    :::column:::
        [State 속성(ADO)](../../../ado/reference/ado-api/state-property-ado.md)  
    :::column-end:::
    :::column:::
        [State 속성(ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)  
    :::column-end:::
:::row-end:::
