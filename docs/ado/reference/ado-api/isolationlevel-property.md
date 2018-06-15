---
title: IsolationLevel 속성 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::IsolationLevel
helpviewer_keywords:
- IsolationLevel property
ms.assetid: ea84e4b2-fbf2-4eef-b9ce-796b22e21800
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4e6de8da487352fe0a26d3524317ced061370771
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35279212"
---
# <a name="isolationlevel-property"></a>IsolationLevel 속성
에 대 한 격리 수준을 나타냅니다는 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환는 [IsolationLevelEnum](../../../ado/reference/ado-api/isolationlevelenum.md) 값입니다. 기본값은 **adXactReadCommitted**합니다.  
  
## <a name="remarks"></a>Remarks  
 사용 하 여는 **IsolationLevel** 수준의 격리를 설정 하려면 속성은 **연결** 개체입니다. 설정이 적용 되지 않습니다는 다음에 호출할 때까지는 [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) 메서드. 요청한 격리 수준을 사용할 수 없는 경우 공급자를 업데이트 하지 않고 다음으로 높은 격리 수준을 반환할 수 있습니다는 **IsolationLevel** 속성입니다.  
  
 **IsolationLevel** 속성은 읽기/쓰기가 가능 합니다.  
  
> [!NOTE]
>  **원격 데이터 서비스 사용** 클라이언트 쪽에서 사용할 때 **연결** 개체는 **IsolationLevel** 속성에만 설정할 수 있습니다 **adXactUnspecified**합니다. 사용자가 사용 하는 연결이 끊어진 때문에 **레코드 집합** 개체는 클라이언트 쪽 캐시에서 다중 사용자 문제가 있을 수 있습니다. 예를 들어, 두 사용자가 동일한 레코드를 업데이트 하려고 시도할 때 원격 데이터 서비스 하기만 하면 사용자가 레코드를 먼저 업데이트 "win"를 오류가 발생 하 여 두 번째 사용자의 업데이트 요청이 실패 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [IsolationLevel 및 모드 속성 예제 (VB)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vb.md)   
 [IsolationLevel 및 모드 속성 예제 (VC + +)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vc.md)   
