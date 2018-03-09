---
title: "Parameters 컬렉션 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
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
- Command15::get_Parameters
- Command15::Parameters
- Command15::GetParameters
helpviewer_keywords:
- Parameters collection [ADO]
ms.assetid: 497cae10-3913-422a-9753-dcbb0a639b1b
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 96d30086b4c05455ef7d4fd5fdd82674979c205d
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="parameters-collection-ado"></a>Parameters 컬렉션 (ADO)
모든 포함 된 [매개 변수](../../../ado/reference/ado-api/parameter-object.md) 의 개체는 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체입니다.  
  
## <a name="remarks"></a>주의  
 A **명령** 개체에는 **매개 변수** 컬렉션으로 이루어져 **매개 변수** 개체입니다.  
  
 사용 하는 [새로 고침](../../../ado/reference/ado-api/refresh-method-ado.md) 에서 메서드는 **명령** 개체의 **매개 변수** 공급자 매개 변수 정보는 저장된 프로시저 또는 매개 변수가 있는 쿼리를 검색 하는 컬렉션 에 지정 된 된 **명령** 개체입니다. 일부 공급자; 매개 변수가 있는 쿼리 또는 저장된 프로시저 호출을 지원 하지 않습니다. 호출의 **새로 고침** 에서 메서드는 **매개 변수** 컬렉션 이러한 공급자를 사용 하는 경우 오류가 반환 됩니다.  
  
 정의 하지 않은 고유한 경우 **매개 변수** 개체 액세스는 **매개 변수** 호출 하기 전에 컬렉션은 **새로 고침** 메서드, ADO에서는 자동으로 호출 하는 메서드의 컬렉션을 채웁니다.  
  
 공급자를 호출 하는 저장된 프로시저와 관련 된 이나 매개 변수가 있는 쿼리의 매개 변수 속성을 알고 있는 경우 성능 개선을 위해 호출할 최소화할 수 있습니다. 사용 하 여는 [CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md) 를 만들 방법을 **매개 변수** 적절 한 속성 설정 및 사용 하 여 사용 하 여 개체는 [Append](../../../ado/reference/ado-api/append-method-ado.md) 메서드를 추가 하는  **매개 변수** 컬렉션입니다. 이 설정 하 고 매개 변수 정보에 대 한 공급자를 호출 하지 않고 매개 변수 값을 반환할 수 있습니다. 수동으로 입력 해야 매개 변수 정보를 제공 하지 않는 공급자를 작성 하는 경우는 **매개 변수** 전혀 매개 변수를 사용 하려면이 메서드를 사용 하 여 컬렉션입니다. 사용 하 여는 [삭제](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md) 제거 하는 메서드 **매개 변수** 에서 개체는 **매개 변수** 필요한 경우 컬렉션입니다.  
  
 개체는 **매개 변수** 의 컬렉션은 **레코드 집합** 이동 (따라서 사용 하지 못하게 될) 범위를 벗어날 때는 **레코드 집합** 닫혀 있습니다.  
  
 저장된 프로시저를 호출할 때 **명령**, 저장된 프로시저의 반환 값/출력 매개 변수는 다음과 같이 검색 됩니다.  
  
1.  매개 변수가 있는 저장된 프로시저를 호출할 때는 **새로 고침** 메서드를는 **매개 변수** 컬렉션을 호출 하기 전에 호출 되어야 합니다는 **Execute** 에서 메서드는 **명령** 개체입니다.  
  
2.  매개 변수 및 매개 변수를 명시적으로 추가 된 저장된 프로시저를 호출할 때는 **매개 변수** 사용 하 여 컬렉션 **Append**, 반환 값/출력 매개 변수는 에추가할것인지**매개 변수** 컬렉션입니다. 반환 값에 먼저 추가 해야 합니다는 **매개 변수** 컬렉션입니다. 사용 하 여 **Append** 에 다른 매개 변수를 추가 하는 **매개 변수** 정의 순서 대로 컬렉션입니다. 예를 들어 저장된 프로시저 SPWithParam에 두 개의 매개 변수가 있습니다. 첫 번째 매개 변수 *InParam*, 입력된 매개 변수 집합이 있으므로 필요 (20)으로 정의 하 고 두 번째 매개 변수는 *OutParam*, output 매개 변수 집합이 있으므로 필요 (20)으로 정의 합니다. 다음 코드와 반환 값/출력 매개 변수를 검색할 수 있습니다.  
  
    ```  
    ' Open Connection Conn  
    set ccmd = CreateObject("ADODB.Command")  
    ccmd.Activeconnection= Conn  
  
    ccmd.CommandText="SPWithParam"  
    ccmd.commandType = 4 'adCmdStoredProc  
  
    ccmd.parameters.Append ccmd.CreateParameter(, adInteger, adParamReturnValue, , NULL)   ' return value  
    ccmd.parameters.Append ccmd.CreateParameter("InParam", adVarChar, adParamInput, 20, "hello world")   ' input parameter  
    ccmd.parameters.Append ccmd.CreateParameter("OutParam", adVarChar, adParamOuput, 20, NULL)   ' output parameter  
  
    ccmd.execute()  
  
    ' Access ccmd.parameters(0) as return value of this stored procedure  
    ' Access ccmd.parameters("OutParam") as the output parameter of this stored procedure.  
  
    ```  
  
3.  매개 변수 및 매개 변수를 호출 하 여 구성 된 저장된 프로시저를 호출할 때는 **항목** 에서 메서드는 **매개 변수** 컬렉션, 저장된 프로시저의 반환 값/출력 매개 변수 수 있습니다. 검색할 수는 **매개 변수** 컬렉션입니다. 예를 들어 저장된 프로시저 SPWithParam에 두 개의 매개 변수가 있습니다. 첫 번째 매개 변수 *InParam*, 입력된 매개 변수 집합이 있으므로 필요 (20)으로 정의 하 고 두 번째 매개 변수는 *OutParam*, output 매개 변수 집합이 있으므로 필요 (20)으로 정의 합니다. 다음 코드와 반환 값/출력 매개 변수를 검색할 수 있습니다.  
  
    ```  
    ' Open Connection Conn  
    set ccmd = CreateObject("ADODB.Command")  
    ccmd.Activeconnection= Conn  
  
    ccmd.CommandText="SPWithParam"  
    ccmd.commandType = 4 'adCmdStoredProc  
  
    ccmd.parameters.Item("InParam").value = "hello world" ' input parameter  
    ccmd.execute()  
  
    ' Access ccmd.parameters(0) as return value of stored procedure  
    ' Access ccmd.parameters(2) or ccmd.parameters("OutParam") as the output parameter.  
    ```  
  
 이 섹션에는 다음 항목 포함 되어 있습니다.  
  
-   [매개 변수 컬렉션의 속성, 메서드 및 이벤트](../../../ado/reference/ado-api/parameters-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목:  
 [Append 메서드 (ADO)](../../../ado/reference/ado-api/append-method-ado.md)   
 [CreateParameter 메서드 (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [Parameter 개체](../../../ado/reference/ado-api/parameter-object.md)
