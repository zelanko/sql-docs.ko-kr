---
description: Parameters 컬렉션(ADO)
title: Parameters 컬렉션 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: bad2570c368e469afeb7c69e4f283bdbdfe04674
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990124"
---
# <a name="parameters-collection-ado"></a>Parameters 컬렉션(ADO)
[Command](./command-object-ado.md) 개체의 모든 [Parameter](./parameter-object.md) 개체를 포함 합니다.  
  
## <a name="remarks"></a>설명  
 **Command** 개체는 **매개 변수** 개체로 구성 된 **매개 변수** 컬렉션을 포함 합니다.  
  
 **Command** 개체의 **Parameters** 컬렉션에 [Refresh](./refresh-method-ado.md) 메서드를 사용 하면 **명령** 개체에 지정 된 저장 프로시저 또는 매개 변수가 있는 쿼리에 대 한 공급자 매개 변수 정보를 검색 합니다. 일부 공급자는 저장 프로시저 호출 또는 매개 변수가 있는 쿼리를 지원 하지 않습니다. 이러한 공급자를 사용할 때 **Parameters** 컬렉션에서 **Refresh** 메서드를 호출 하면 오류가 반환 됩니다.  
  
 사용자 고유의 **매개 변수** 개체를 정의 하지 않은 경우 **Refresh** 메서드를 호출 하기 전에 **매개 변수** 컬렉션에 액세스 하면 ADO에서 자동으로 메서드를 호출 하 고 컬렉션을 채웁니다.  
  
 호출할 저장 프로시저 또는 매개 변수가 있는 쿼리와 연결 된 매개 변수의 속성을 알고 있는 경우 공급자에 대 한 호출을 최소화 하 여 성능을 향상 시킬 수 있습니다. [Createparameter](./createparameter-method-ado.md) 메서드를 사용 하 여 적절 한 속성 설정이 포함 된 **매개 변수** 개체를 만들고 [Append](./append-method-ado.md) 메서드를 사용 하 여 **Parameters** 컬렉션에 추가 합니다. 이렇게 하면 매개 변수 정보에 대 한 공급자를 호출 하지 않고도 매개 변수 값을 설정 하 고 반환할 수 있습니다. 매개 변수 정보를 제공 하지 않는 공급자에 작성 하는 경우 매개 변수를 사용할 수 있도록이 메서드를 사용 하 여 **매개 변수** 컬렉션을 수동으로 채워야 합니다. 필요한 경우 [Delete](./delete-method-ado-parameters-collection.md) 메서드를 사용 하 **여 매개 변수 컬렉션에서** **매개 변수** 개체를 제거 합니다.  
  
 레코드 **집합의** **Parameters** 컬렉션에 있는 개체는 **레코드 집합** 을 닫을 때 범위를 벗어날 수 있습니다.  
  
 **명령을**사용 하 여 저장 프로시저를 호출 하는 경우 저장 프로시저의 반환 값/출력 매개 변수는 다음과 같이 검색 됩니다.  
  
1.  매개 변수가 없는 저장 프로시저를 호출 하는 경우에는 **Command** 개체에서 **Execute** 메서드를 호출 하기 전에 **parameters** 컬렉션의 **Refresh** 메서드를 호출 해야 합니다.  
  
2.  매개 변수를 사용 하 여 저장 프로시저를 호출 하 고 **Append**를 사용 하 **여 매개 변수 컬렉션에** 매개 변수를 명시적으로 추가 하는 경우 반환 값/출력 매개 변수를 **parameters** 컬렉션에 추가 해야 합니다. 반환 값은 먼저 **Parameters** 컬렉션에 추가 해야 합니다. Add **를 사용 하 여 다른** 매개 변수를 정의 순서 대로 **parameters** 컬렉션에 추가 합니다. 예를 들어 저장 프로시저 SPWithParam에는 두 개의 매개 변수가 있습니다. 첫 번째 매개 변수인 *Inparam*은 adVarChar (20)으로 정의 된 입력 매개 변수이 고, 두 번째 매개 변수 *Outparam*은 adVarChar (20)로 정의 된 출력 매개 변수입니다. 다음 코드를 사용 하 여 반환 값/출력 매개 변수를 검색할 수 있습니다.  
  
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
  
3.  매개 변수를 사용 하 여 저장 프로시저를 호출 하 **고 매개 변수 컬렉션에서** **Item** 메서드를 호출 하 여 매개 변수를 구성 하는 경우 저장 프로시저의 반환 값/출력 매개 변수를 **parameters** 컬렉션에서 검색할 수 있습니다. 예를 들어 저장 프로시저 SPWithParam에는 두 개의 매개 변수가 있습니다. 첫 번째 매개 변수인 *Inparam*은 adVarChar (20)으로 정의 된 입력 매개 변수이 고, 두 번째 매개 변수 *Outparam*은 adVarChar (20)로 정의 된 출력 매개 변수입니다. 다음 코드를 사용 하 여 반환 값/출력 매개 변수를 검색할 수 있습니다.  
  
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
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [Parameters 컬렉션 속성, 메서드 및 이벤트](./parameters-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>참고 항목  
 [Append 메서드 (ADO)](./append-method-ado.md)   
 [CreateParameter 메서드 (ADO)](./createparameter-method-ado.md)   
 [Parameter 개체](./parameter-object.md)