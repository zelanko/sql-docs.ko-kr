---
title: ActiveCommand 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::ActiveCommand
helpviewer_keywords:
- ActiveCommand property [ADO]
ms.assetid: fb4088d5-5968-42d6-aeaa-3955046bb4da
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d2a2f23360cf3ce032d14af7ca475d5c2c3ea638
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67921673"
---
# <a name="activecommand-property-ado"></a>ActiveCommand 속성(ADO)
연결 된 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체를 만든 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체를 나타냅니다.  
  
## <a name="return-value"></a>Return Value  
 **명령** 개체를 포함 하는 **Variant** 를 반환 합니다. 기본값은 null 개체 참조입니다.  
  
## <a name="remarks"></a>설명  
 **ActiveCommand** 속성은 읽기 전용입니다.  
  
 **명령** 개체를 사용 하 여 현재 **레코드 집합**을 만들지 않은 경우 **Null** 개체 참조가 반환 됩니다.  
  
 결과 **레코드 집합** 개체만 제공 되는 경우이 속성을 사용 하 여 연결 된 **명령** 개체를 찾을 수 있습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [ActiveCommand 속성 예제 (VB)](../../../ado/reference/ado-api/activecommand-property-example-vb.md)   
 [ActiveCommand 속성 예제 (JScript)](../../../ado/reference/ado-api/activecommand-property-example-jscript.md)   
 [ActiveCommand 속성 예제 (VC + +)](../../../ado/reference/ado-api/activecommand-property-example-vc.md)   
 [명령 개체(ADO)](../../../ado/reference/ado-api/command-object-ado.md)
