---
title: CommandStream 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Command::CommandStream
helpviewer_keywords:
- CommandStream property [ADO]
ms.assetid: f78f61b6-87e0-48dc-961e-83d0e20da58e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b1048e8d243bd19d86d60c3c4f92e4e4b9d137a9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47828790"
---
# <a name="commandstream-property-ado"></a>CommandStream 속성(ADO)
에 대 한 입력으로 사용 되는 스트림을 나타내며를 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 입력으로 사용 되는 스트림을 반환 된 **명령** 개체입니다. 이 스트림에 대 한 형식으로 공급자별으로 다릅니다. 자세한 내용은 해당 공급자의 설명서를 참조 하세요. 이 속성은 비슷합니다는 [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) 의 입력에 대 한 문자열을 지정 하는 데 사용 하는 속성을 **명령**입니다.  
  
## <a name="remarks"></a>Remarks  
 **CommandStream** 하 고 **CommandText** 함께 사용할 수 없습니다. 사용자 설정 하는 경우는 **CommandStream** 속성을 **CommandText** 속성을 빈 문자열로 설정 됩니다 (""). 사용자 설정 하는 경우는 **CommandText** 속성을 **CommandStream** 속성으로 설정 됩니다 **Nothing**.  
  
 동작을 **Command.Parameters.Refresh** 하 고 **Command.Prepare** 메서드 공급자에 의해 정의 됩니다. 스트림에서 매개 변수의 값을 새로 고칠 수 있습니다.  
  
 입력된 스트림의 소스를 반환 하는 다른 ADO 개체에 사용할 수 없는 **명령**입니다. 예를 들어 경우는 [원본](../../../ado/reference/ado-api/source-property-ado-recordset.md) 의 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 로 설정 됩니다는 **명령** 해당 입력으로 스트림이 있는 개체 **Recordset.Source** 계속 해 서 반환 합니다 **CommandText** 빈 문자열을 포함 하는 속성 ("")의 스트림 내용을 대신 합니다 **CommandStream** 속성입니다.  
  
 명령 스트림을 사용 하는 경우 (지정 된 대로 **CommandStream**)의 유일한 유효 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) 에 대 한 값을 [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) 속성은  **adCmdText** 하 고 **adCmdUnknown**합니다. 다른 값에 오류가 발생 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [명령 개체(ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [CommandText 속성 (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [Dialect 속성](../../../ado/reference/ado-api/dialect-property.md)   
 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)
