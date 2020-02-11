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
ms.openlocfilehash: dc360bc91e977228a6f9139089a7bfa87d912e1f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67918447"
---
# <a name="isolationlevel-property"></a>IsolationLevel 속성
[연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체에 대 한 격리 수준을 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 [IsolationLevelEnum](../../../ado/reference/ado-api/isolationlevelenum.md) 값을 설정 하거나 반환 합니다. 기본값은 **adXactReadCommitted**입니다.  
  
## <a name="remarks"></a>설명  
 **IsolationLevel** 속성을 사용 하 여 **연결** 개체의 격리 수준을 설정 합니다. 이 설정은 다음에 [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) 메서드를 호출할 때까지 적용 되지 않습니다. 요청 하는 격리 수준이 사용 불가능 한 경우 공급자는 **IsolationLevel** 속성을 업데이트 하지 않고 다음으로 높은 수준의 격리를 반환할 수 있습니다.  
  
 **IsolationLevel** 속성은 읽기/쓰기입니다.  
  
> [!NOTE]
>  **원격 데이터 서비스 사용** 클라이언트 쪽 **연결** 개체에서 사용 하는 경우 **IsolationLevel** 속성은 **adXactUnspecified**로만 설정할 수 있습니다. 사용자는 클라이언트 쪽 캐시에서 연결 되지 않은 **레코드 집합** 개체를 사용 하 여 작업 하므로 다중 사용자 문제가 있을 수 있습니다. 예를 들어 서로 다른 두 사용자가 같은 레코드를 업데이트 하려고 하면 원격 데이터 서비스에서 먼저 레코드를 "win"으로 업데이트 하는 사용자를 허용 합니다. 두 번째 사용자의 업데이트 요청은 오류와 함께 실패 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [IsolationLevel 및 Mode 속성 예제 (VB)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vb.md)   
 [IsolationLevel 및 Mode 속성 예제 (VC + +)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vc.md)   
