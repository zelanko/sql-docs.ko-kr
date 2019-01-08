---
title: Parameters 컬렉션 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::get_Parameters
- Command15::Parameters
- Command15::GetParameters
helpviewer_keywords:
- Parameters collection [ADO]
ms.assetid: 497cae10-3913-422a-9753-dcbb0a639b1b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7dbfff2a8db4405e19eb448e7bd7db5c8ac236f8
ms.sourcegitcommit: 98324d9803edfa52508b6d5d3554614d0350a0b9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52321799"
---
# <a name="parameters-collection-ado"></a>Parameters 컬렉션(ADO)
모두 포함 합니다 [매개 변수](../../../ado/reference/ado-api/parameter-object.md) 의 개체를 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체입니다.  
  
## <a name="remarks"></a>Remarks  
 A **명령** 개체에는 **매개 변수** 컬렉션으로 이루어져 **매개 변수** 개체입니다.  
  
 사용 하 여 합니다 [새로 고침](../../../ado/reference/ado-api/refresh-method-ado.md) 메서드를 **명령** 개체의 **매개 변수** 컬렉션 저장된 프로시저 또는 매개 변수가 있는 쿼리를 실행 하는 것에 대 한 공급자 매개 변수 정보를 검색 합니다. 에 지정 된 **명령** 개체입니다. 저장된 프로시저 호출 또는 매개 변수가 있는 쿼리에 일부 공급자를 지원 하지 않습니다. 호출을 **새로 고침** 메서드는 **매개 변수** 컬렉션 이러한 공급자를 사용 하는 경우 오류가 반환 됩니다.  
  
 정의 하지 않은 고유한 경우 **매개 변수** 개체에 액세스를 **매개 변수** 호출 하기 전에 컬렉션을 **새로 고침** 메서드, ADO를 자동으로 호출 합니다 메서드를 컬렉션을 채웁니다.  
  
 공급자를 호출 하는 저장된 프로시저를 사용 하 여 연결 또는 매개 변수가 있는 쿼리의 매개 변수 속성을 알고 있는 경우 성능 향상을 위해 호출 하려는 최소화할 수 있습니다. 사용 합니다 [CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md) 메서드를 **매개 변수** 사용 하 여 확인 하 고 적절 한 속성 설정을 사용 하 여 개체를 [추가](../../../ado/reference/ado-api/append-method-ado.md) 메서드를 추가할는  **매개 변수** 컬렉션입니다. 이 방법으로 설정 하 고 매개 변수 정보에 대 한 공급자를 호출 하지 않고 매개 변수 값을 반환할 수 있습니다. 매개 변수 정보를 제공 하지 않는 공급자를 작성 하는 경우 수동으로 채워야 합니다 **매개 변수** 전혀 매개 변수를 사용 하려면이 메서드를 사용 하 여 컬렉션입니다. 사용 된 [삭제](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md) 제거 하는 방법 **매개 변수** 에서 개체를 **매개 변수** 필요한 경우 컬렉션.  
  
 개체는 **매개 변수** 의 컬렉션을 **레코드 집합** (따라서 사용할 수 없게 되) 범위를 벗어납니다 이동 때를 **레코드 집합** 닫혀 합니다.  
  
 사용 하 여 저장된 프로시저를 호출할 때 **명령**, 저장된 프로시저의 반환 값/출력 매개 변수는 다음과 같이 검색 됩니다.  
  
1.  매개 변수가 있는 저장된 프로시저를 호출 하는 경우는 **새로 고침** 메서드를를 **매개 변수** 컬렉션을 호출 하기 전에 호출 해야 합니다 **Execute** 메서드를는 **명령** 개체입니다.  
  
2.  매개 변수 및 매개 변수를 명시적으로 추가 사용 하 여 저장된 프로시저를 호출할 때 합니다 **매개 변수** 수집과 **추가**, 반환 값/출력 매개 변수는 에추가할것인지**매개 변수** 컬렉션입니다. 반환 값에 먼저 추가 되어야 합니다 **매개 변수** 컬렉션입니다. 사용 하 여 **추가** 에 다른 매개 변수를 추가 합니다 **매개 변수** 정의 순서 대로 컬렉션입니다. 예를 들어 저장된 프로시저 SPWithParam에 두 개의 매개 변수입니다. 첫 번째 매개 변수를 *InParam*입력된 매개 변수 집합이 있으므로 필요 (20)으로 정의 되어 두 번째 매개 변수를 *OutParam*, 출력 매개 변수 집합이 있으므로 필요 (20)으로 정의 합니다. 다음 코드를 사용 하 여 반환 값/출력 매개 변수를 검색할 수 있습니다.  
  
    ```vb
    ' Open Connection Conn  
    set ccmd = CreateObject("ADODB.Command")  
    ccmd.Activeconnection= Conn  
  
    ccmd.CommandText="SPWithParam"  
    ccmd.commandType = 4 'adCmdStoredProc  
  
    ccmd.parameters.Append ccmd.CreateParameter(, adInteger, adParamReturnValue, , NULL)   ' return value  
    ccmd.parameters.Append ccmd.CreateParameter("InParam", adVarChar, adParamInput, 20, "hello world")   ' input parameter  
    ccmd.parameters.Append ccmd.CreateParameter("OutParam", adVarChar, adParamOutput, 20, NULL)   ' output parameter  
  
    ccmd.execute()  
  
    ' Access ccmd.parameters(0) as return value of this stored procedure  
    ' Access ccmd.parameters("OutParam") as the output parameter of this stored procedure.  
  
    ```  
  
3.  매개 변수 및 매개 변수를 호출 하 여 구성를 사용 하 여 저장된 프로시저를 호출할 때 합니다 **항목** 메서드는 **매개 변수** 컬렉션, 저장된 프로시저의 반환 값/출력 매개 변수 수 검색할 수는 **매개 변수** 컬렉션입니다. 예를 들어 저장된 프로시저 SPWithParam에 두 개의 매개 변수입니다. 첫 번째 매개 변수를 *InParam*입력된 매개 변수 집합이 있으므로 필요 (20)으로 정의 되어 두 번째 매개 변수를 *OutParam*, 출력 매개 변수 집합이 있으므로 필요 (20)으로 정의 합니다. 다음 코드를 사용 하 여 반환 값/출력 매개 변수를 검색할 수 있습니다.  
  
    ```vb
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
  
 이 섹션에서는 다음 항목을 포함합니다.  
  
-   [Parameters 컬렉션 속성, 메서드 및 이벤트](../../../ado/reference/ado-api/parameters-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목  
 [Append 메서드 (ADO)](../../../ado/reference/ado-api/append-method-ado.md)   
 [CreateParameter 메서드 (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [Parameter 개체](../../../ado/reference/ado-api/parameter-object.md)
