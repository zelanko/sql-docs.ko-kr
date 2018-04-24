---
title: CommandStream 속성 (ADO) | Microsoft Docs
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
- _Command::CommandStream
helpviewer_keywords:
- CommandStream property [ADO]
ms.assetid: f78f61b6-87e0-48dc-961e-83d0e20da58e
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f720cc4ab3b388f974d34e23690b8aef91c20ba3
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="commandstream-property-ado"></a>CommandStream 속성 (ADO)
에 대 한 입력으로 사용 되는 스트림과 나타냅니다는 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환에 대 한 입력으로 사용 되는 스트림과 **명령** 개체입니다. 이 스트림에 대 한 형식은 공급자별; 자세한 내용은 해당 공급자의 설명서를 참조 하십시오. 이 속성은 비슷합니다는 [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) 속성의 입력에 대 한 문자열을 지정 하는 데 사용 된 **명령**합니다.  
  
## <a name="remarks"></a>주의  
 **CommandStream** 및 **CommandText** 함께 사용할 수 없습니다. 사용자 설정 하는 경우는 **CommandStream** 속성에는 **CommandText** 속성이 빈 문자열로 설정 됩니다 (""). 사용자가을 설정 하는 경우는 **CommandText** 속성에는 **CommandStream** 속성으로 설정 됩니다 **Nothing**합니다.  
  
 동작에서 **Command.Parameters.Refresh** 및 **Command.Prepare** 공급자에 의해 정의 된 메서드가 있습니다. 스트림에서 매개 변수의 값을 새로 고칠 수 있습니다.  
  
 입력된 스트림의의 원본을 반환 하는 다른 ADO 개체를 사용할 수 없으면는 **명령**합니다. 예를 들어 경우는 [소스](../../../ado/reference/ado-api/source-property-ado-recordset.md) 의 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 로 설정 되는 **명령** 해당 입력으로 스트림을 가진 개체를 **Recordset.Source** 계속 해 서 반환는 **CommandText** 속성 값에 빈 문자열 ("")의 스트림 내용을 대신는 **CommandStream** 속성 합니다.  
  
 명령 스트림을 사용 하는 경우 (에 지정 된 대로 **CommandStream**)의 유일한 유효 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) 에 대 한 값은 [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) 속성  **adCmdText** 및 **adCmdUnknown**합니다. 다른 모든 값에 오류가 발생합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [명령 개체(ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [CommandText 속성 (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [언어 속성](../../../ado/reference/ado-api/dialect-property.md)   
 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)
