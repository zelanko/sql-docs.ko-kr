---
description: 명령 개체(ADO)
title: Command 개체 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command
helpviewer_keywords:
- Command object [ADO]
ms.assetid: a02c22fb-542d-465e-a629-30fd59dcbebf
author: rothja
ms.author: jroth
ms.openlocfilehash: b53f70c5f9a0da139346865b67df57a069b03e80
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88450885"
---
# <a name="command-object-ado"></a>명령 개체(ADO)
데이터 원본에 대해 실행 하려는 특정 명령을 정의 합니다.  
  
## <a name="remarks"></a>설명  
 **명령** 개체를 사용 하 여 데이터베이스를 쿼리하고 레코드 [집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체의 레코드를 반환 하거나 대량 작업을 실행 하거나 데이터베이스 구조를 조작할 수 있습니다. 공급자의 기능에 따라 일부 **명령** 컬렉션, 메서드 또는 속성을 참조 하는 경우 오류를 생성할 수 있습니다.  
  
 **Command** 개체의 컬렉션, 메서드 및 속성을 사용 하 여 다음을 수행할 수 있습니다.  
  
-   [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) 속성을 사용 하 여 명령의 실행 파일 텍스트 (예: SQL 문)를 정의 합니다. 또는 단순한 문자열이 아닌 명령 또는 쿼리 구조 (예: XML 템플릿 쿼리)의 경우 [Commandstream](../../../ado/reference/ado-api/commandstream-property-ado.md) 속성을 사용 하 여 명령을 정의 합니다.  
  
-   필요에 따라 [언어](../../../ado/reference/ado-api/dialect-property.md) 속성을 사용 하 여 **CommandText** 또는 **commandstream** 에 사용 되는 명령 언어를 지정 합니다.  
  
-   [매개 변수](../../../ado/reference/ado-api/parameter-object.md) 개체 및 [매개](../../../ado/reference/ado-api/parameters-collection-ado.md) 변수 컬렉션을 사용 하 여 매개 변수가 있는 쿼리 또는 저장 프로시저 인수를 정의 합니다.  
  
-   [Namedparameters](../../../ado/reference/ado-api/namedparameters-property-ado.md) 속성을 사용 하 여 매개 변수 이름을 공급자에 게 전달할지 여부를 나타냅니다.  
  
-   명령을 실행 하 고 [execute](../../../ado/reference/ado-api/execute-method-ado-command.md) 메서드에 적절 한 경우 **레코드 집합** 개체를 반환 합니다.  
  
-   성능을 최적화 하기 위해 실행 하기 전에 [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) 속성을 사용 하 여 명령 유형을 지정 합니다.  
  
-   [준비](../../../ado/reference/ado-api/prepared-property-ado.md) 된 속성을 사용 하 여 실행 하기 전에 공급자가 명령의 준비 된 버전 (또는 컴파일)을 저장할지 여부를 제어 합니다.  
  
-   [CommandTimeout](../../../ado/reference/ado-api/commandtimeout-property-ado.md) 속성을 사용 하 여 명령이 실행 될 때까지 공급자가 대기할 시간 (초)을 설정 합니다.  
  
-   [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) 속성을 설정 하 여 열린 연결을 **명령** 개체와 연결 합니다.  
  
-   [이름](../../../ado/reference/ado-api/name-property-ado.md) 속성을 설정 하 여 연결 된 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체에 대 한 메서드로 **명령** 개체를 식별 합니다.  
  
-   **명령** 개체를 **레코드 집합** 의 [원본](../../../ado/reference/ado-api/source-property-ado-recordset.md) 속성에 전달 하 여 데이터를 가져옵니다.  
  
-   [Properties](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션을 사용 하 여 공급자별 특성에 액세스 합니다.  
  
> [!NOTE]
>  **Command** 개체를 사용 하지 않고 쿼리를 실행 하려면 쿼리 문자열을 **Connection** 개체의 [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) 메서드에 전달 하거나 **레코드 집합** 개체의 [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) 메서드로 전달 합니다. 그러나 명령 텍스트를 유지 하 고 다시 실행 하거나 쿼리 매개 변수를 사용 하려는 경우에는 **command** 개체가 필요 합니다.  
  
 이전에 정의한 **연결** 개체와는 독립적으로 **Command** 개체를 만들려면 해당 **ActiveConnection** 속성을 유효한 연결 문자열로 설정 합니다. ADO는 여전히 **연결** 개체를 만들지만 개체 변수에는 해당 개체를 할당 하지 않습니다. 그러나 동일한 연결을 사용 하 여 여러 **명령** 개체를 연결 하는 경우에는 명시적으로 **연결** 개체를 만들고 열어야 합니다. 그러면 **연결** 개체가 개체 변수에 할당 됩니다. 닫힌 **연결** 개체를 할당 하면 오류가 발생 하므로 **Command** 개체의 **ActiveConnection** 속성에 연결 개체를 할당 하기 전에 **연결** 개체가 성공적으로 열리는지 확인 합니다. **Command** 개체의 **ActiveConnection** 속성을이 개체 변수로 설정 하지 않으면 동일한 연결 문자열을 사용 하는 경우에도 ADO에서 각 **명령** 개체에 대 한 새 **연결** 개체를 만듭니다.  
  
 **명령을**실행 하려면 연결 된 **연결** 개체에 대 한 [이름](../../../ado/reference/ado-api/name-property-ado.md) 속성으로 호출 합니다. **명령의** **ActiveConnection** 속성을 **Connection** 개체로 설정 해야 합니다. **명령** 에 매개 변수가 있는 경우 해당 값을 메서드에 인수로 전달 합니다.  
  
 두 개 이상의 **명령** 개체가 동일한 연결에서 실행 되 고 **명령** 개체 중 하나가 output 매개 변수가 있는 저장 프로시저 이면 오류가 발생 합니다. 각 **명령** 개체를 실행 하려면 별도의 연결을 사용 하거나 연결에서 다른 모든 **명령** 개체의 연결을 끊습니다.  
  
 **Parameters** 컬렉션은 **Command** 개체의 기본 멤버입니다. 따라서 다음 두 코드 문은 동일 합니다.  
  
```  
objCmd.Parameters.Item(0)  
objCmd(0)  
```  
  
-   **명령** 개체는 스크립팅에 안전 하지 않습니다.  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [Command 개체 속성, 메서드 및 이벤트](../../../ado/reference/ado-api/command-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>참고 항목  
 [Connection 개체 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Parameters 컬렉션 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Properties 컬렉션 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [부록 A: 공급자](../../../ado/guide/appendixes/appendix-a-providers.md)
