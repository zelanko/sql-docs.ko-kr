---
title: "CommandType 속성 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
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
- Command15::CommandType
helpviewer_keywords:
- CommandType property [ADO]
ms.assetid: ca44809c-8647-48b6-a7fb-0be70a02f53e
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d670a188c89ed96001c93d17a33dc0c03d601a82
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="commandtype-property-ado"></a>CommandType 속성 (ADO)
유형을 나타냅니다는 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 하나 이상의 반환 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) 값입니다.  
  
> [!NOTE]
>  사용 하지 않는 **CommandTypeEnum** 값 **adCmdFile** 또는 **adCmdTableDirect** 와 **CommandType**합니다. 사용한 옵션으로 이러한 값만 사용할 수는 [열려](../../../ado/reference/ado-api/open-method-ado-recordset.md) 및 [Requery](../../../ado/reference/ado-api/requery-method.md) 의 메서드는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)합니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **CommandType** 속성의 평가 최적화 하는 [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) 속성입니다.  
  
 경우는 **CommandType** 속성 값이 기본 값으로 설정 **adCmdUnknown**, ADO 여부를 확인 하는 공급자에 대 한 호출을 확인 해야 하기 때문에 성능이 저하 될 수 있습니다는  **CommandText** 속성은 SQL 문, 저장된 프로시저 또는 테이블 이름입니다. 명령 유형을 사용 하는 알고 있는 경우 설정의 **CommandType** 속성 관련 코드로 바로 이동할 수는 ADO에 지시 합니다. 경우는 **CommandType** 속성에서 명령의 형식과 일치 하지 않습니다는 **CommandText** 속성을 호출 하는 경우 오류가 발생 된 [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) 메서드.  
  
## <a name="applies-to"></a>적용 대상  
 [명령 개체(ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [ActiveConnection, CommandText, CommandTimeout, CommandType, 크기 및 방향 속성 예제 (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, 크기 및 방향 속성 예제 (VC + +)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, 크기 및 방향 속성 예제 (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)

