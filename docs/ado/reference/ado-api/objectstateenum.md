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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67931924"
---
# <a name="objectstateenum"></a>ObjectStateEnum
개체가 열려 있는지 또는 닫혀 있는지, 데이터 원본에 연결 하 고, 명령을 실행 하거나, 데이터를 검색할지를 지정 합니다.  
  
|지속적임|값|Description|  
|--------------|-----------|-----------------|  
|**adStateClosed**|0|개체가 닫혀 있음을 나타냅니다.|  
|**Adstateopen then**|1|개체가 열려 있음을 나타냅니다.|  
|**adStateConnecting**|2|개체가 연결 중임을 나타냅니다.|  
|**adStateExecuting**|4|개체가 명령을 실행 중임을 나타냅니다.|  
|**adStateFetching**|8|개체의 행이 검색 되 고 있음을 나타냅니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 Package: **com.ms.wfc.data**  
  
|지속적임|  
|--------------|  
|AdoEnums. ObjectState|  
|AdoEnums|  
|AdoEnums 상태입니다. 연결 중|  
|AdoEnums 상태입니다. 실행 중|  
|AdoEnums|  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[State 속성(ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)|[State 속성(ADO)](../../../ado/reference/ado-api/state-property-ado.md)|
