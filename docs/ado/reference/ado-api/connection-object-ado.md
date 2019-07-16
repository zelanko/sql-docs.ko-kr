---
title: 연결 개체 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection
helpviewer_keywords:
- Connection object [ADO]
ms.assetid: ef6b1824-5b12-43db-89d7-8f3d13896d4d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 278e2d90ed20b99706f00acf72e2892941c42865
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67933570"
---
# <a name="connection-object-ado"></a>연결 개체(ADO)
데이터 원본에 대해 열린 연결을 나타냅니다.  
  
## <a name="remarks"></a>설명  
 A **연결** 개체 데이터 소스를 사용 하 여 고유한 세션을 나타냅니다. 클라이언트/서버 데이터베이스 시스템에서 서버는 실제 네트워크 연결에 해당 하는 수 있습니다. 공급자, 몇 가지 컬렉션, 메서드 또는 속성을 지 원하는 기능에 따라 한 **연결** 개체를 사용할 수 없습니다.  
  
 컬렉션, 메서드 및 속성을 사용 하 여는 **연결** 개체를 다음을 수행할 수 있습니다.  
  
-   사용 하 여 열기 전에 연결을 구성 합니다 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)를 [ConnectionTimeout](../../../ado/reference/ado-api/connectiontimeout-property-ado.md), 및 [모드](../../../ado/reference/ado-api/mode-property-ado.md) 속성입니다. **ConnectionString** 의 기본 속성을 **연결** 개체입니다.  
  
-   설정 합니다 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성을 호출 하는 클라이언트는 [OLE DB에 대 한 Microsoft 커서 서비스](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)는 지원 일괄 업데이트 합니다.  
  
-   연결에 대 한 기본 데이터베이스를 설정 합니다 [DefaultDatabase](../../../ado/reference/ado-api/defaultdatabase-property.md) 속성입니다.  
  
-   트랜잭션 격리 수준을 사용 하 여 연결에 대해 열려 집합 합니다 [IsolationLevel](../../../ado/reference/ado-api/isolationlevel-property.md) 속성입니다.  
  
-   사용 하 여 OLE DB 공급자를 지정 합니다 [공급자](../../../ado/reference/ado-api/provider-property-ado.md) 속성입니다.  
  
-   를 설정 하 고 해제 한 실제 연결을 사용 하 여 데이터 소스를 [열려](../../../ado/reference/ado-api/open-method-ado-connection.md) 하 고 [닫기](../../../ado/reference/ado-api/close-method-ado.md) 메서드.  
  
-   사용한 연결로 명령을 실행 합니다 [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) 메서드 사용 하 여 실행을 구성 하 고는 [CommandTimeout](../../../ado/reference/ado-api/commandtimeout-property-ado.md) 속성.  
  
    > [!NOTE]
    >  명령 개체를 사용 하지 않고 쿼리를 실행 하려면 쿼리 문자열을 전달 하는 **Execute** 메서드를 **연결** 개체입니다. 그러나를 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체는 명령 텍스트를 유지 하 고 다시 실행 하거나 쿼리 매개 변수를 사용 하려는 경우에 필요 합니다.  
  
-   공급자가 지 원하는 경우를 사용 하 여 중첩 된 트랜잭션을 포함 하 여 열린 연결에서 트랜잭션을 관리 합니다 [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)를 [CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md), 및 [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) 메서드 및 [특성](../../../ado/reference/ado-api/attributes-property-ado.md) 속성입니다.  
  
-   사용 하 여 데이터 소스에서 반환 된 오류를 검토 합니다 [오류](../../../ado/reference/ado-api/errors-collection-ado.md) 컬렉션입니다.  
  
-   사용한 ADO 구현에서 버전을 읽을 합니다 [버전](../../../ado/reference/ado-api/version-property-ado.md) 속성입니다.  
  
-   사용 하 여 데이터베이스에 대 한 스키마 정보를 [OpenSchema](../../../ado/reference/ado-api/openschema-method.md) 메서드.  
  
 만들 수 있습니다 **연결** 이전에 정의 된 다른 개체와 독립적으로 개체입니다.  
  
 네이티브 메서드인 것 처럼 명명 된 명령 또는 저장된 프로시저를 실행할 수 있습니다는 **연결** 다음 섹션에 나와 있는 것 처럼 개체입니다. 명명 된 명령에 동일한 이름으로 저장된 프로시저의 경우 호출 "네이티브 메서드"에 **연결** 개체는 항상 저장 프로시저 대신 명명 된 명령을 실행 합니다.  
  
> [!NOTE]
>  이 기능을 사용 하지 마십시오 (에서 네이티브 메서드 처럼 명명 된 명령 또는 저장된 프로시저를 호출 합니다 **연결** 개체) Microsoft®.NET Framework 응용 프로그램에서 때문에 기본 구현의 기능 충돌 com 상호 운용.NET Framework는 방식  
  
## <a name="execute-a-command-as-a-native-method-of-a-connection-object"></a>연결 개체의 기본 메서드로 명령 실행  
 명령을 실행할 제공 명령을 사용 하 여 이름을 합니다 **명령** 개체 [이름](../../../ado/reference/ado-api/name-property-ado.md) 속성입니다. 설정 합니다 **ActiveConnection** 의 속성을 **명령** 연결 개체. 명령 이름에 메서드인 것 처럼 되는 문을 다음 합니다 **연결** 뒤에 매개 변수를 개체 및 **레코드 집합** 모든 행이 반환 하는 경우 개체입니다. 설정 된 **레코드 집합** 결과 사용자 지정 속성 **레코드 집합**합니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
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
  
## <a name="execute-a-stored-procedure-as-a-native-method-of-a-connection-object"></a>연결 개체의 기본 메서드로 저장된 프로시저를 실행 합니다.  
 저장된 프로시저를 실행 하려면 저장된 프로시저 이름에 메서드인 것 처럼 되는 문을 실행 합니다 **연결** 뒤에 매개 변수 개체입니다. ADO 매개 변수 형식의 "최상의 추측"를 확인 합니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
```  
Dim cnn As New ADODB.Connection  
...  
'Your stored procedure name and any parameters.  
cnn. "parameter"  
```  
  
 합니다 **연결** 개체가 스크립팅 작업에 안전 합니다.  
  
 이 섹션에서는 다음 항목을 포함합니다.  
  
-   [연결 개체 속성, 메서드 및 이벤트](../../../ado/reference/ado-api/connection-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목  
 [명령 개체 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [Errors 컬렉션 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [Properties 컬렉션 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [레코드 집합 개체 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [부록 A: 공급자](../../../ado/guide/appendixes/appendix-a-providers.md)
