---
title: ActiveCommand 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::ActiveCommand
helpviewer_keywords:
- ActiveCommand property [ADO]
ms.assetid: fb4088d5-5968-42d6-aeaa-3955046bb4da
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b221cc04d9a9e7d4d6c163867d6b77be71292e5e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="activecommand-property-ado"></a>ActiveCommand 속성 (ADO)
나타냅니다는 [명령](../../../ado/reference/ado-api/command-object-ado.md) 만든 연결 된 개체를 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다.  
  
## <a name="return-value"></a>반환 값  
 반환 된 **Variant** 를 포함 하는 **명령** 개체입니다. 기본값은 null 개체 참조입니다.  
  
## <a name="remarks"></a>주의  
 **ActiveCommand** 속성은 읽기 전용입니다.  
  
 경우는 **명령** 개체 현재를 만드는 데 사용 되지 **레코드 집합**는 **Null** 개체 참조가 반환 됩니다.  
  
 이 속성을 사용 하 여 연결 된 찾으려고 **명령** 결과 제공 되 면 개체 **레코드 집합** 개체입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [ActiveCommand 속성 예제 (VB)](../../../ado/reference/ado-api/activecommand-property-example-vb.md)   
 [ActiveCommand 속성 예제 (JScript)](../../../ado/reference/ado-api/activecommand-property-example-jscript.md)   
 [ActiveCommand 속성 예제 (VC + +)](../../../ado/reference/ado-api/activecommand-property-example-vc.md)   
 [명령 개체(ADO)](../../../ado/reference/ado-api/command-object-ado.md)
