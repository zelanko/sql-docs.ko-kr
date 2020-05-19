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
author: rothja
ms.author: jroth
ms.openlocfilehash: b89876366c80d20bde110da9e9d86414873e86bc
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82747474"
---
# <a name="activecommand-property-ado"></a>ActiveCommand 속성(ADO)
연결 된 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체를 만든 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체를 나타냅니다.  
  
## <a name="return-value"></a>반환 값  
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
