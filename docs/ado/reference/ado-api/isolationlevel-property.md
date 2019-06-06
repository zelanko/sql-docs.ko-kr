---
title: IsolationLevel 속성 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::IsolationLevel
helpviewer_keywords:
- IsolationLevel property
ms.assetid: ea84e4b2-fbf2-4eef-b9ce-796b22e21800
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9e027e325ec27bf5a80cf4df85afcfe59656ce3c
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66697588"
---
# <a name="isolationlevel-property"></a>IsolationLevel 속성
에 대 한 격리 수준을 나타냅니다는 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환 된 [IsolationLevelEnum](../../../ado/reference/ado-api/isolationlevelenum.md) 값입니다. 기본값은 **adXactReadCommitted**합니다.  
  
## <a name="remarks"></a>Remarks  
 사용 된 **IsolationLevel** 격리 수준을 설정 하려면 속성을 **연결** 개체. 설정이 적용 되지 않습니다 다음에 호출 될 때까지 합니다 [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) 메서드. 요청 하는 격리 수준을 사용할 수 없는 경우 공급자를 업데이트 하지 않고 다음 더 높은 수준의 격리를 반환할 수 있습니다 합니다 **IsolationLevel** 속성입니다.  
  
 합니다 **IsolationLevel** 속성은 읽기/쓰기가 가능 합니다.  
  
> [!NOTE]
>  **원격 데이터 서비스 사용** 클라이언트 쪽에서 사용 되 면 **연결** 개체를 **IsolationLevel** 속성에만 설정할 수 있습니다 **adXactUnspecified**합니다. 사용자는 연결이 끊긴 작업 때문에 **레코드 집합** 개체는 클라이언트 쪽 캐시에서 다중 사용자 문제가 있을 수 있습니다. 예를 들어, 두 사용자를 동일한 레코드를 업데이트 하려고 하는 경우 원격 데이터 서비스 하기만 하면 사용자가 레코드를 먼저 업데이트 "win"를 오류가 발생 하 여 두 번째 사용자의 업데이트 요청이 실패 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [IsolationLevel 및 모드 속성 예제 (VB)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vb.md)   
 [IsolationLevel 및 모드 속성 예제 (VC + +)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vc.md)   
