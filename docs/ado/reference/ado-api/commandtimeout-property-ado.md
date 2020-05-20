---
title: CommandTimeout 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::CommandTimeout
helpviewer_keywords:
- CommandTimeout property [ADO]
ms.assetid: c611f857-d6b0-4dca-8925-f4a02e769eb0
author: rothja
ms.author: jroth
ms.openlocfilehash: b771c5b8dc54bb312893885aea9c9c151feef3e3
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760392"
---
# <a name="commandtimeout-property-ado"></a>CommandTimeout 속성(ADO)
시도를 종료 하 고 오류를 생성 하기 전에 명령을 실행 하는 동안 대기 하는 시간을 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 명령이 실행 될 때까지 대기 하는 시간 (초)을 나타내는 **long** 값을 설정 하거나 반환 합니다. 기본값은 30입니다.  
  
## <a name="remarks"></a>설명  
 네트워크 트래픽 또는 과도 한 서버 사용의 지연으로 인해 [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) 메서드 호출을 취소할 수 있도록 하려면 [Connection](../../../ado/reference/ado-api/connection-object-ado.md) 개체 또는 [Command](../../../ado/reference/ado-api/command-object-ado.md) 개체에서 **CommandTimeout** 속성을 사용 합니다. 명령 실행이 완료 되기 전에 **CommandTimeout** 속성에 설정 된 간격이 경과 하면 오류가 발생 하 고 ADO에서 명령이 취소 됩니다. 속성을 0으로 설정 하면 ADO는 실행이 완료 될 때까지 무기한 대기 합니다. 코드를 작성 하는 공급자 및 데이터 소스가 **CommandTimeout** 기능을 지원 하는지 확인 합니다.  
  
 **연결** 개체에 대 한 **CommandTimeout** 설정은 동일한 **연결**에서 **명령** 개체의 **CommandTimeout** 설정에 영향을 주지 않습니다. 즉, **Command** 개체의 **CommandTimeout** 속성은 **Connection** 개체의 **CommandTimeout** 값을 상속 하지 않습니다.  
  
 **연결** 개체에서 **CommandTimeout** 속성은 **연결이** 열린 후 읽기/쓰기 상태로 유지 됩니다.  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[명령 개체(ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ActiveConnection, CommandText, CommandTimeout, CommandType, Size 및 Direction 속성 예제 (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, Size 및 Direction 속성 예제 (VC + +)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, Size 및 Direction 속성 예제 (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [ConnectionTimeout 속성(ADO)](../../../ado/reference/ado-api/connectiontimeout-property-ado.md)
