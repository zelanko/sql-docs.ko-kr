---
title: "연결 개체 (ADO) | Microsoft Docs"
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
- Connection
helpviewer_keywords:
- Connection object [ADO]
ms.assetid: ef6b1824-5b12-43db-89d7-8f3d13896d4d
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: be2ba43e34c56e19dcb6eee03368ab1b3bc442a1
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="connection-object-ado"></a>연결 개체 (ADO)
데이터 원본에 대해 열린 연결을 나타냅니다.  
  
## <a name="remarks"></a>주의  
 A **연결** 개체 데이터 소스와 고유 세션을 나타냅니다. 클라이언트/서버 데이터베이스 시스템에 해당 하는 실제 네트워크 연결 서버에 수도 있습니다. 공급자, 일부 컬렉션, 메서드 또는 속성을 지 원하는 기능에 따라 한 **연결** 개체를 사용할 수 없습니다.  
  
 컬렉션, 메서드 및 속성의는 **연결** 개체를 다음을 수행할 수 있습니다.  
  
-   사용 하 여 열기 전에 연결을 구성에서 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md), [ConnectionTimeout](../../../ado/reference/ado-api/connectiontimeout-property-ado.md), 및 [모드](../../../ado/reference/ado-api/mode-property-ado.md) 속성입니다. **ConnectionString** 은의 기본 속성은 **연결** 개체입니다.  
  
-   설정의 [앞](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성을 호출 하는 클라이언트는 [OLE DB에 대 한 Microsoft 커서 서비스](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)이며 지원 일괄 업데이트 합니다.  
  
-   와 연결에 대 한 기본 데이터베이스를 설정 하는 [DefaultDatabase](../../../ado/reference/ado-api/defaultdatabase-property.md) 속성입니다.  
  
-   트랜잭션에 대 한 격리 수준을 사용 하 여 연결에서 열 집합은 [IsolationLevel](../../../ado/reference/ado-api/isolationlevel-property.md) 속성입니다.  
  
-   지정 된 OLE DB 공급자는 [공급자](../../../ado/reference/ado-api/provider-property-ado.md) 속성입니다.  
  
-   을 설정 하 고 해제 실제 연결을 사용 하 여 데이터 소스는 [열려](../../../ado/reference/ado-api/open-method-ado-connection.md) 및 [닫기](../../../ado/reference/ado-api/close-method-ado.md) 메서드.  
  
-   와 연결에서 명령을 실행의 [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) 메서드 사용 하 여 실행을 구성 하 고는 [CommandTimeout](../../../ado/reference/ado-api/commandtimeout-property-ado.md) 속성입니다.  
  
    > [!NOTE]
    >  명령 개체를 사용 하지 않고 쿼리를 실행 하는 쿼리 문자열을 전달는 **Execute** 의 메서드는 **연결** 개체입니다. 그러나 한 [명령](../../../ado/reference/ado-api/command-object-ado.md) 명령 텍스트를 유지 하 고 했다가 나중에 다시 실행 하거나 쿼리 매개 변수를 사용 하려는 경우 개체가 필요 합니다.  
  
-   공급자가 지 원하는 경우와 중첩 된 트랜잭션을 포함 하 여 열린 연결에는 트랜잭션 관리는 [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md), [CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md), 및 [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) 메서드 및 [특성](../../../ado/reference/ado-api/attributes-property-ado.md) 속성입니다.  
  
-   사용 하 여 데이터 소스에서 반환 된 오류 검사는 [오류](../../../ado/reference/ado-api/errors-collection-ado.md) 컬렉션입니다.  
  
-   함께 사용할 ADO 구현에서 버전을 읽습니다.는 [버전](../../../ado/reference/ado-api/version-property-ado.md) 속성입니다.  
  
-   데이터베이스에 대 한 스키마 정보는 [OpenSchema](../../../ado/reference/ado-api/openschema-method.md) 메서드.  
  
 만들 수 있습니다 **연결** 이전에 정의 된 다른 개체와 독립적으로 개체입니다.  
  
 네이티브 메서드에서 듯 명명 된 명령 또는 저장된 프로시저를 실행할 수 있습니다는 **연결** 다음 섹션에 나와 있는 것 처럼 개체입니다. 명명 된 명령에 동일한 이름으로 저장된 프로시저의 경우 호출을 수행 하면 "로 인해 네이티브 메서드"에 **연결** 개체에는 항상 저장 프로시저 대신 명명 된 명령을 실행 합니다.  
  
> [!NOTE]
>  이 기능을 사용 하지 마십시오 (네이티브 메서드 인쇄 된 하는 경우 명명 된 명령 또는 저장된 프로시저를 호출의 **연결** 개체)는 Microsoft®.NET Framework 응용 프로그램에서 때문에 기능 충돌의 기본 구현 com 상호 운용.NET Framework는 방식과  
  
## <a name="execute-a-command-as-a-native-method-of-a-connection-object"></a>연결 개체의 기본 방법으로 명령을 실행합니다  
 명령을 실행 하려면 명령을 이름을 사용 하 여 지정 된 **명령** 개체 [이름](../../../ado/reference/ado-api/name-property-ado.md) 속성입니다. 설정의 **ActiveConnection** 속성은 **명령** 개체를 연결 합니다. 메서드처럼 하는 경우 명령 이름 사용 되는 위치 명령문을 발급 하는 **연결** 매개 변수, 개체 및 **레코드 집합** 모든 행이 반환 하는 경우 개체입니다. 설정의 **레코드 집합** 결과 사용자 지정 하는 속성 **레코드 집합**합니다. 예를 들어  
  
```  
Dim cnn As New ADODB.Connection  
Dim cmd As New ADODB.Command  
Dim rst As New ADODB.Recordset  
...  
cnn.Open "..."  
cmd.Name = "yourCommandName"  
cmd.ActiveConnection = cnn  
...  
'Your command name, any parameters, and an optional Recordset.  
cnn. "parameter", rst  
```  
  
## <a name="execute-a-stored-procedure-as-a-native-method-of-a-connection-object"></a>연결 개체의 기본 방법으로 저장된 프로시저를 실행 합니다.  
 저장된 프로시저를 실행 하려면 저장된 프로시저 이름이 사용 되는 위치 처럼에 메서드처럼 문을 발행는 **연결** 묶인 매개 변수 개체입니다. ADO는 "최상의 추측" 매개 변수 형식의 생성 됩니다. 예를 들어  
  
```  
Dim cnn As New ADODB.Connection  
...  
'Your stored procedure name and any parameters.  
cnn. "parameter"  
```  
  
 **연결** 개체는 스크립팅 작업에 안전 합니다.  
  
 이 섹션에는 다음 항목 포함 되어 있습니다.  
  
-   [연결 개체 속성, 메서드 및 이벤트](../../../ado/reference/ado-api/connection-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목:  
 [Command 개체 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [Errors 컬렉션 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [Properties 컬렉션 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [레코드 집합 개체 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [부록 A: 공급자](../../../ado/guide/appendixes/appendix-a-providers.md)

