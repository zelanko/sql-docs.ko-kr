---
description: 연결 개체(ADO)
title: Connection 개체 (ADO) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 0ce6a6e3c2e665c57b9a82d968dac3cf3c74a731
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775962"
---
# <a name="connection-object-ado"></a>연결 개체(ADO)
데이터 소스에 대해 열려 있는 연결을 나타냅니다.  
  
## <a name="remarks"></a>설명  
 **Connection** 개체는 데이터 원본에 대 한 고유한 세션을 나타냅니다. 클라이언트/서버 데이터베이스 시스템에서 서버에 대 한 실제 네트워크 연결에 해당 하는 것일 수 있습니다. 공급자가 지 원하는 기능에 따라 **연결** 개체의 일부 컬렉션, 메서드 또는 속성을 사용 하지 못할 수 있습니다.  
  
 **연결** 개체의 컬렉션, 메서드 및 속성을 사용 하 여 다음을 수행할 수 있습니다.  
  
-   [ConnectionString](./connectionstring-property-ado.md), [ConnectionTimeout](./connectiontimeout-property-ado.md)및 [Mode](./mode-property-ado.md) 속성을 사용 하 여 열기 전에 연결을 구성 합니다. **ConnectionString** 은 **Connection** 개체의 기본 속성입니다.  
  
-   [CursorLocation](./cursorlocation-property-ado.md) 속성을 client로 설정 하 여 batch 업데이트를 지 원하는 [OLE DB 용 Microsoft Cursor Service](../../guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)를 호출 합니다.  
  
-   [Defaultdatabase](./defaultdatabase-property.md) 속성을 사용 하 여 연결에 대 한 기본 데이터베이스를 설정 합니다.  
  
-   [IsolationLevel](./isolationlevel-property.md) 속성을 사용 하 여 연결에서 열린 트랜잭션의 격리 수준을 설정 합니다.  
  
-   [공급자](./provider-property-ado.md) 속성을 사용 하 여 OLE DB 공급자를 지정 합니다.  
  
-   [Open](./open-method-ado-connection.md) 및 [Close](./close-method-ado.md) 메서드를 사용 하 여 데이터 원본에 대 한 실제 연결을 설정 하 고 나중에 중단 합니다.  
  
-   [Execute](./execute-method-ado-connection.md) 메서드를 사용 하 여 연결에 대해 명령을 실행 하 고 [CommandTimeout](./commandtimeout-property-ado.md) 속성을 사용 하 여 실행을 구성 합니다.  
  
    > [!NOTE]
    >  명령 개체를 사용 하지 않고 쿼리를 실행 하려면 **연결** 개체의 **execute** 메서드에 쿼리 문자열을 전달 합니다. 그러나 명령 텍스트를 유지 하 고 다시 실행 하거나 쿼리 매개 변수를 사용 하려는 경우에는 [command](./command-object-ado.md) 개체가 필요 합니다.  
  
-   [BeginTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md), [CommitTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md)및 [RollbackTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md) 메서드와 [Attributes](./attributes-property-ado.md) 속성이 포함 된 중첩 트랜잭션을 포함 하 여 열려 있는 연결의 트랜잭션을 관리 합니다.  
  
-   [Errors](./errors-collection-ado.md) 컬렉션을 사용 하 여 데이터 원본에서 반환 된 오류를 검사 합니다.  
  
-   [Version](./version-property-ado.md) 속성에 사용 된 ADO 구현에서 버전을 읽습니다.  
  
-   [OpenSchema](./openschema-method.md) 메서드를 사용 하 여 데이터베이스에 대 한 스키마 정보를 가져옵니다.  
  
 이전에 정의 된 다른 개체와 독립적으로 **연결** 개체를 만들 수 있습니다.  
  
 다음 섹션에 표시 된 것 처럼 명명 된 명령 또는 저장 프로시저를 **연결** 개체의 네이티브 메서드인 것 처럼 실행할 수 있습니다. 명명 된 명령의 이름이 저장 프로시저의 이름과 같을 경우 **연결** 개체에서 "네이티브 메서드 호출"을 호출 하면 항상 저장 프로시저 대신 명명 된 명령을 실행 합니다.  
  
> [!NOTE]
>  Microsoft® .NET Framework 응용 프로그램에서이 기능 (명명 된 명령 또는 저장 프로시저를 **연결** 개체의 네이티브 메서드인 것 처럼 호출)을 사용 하지 마세요 .이 기능은 .NET Framework의 기본 구현이 COM과 상호 작용 하는 방식과 충돌 하기 때문입니다.  
  
## <a name="execute-a-command-as-a-native-method-of-a-connection-object"></a>연결 개체의 네이티브 메서드로 명령을 실행 합니다.  
 명령을 실행 하려면 명령 개체 [이름](./name-property-ado.md) **속성을 사용** 하 여 명령에 이름을 지정 합니다. **명령** 개체의 **ActiveConnection** 속성을 연결로 설정 합니다. 그런 다음 명령 이름이 **연결** 개체의 메서드인 것 처럼 사용 되는 문을 실행 한 다음 매개 변수를 사용 하 고 행이 반환 되 면 **레코드 집합** 개체를 실행 합니다. **레코드** 집합 속성을 설정 하 여 결과 **레코드**집합을 사용자 지정 합니다. 예를 들면 다음과 같습니다.  
  
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
  
## <a name="execute-a-stored-procedure-as-a-native-method-of-a-connection-object"></a>연결 개체의 네이티브 메서드로 저장 프로시저 실행  
 저장 프로시저를 실행 하려면 저장 프로시저 이름이 **Connection** 개체의 메서드인 것 처럼 사용 된 다음 매개 변수를 사용 하는 문을 실행 합니다. ADO는 매개 변수 형식의 "최상의 추측"을 만듭니다. 예를 들면 다음과 같습니다.  
  
```  
Dim cnn As New ADODB.Connection  
...  
'Your stored procedure name and any parameters.  
cnn. "parameter"  
```  
  
 **연결** 개체는 스크립팅에 안전 합니다.  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [Connection 개체 속성, 메서드 및 이벤트](./connection-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>참고 항목  
 [Command 개체 (ADO)](./command-object-ado.md)   
 [Errors 컬렉션 (ADO)](./errors-collection-ado.md)   
 [Properties 컬렉션 (ADO)](./properties-collection-ado.md)   
 [레코드 집합 개체 (ADO)](./recordset-object-ado.md)   
 [부록 A: 공급자](../../guide/appendixes/appendix-a-providers.md)