---
title: "명령 개체 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Command
helpviewer_keywords:
- Command object [ADO]
ms.assetid: a02c22fb-542d-465e-a629-30fd59dcbebf
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 863c922dce68f5e3108136baf90ebc5a3d0b697a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="command-object-ado"></a>Command 개체 (ADO)
데이터 원본에 대해 실행 하려는 특정 명령을 정의 합니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **명령** 의 레코드를 반환 하 고 데이터베이스를 쿼리 하는 개체는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체를 대량 작업을 실행 하거나 데이터베이스의 구조를 조작 합니다. 일부 공급자의 기능에 따라 **명령** 컬렉션, 메서드 또는 속성 참조 될 때 오류를 생성할 수 있습니다.  
  
 컬렉션, 메서드 및 속성의는 **명령** 개체를 다음을 수행할 수 있습니다.  
  
-   사용 하 여 명령 (예를 들어 SQL 문)의 실행 텍스트 정의 [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) 속성입니다. 또는 간단한 이외의 다른 명령 또는 쿼리 구조에 대 한 문자열 (예를 들어, XML 서식 파일 쿼리) 정의 사용 하 여 명령을 [CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md) 속성입니다.  
  
-   필요에 따라 사용 되는 명령 언어를 나타내는 **CommandText** 또는 **CommandStream** 와 [언어](../../../ado/reference/ado-api/dialect-property.md) 속성입니다.  
  
-   매개 변수가 있는 쿼리 또는 저장 프로시저 인수를 정의 [매개 변수](../../../ado/reference/ado-api/parameter-object.md) 개체 및 [매개 변수](../../../ado/reference/ado-api/parameters-collection-ado.md) 컬렉션입니다.  
  
-   매개 변수 이름을 사용 하 여 공급자에 전달 되어야 하는지 여부를 나타내기는 [NamedParameters](../../../ado/reference/ado-api/namedparameters-property-ado.md) 속성입니다.  
  
-   명령을 실행 하 고 반환 된 **레코드 집합** 개체와 해당 하는 경우는 [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) 메서드.  
  
-   사용 하 여 명령의 유형을 지정는 [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) 성능을 최적화 하기 위해 실행 전에 속성입니다.  
  
-   공급자는 준비 된 (또는 컴파일된) 명령의 버전을 사용 하 여 실행 하기 전에 저장 하는지 여부를 제어는 [Prepared](../../../ado/reference/ado-api/prepared-property-ado.md) 속성입니다.  
  
-   공급자에서으로 실행 되도록 명령에 대 한 대기 하는 시간 (초)의 수를 설정의 [CommandTimeout](../../../ado/reference/ado-api/commandtimeout-property-ado.md) 속성입니다.  
  
-   연결 된 열려 있는 연결을 **명령** 개체를 설정 하 여 해당 [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) 속성입니다.  
  
-   설정의 [이름](../../../ado/reference/ado-api/name-property-ado.md) 속성을 식별 하는 **명령** 개체에 연결 된 메서드로 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체입니다.  
  
-   전달는 **명령** 개체를 [소스](../../../ado/reference/ado-api/source-property-ado-recordset.md) 속성은 **레코드 집합** 데이터를 가져올 수 있습니다.  
  
-   공급자별 특성을 액세스는 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션입니다.  
  
> [!NOTE]
>  사용 하지 않고 쿼리를 실행 하는 **명령** 개체에 쿼리 문자열을 전달 하는 [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) 의 메서드는 **연결** 개체 또는 [열고](../../../ado/reference/ado-api/open-method-ado-recordset.md)의 메서드는 **레코드 집합** 개체입니다. 그러나 한 **명령** 명령 텍스트를 유지 하 고 했다가 나중에 다시 실행 하거나 쿼리 매개 변수를 사용 하려는 경우 개체가 필요 합니다.  
  
 만들려는 **명령** 독립적으로 이전에 정의 된 개체 **연결** 개체, 설정 해당 **ActiveConnection** 속성을 유효한 연결 문자열입니다. ADO 만듭니다는 **연결** 개체를 할당 하지 않습니다 해당 개체는 개체 변수입니다. 그러나 여러를 연결 하는 경우 **명령** 동일한 연결을 통해 개체를 명시적으로 만들고이 열을 **연결** 개체;이 할당은 **연결** 개체 변수에 개체입니다. 다음 사항을 확인는 **연결** 에 할당 하기 전에 개체가 성공적으로 열렸을 **ActiveConnection** 속성의는 **명령** 개체를 할당 하기 때문에 닫힌 **연결** 개체 하면 오류가 발생 합니다. 설정 하지 않은 경우는 **ActiveConnection** 의 속성은 **명령** ADO를 새로 만듭니다.이 개체 변수에 개체 **연결** 각각에 대 한 개체 ** 명령** 개체를 동일한 연결 문자열을 사용 하는 경우에 합니다.  
  
 실행 하는 **명령**, 하 여 호출 해당 [이름](../../../ado/reference/ado-api/name-property-ado.md) 속성은 관련 **연결** 개체입니다. **명령** 있어야 해당 **ActiveConnection** 속성이로 설정 된 **연결** 개체입니다. 경우는 **명령** 에 매개 변수가 해당 값을 메서드에 인수로 전달 합니다.  
  
 둘 이상의 **명령** 개체가 한 동일한 연결에서 실행 되 **명령** 개체는 출력 매개 변수가 있는 저장된 프로시저는 오류가 발생 합니다. 각 실행 **명령** 개체를 별도 연결을 사용 하거나 다른 모든 연결을 끊을 **명령** 연결에서 개체입니다.  
  
 **매개 변수** 컬렉션은의 기본 멤버는 **명령** 개체입니다. 결과적으로, 다음 두 코드 문은 동일합니다.  
  
```  
objCmd.Parameters.Item(0)  
objCmd(0)  
```  
  
-   **명령** 개체가 스크립팅 작업에 안전 합니다.  
  
 이 섹션에는 다음 항목 포함 되어 있습니다.  
  
-   [명령 개체 속성, 메서드 및 이벤트](../../../ado/reference/ado-api/command-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목:  
 [연결 개체 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Parameters 컬렉션 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Properties 컬렉션 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [부록 A: 공급자](../../../ado/guide/appendixes/appendix-a-providers.md)
