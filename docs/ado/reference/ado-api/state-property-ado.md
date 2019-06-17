---
title: State 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command25::State
helpviewer_keywords:
- State property [ADO]
ms.assetid: 0b993bac-2653-40b1-bcbb-5b57b6aae2bf
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e8a46dd9358b085fb6079f03df88474b72440068
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66711253"
---
# <a name="state-property-ado"></a>State 속성(ADO)
적용 가능한 모든 개체에 대 한 개체의 상태 열렸는지 닫혔는지 여부를 나타냅니다. 개체는 비동기 메서드를 실행 하는 경우 개체의 현재 상태에 연결, 실행 또는 검색을 나타냅니다.  
  
## <a name="return-value"></a>반환 값  
 반환을 **긴** 될 수 있는 값을 [ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md) 값입니다. 기본값은 **adStateClosed**합니다.  
  
## <a name="remarks"></a>Remarks  
 사용할 수는 **상태** 속성을 언제 든 지 지정된 된 개체의 현재 상태를 확인 합니다.  
  
 개체의 **상태** 속성 값 조합을 가질 수 있습니다. 예를 들어, 문을 실행 하는 경우이 속성 값이 있는을 결합 **adStateOpen** 하 고 **adStateExecuting**합니다.  
  
 합니다 **상태** 속성은 읽기 전용입니다.  
  
## <a name="applies-to"></a>적용 대상  
  
||||  
|-|-|-|  
|[명령 개체(ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[레코드 개체(ADO)](../../../ado/reference/ado-api/record-object-ado.md)|  
|[레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)||  
  
## <a name="see-also"></a>관련 항목  
 [ConnectionString, ConnectionTimeout, 및 State 속성 예제 (VB)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [ConnectionString, ConnectionTimeout, 및 State 속성 예제 (VC + +)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
