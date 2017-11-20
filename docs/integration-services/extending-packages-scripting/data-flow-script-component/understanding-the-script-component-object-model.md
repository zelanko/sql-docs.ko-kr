---
title: "스크립트 구성 요소 개체 모델 이해 | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- Script component [Integration Services], object model
ms.assetid: 2a0aae82-39cc-4423-b09a-72d2f61033bd
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 09de00344fe94087b6287b07c4b1ffe933d27b7c
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="understanding-the-script-component-object-model"></a>스크립트 구성 요소 개체 모델 이해
  에 설명 된 대로 [코딩 및 스크립트 구성 요소 디버깅](../../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md), 스크립트 구성 요소 프로젝트에는 세 개의 프로젝트 항목이 포함 되어 있습니다.  
  
1.  **ScriptMain** 포함 하는 항목이 **ScriptMain** 클래스 코드를 작성 합니다. **ScriptMain** 클래스에서 상속 된 **UserComponent** 클래스입니다.  
  
2.  **ComponentWrapper** 포함 하는 항목이 **UserComponent** 클래스의 인스턴스 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 메서드 및 데이터를 처리 하 고 패키지와 상호 작용에 사용할 속성을 포함 하 합니다. **ComponentWrapper** 항목도 포함 되어 **연결** 및 **변수** 컬렉션 클래스입니다.  
  
3.  **BufferWrapper** 에서 상속 하는 클래스를 포함 하는 항목이 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> 각 열에 대 한 각 입력 및 출력, 및 형식화 된 속성에 대 한 합니다.  
  
 코드를 작성할 때는 **ScriptMain** 항목을 사용할지 개체, 메서드 및 속성을이 항목에서 설명 합니다. 각 구성 요소에서 여기에 나열된 메서드를 모두 사용하는 것은 아니지만 사용될 경우에는 여기에 표시된 순서대로 사용됩니다.  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 기본 클래스에는 이 항목에 설명된 메서드의 구현 코드가 들어 있지 않습니다. 따라서 메서드 구현에 기본 클래스 구현에 대한 호출을 추가하는 것은 불필요하지만 해가 되지는 않습니다.  
  
 특정 유형의 스크립트 구성 요소에서 메서드 및 이러한 클래스의 속성을 사용 하는 방법에 대 한 내용은 섹션을 참조 하십시오. [Additional Script Component Examples](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md)합니다. 예 항목에는 전체 코드 예제도 들어 있습니다.  
  
## <a name="acquireconnections-method"></a>AcquireConnections 메서드  
 원본 및 대상은 일반적으로 외부 데이터 원본에 연결해야 합니다. <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.AcquireConnections%2A> 기본 클래스의 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 메서드를 재정의하여 적절한 연결 관리자에서 연결 또는 연결 정보를 검색합니다.  
  
 다음 예제에서는 반환 된 **System.Data.SqlClient.SqlConnection** ADO.NET 연결 관리자에서 합니다.  
  
```vb  
Dim connMgr As IDTSConnectionManager100  
Dim sqlConn As SqlConnection  
  
Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
    connMgr = Me.Connections.MyADONETConnection  
    sqlConn = CType(connMgr.AcquireConnection(Nothing), SqlConnection)  
  
End Sub  
```  
  
 다음 예제에서 플랫 파일 연결 관리자, 전체 경로 파일 이름을 반환 하 고 다음 사용 하 여 파일을 엽니다는 **System.IO.StreamReader**합니다.  
  
```vb  
Private textReader As StreamReader  
Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
    Dim connMgr As IDTSConnectionManager100 = _  
        Me.Connections.MyFlatFileSrcConnectionManager  
    Dim exportedAddressFile As String = _  
        CType(connMgr.AcquireConnection(Nothing), String)  
    textReader = New StreamReader(exportedAddressFile)  
  
End Sub  
```  
  
## <a name="preexecute-method"></a>PreExecute 메서드  
 데이터 행의 처리를 시작하기 전에만 한 번 수행해야 하는 처리가 있을 때마다 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.PreExecute%2A> 기본 클래스의 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 메서드를 재정의합니다. 예를 들어 대상에서 데이터 원본에 각 데이터 행을 삽입하는 데 사용할 매개 변수가 있는 명령을 구성할 수 있습니다.  
  
```vb  
    Dim sqlConn As SqlConnection  
    Dim sqlCmd As SqlCommand  
    Dim sqlParam As SqlParameter  
...  
    Public Overrides Sub PreExecute()  
  
        sqlCmd = New SqlCommand("INSERT INTO Person.Address2(AddressID, City) " & _  
            "VALUES(@addressid, @city)", sqlConn)  
        sqlParam = New SqlParameter("@addressid", SqlDbType.Int)  
        sqlCmd.Parameters.Add(sqlParam)  
        sqlParam = New SqlParameter("@city", SqlDbType.NVarChar, 30)  
        sqlCmd.Parameters.Add(sqlParam)  
  
    End Sub  
```  
  
```csharp  
SqlConnection sqlConn;   
SqlCommand sqlCmd;   
SqlParameter sqlParam;   
  
public override void PreExecute()   
{   
  
    sqlCmd = new SqlCommand("INSERT INTO Person.Address2(AddressID, City) " + "VALUES(@addressid, @city)", sqlConn);   
    sqlParam = new SqlParameter("@addressid", SqlDbType.Int);   
    sqlCmd.Parameters.Add(sqlParam);   
    sqlParam = new SqlParameter("@city", SqlDbType.NVarChar, 30);   
    sqlCmd.Parameters.Add(sqlParam);   
  
}  
```  
  
## <a name="processing-inputs-and-outputs"></a>입력 및 출력 처리  
  
### <a name="processing-inputs"></a>입력 처리  
 변환 또는 대상으로 구성된 스크립트 구성 요소에는 하나의 입력이 있습니다.  
  
#### <a name="what-the-bufferwrapper-project-item-provides"></a>BufferWrapper 프로젝트 항목의 제공 내용  
 구성 했는지, 각 입력에 대해는 **BufferWrapper** 에서 파생 된 클래스를 포함 하는 프로젝트 항목 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> 입력으로 동일한 이름을 가진 합니다. 각 입력 버퍼 클래스에는 다음과 같은 속성, 함수 및 메서드가 들어 있습니다.  
  
-   선택한 각 입력 열에 대한 명명되고 형식화된 접근자 속성. 이러한 속성은 읽기 전용 또는 읽기/쓰기에 따라는 **사용 유형을** 에서 열에 지정한는 **입력 열** 의 페이지는 **스크립트 변환 편집기**합니다.  
  
-   A  **\<열 > _IsNull** 각 속성이 선택한 입력 열입니다. 이 속성은 또한 읽기 전용 또는 읽기/쓰기에 따라는 **사용 유형을** 열에 대해 지정 합니다.  
  
-   A **DirectRowTo\<outputbuffer >** 메서드 각각에 대 한 출력을 구성 합니다. 행을 동일한 여러 출력 중 하나로 필터링 하는 경우에 이러한 메서드를 사용 합니다 **ExclusionGroup**합니다.  
  
-   A **NextRow** 다음 입력된 행을 가져오는 함수를 및 **EndOfRowset** 데이터의 마지막 버퍼가 처리 되었는지 여부를 결정 하는 함수입니다. 일반적으로 불필요 이러한 함수 입력 처리에서 구현 된 메서드를 사용 하는 경우는 **UserComponent** 기본 클래스입니다. 다음 섹션에 대 한 자세한 정보를 제공는 **UserComponent** 기본 클래스입니다.  
  
#### <a name="what-the-componentwrapper-project-item-provides"></a>ComponentWrapper 프로젝트 항목의 제공 내용  
 ComponentWrapper 프로젝트 항목 클래스를 포함 **UserComponent** 에서 파생 된 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>합니다. **ScriptMain** 사용자 지정 코드를 작성 하는 클래스에서 파생 **UserComponent**합니다. **UserComponent** 클래스에는 다음과 같은 메서드가 들어 있습니다.  
  
-   재정의 된 구현을 **ProcessInput** 메서드. 이 데이터 흐름는 엔진 호출 다음 런타임에 후 메서드는 **PreExecute** 수 여러 번 호출 될 메서드를 합니다. **ProcessInput** 처리를 넘깁니다는  **\<inputbuffer > _ProcessInput** 메서드. 그런 다음 **ProcessInput** 메서드 입력된 버퍼의 끝을 확인 하 고, 버퍼의 끝에 도달한 경우 재정의 가능한 호출 **FinishOutputs** 메서드와 전용 **MarkOutputsAsFinished** 메서드. **MarkOutputsAsFinished** 메서드를 호출 **SetEndOfRowset** 마지막 출력 버퍼에 있습니다.  
  
-   재정의 가능한 구현을  **\<inputbuffer > _ProcessInput** 메서드. 이 기본 구현은 단순히 각 입력된 행과 호출을 반복  **\<inputbuffer > _ProcessInputRow**합니다.  
  
-   재정의 가능한 구현을  **\<inputbuffer > _ProcessInputRow** 메서드. 기본 구현은 비어 있습니다. 이 메서드는 일반적으로 사용자 지정 데이터 처리 코드를 작성하기 위해 재정의하는 메서드입니다.  
  
#### <a name="what-your-custom-code-should-do"></a>사용자 지정 코드로 수행하는 작업  
 다음 메서드를 사용 하 여에서 입력을 처리 하는 **ScriptMain** 클래스:  
  
-   재정의  **\<inputbuffer > _ProcessInputRow** 통과할 때 각 입력된 행의 데이터를 처리할 수 있습니다.  
  
-   재정의  **\<inputbuffer > _ProcessInput** 입력된 행을 반복 하는 동안 추가 작업을 수행 해야 할 경우에 합니다. (에 대 한 테스트 해야 하는 예를 들어 **EndOfRowset** 어떤 작업도 몇 가지 다른 모든 행이 처리 된.) 호출  **\<inputbuffer > _ProcessInputRow** 행 처리를 수행 합니다.  
  
-   재정의 **FinishOutputs** 닫기 전에 출력에 작업을 수행 해야 할 경우.  
  
 **ProcessInput** 메서드를 사용 하면 적절 한 시간에 이러한 메서드를 호출 합니다.  
  
### <a name="processing-outputs"></a>출력 처리  
 원본 또는 변환으로 구성된 스크립트 구성 요소에는 하나 이상의 출력이 있습니다.  
  
#### <a name="what-the-bufferwrapper-project-item-provides"></a>BufferWrapper 프로젝트 항목의 제공 내용  
 BufferWrapper 프로젝트 항목에는 사용자가 구성한 각 출력에 대해 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer>에서 파생되며 출력과 이름이 동일한 클래스가 들어 있습니다. 각 입력 버퍼 클래스에는 다음과 같은 속성 및 메서드가 들어 있습니다.  
  
-   각 출력 열에 대한 명명되고 형식화된 쓰기 전용 접근자 속성  
  
-   쓰기 전용  **\<열 > _IsNull** 열 값을 설정 하는 데 사용할 수 있는 각 선택한 출력 열에 대 한 속성 **null**합니다.  
  
-   **AddRow** 메서드를 비어 있는 새 행을 출력 버퍼에 추가 합니다.  
  
-   A **SetEndOfRowset** 메서드 데이터 버퍼가 더 이상 예상 되는 데이터 흐름 엔진 수 있도록 합니다. 또한는 **EndOfRowset** 현재 버퍼가 마지막 데이터 버퍼 인지 여부를 결정 하는 함수입니다. 일반적으로 불필요 이러한 함수 입력 처리에서 구현 된 메서드를 사용 하는 경우는 **UserComponent** 기본 클래스입니다.  
  
#### <a name="what-the-componentwrapper-project-item-provides"></a>ComponentWrapper 프로젝트 항목의 제공 내용  
 ComponentWrapper 프로젝트 항목 클래스를 포함 **UserComponent** 에서 파생 된 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>합니다. **ScriptMain** 사용자 지정 코드를 작성 하는 클래스에서 파생 **UserComponent**합니다. **UserComponent** 클래스에는 다음과 같은 메서드가 들어 있습니다.  
  
-   재정의 된 구현을 **PrimeOutput** 메서드. 먼저이 메서드를 호출 하는 데이터 흐름 엔진 **ProcessInput** 런타임 시 한 번만 호출 됩니다. **PrimeOutput** 처리를 넘깁니다는 **CreateNewOutputRows** 메서드. 그런 다음 구성 요소가 원본인 경우 (즉, 구성 요소는 입력에) **PrimeOutput** 재정의 가능한 호출 **FinishOutputs** 메서드와 전용 **MarkOutputsAsFinished** 메서드. **MarkOutputsAsFinished** 메서드 호출 **SetEndOfRowset** 마지막 출력 버퍼에 있습니다.  
  
-   재정의 가능한 구현을 **CreateNewOutputRows** 메서드. 기본 구현은 비어 있습니다. 이 메서드는 일반적으로 사용자 지정 데이터 처리 코드를 작성하기 위해 재정의하는 메서드입니다.  
  
#### <a name="what-your-custom-code-should-do"></a>사용자 지정 코드로 수행하는 작업  
 다음 메서드를 사용 하 여 출력을 처리 하는 **ScriptMain** 클래스:  
  
-   재정의 **CreateNewOutputRows** 입력된 행을 처리 하기 전에 추가 하 고 채울 수 때 출력 행에만 합니다. 사용할 수는 예를 들어 **CreateNewOutputRows** 호출 해야 소스, 있지만 비동기 출력을 사용 하는 변환에 **AddRow** 중 이나 후 입력된 데이터의 처리 합니다.  
  
-   재정의 **FinishOutputs** 닫기 전에 출력에 작업을 수행 해야 할 경우.  
  
 **PrimeOutput** 메서드를 사용 하면 적절 한 시간에 이러한 메서드를 호출 합니다.  
  
## <a name="postexecute-method"></a>PostExecute 메서드  
 데이터 행의 처리를 시작한 후에만 한 번 수행해야 하는 처리가 있을 때마다 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.PostExecute%2A> 기본 클래스의 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 메서드를 재정의합니다. 예를 들어, 소스, 하려는 닫습니다는 **System.Data.SqlClient.SqlDataReader** 사용 데이터 흐름에 데이터를 로드 합니다.  
  
> [!IMPORTANT]  
>  컬렉션 **ReadWriteVariables** 에서만 사용할 수는 **PostExecute** 메서드. 따라서 각 데이터 행을 처리할 때 패키지 변수의 값을 직접 증분시킬 수 없습니다. 대신 지역 변수의 값이 증가 하 고 패키지 변수의 값에 있는 지역 변수의 값으로 설정 된 **PostExecute** 메서드 후 모든 데이터를 처리 합니다.  
  
## <a name="releaseconnections-method"></a>ReleaseConnections 메서드  
 원본과 대상은 일반적으로 외부 데이터 원본에 연결해야 합니다. <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReleaseConnections%2A> 기본 클래스의 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 메서드를 재정의하여 이전에 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.AcquireConnections%2A> 메서드에서 연 연결을 닫고 해제합니다.  
  
```vb  
    Dim connMgr As IDTSConnectionManager100  
...  
    Public Overrides Sub ReleaseConnections()  
  
        connMgr.ReleaseConnection(sqlConn)  
  
    End Sub  
```  
  
```csharp  
IDTSConnectionManager100 connMgr;  
  
public override void ReleaseConnections()  
{  
  
    connMgr.ReleaseConnection(sqlConn);  
  
}  
```  
  
## <a name="see-also"></a>관련 항목:  
 [스크립트 구성 요소 편집기에서 스크립트 구성 요소 구성](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)   
 [코딩 및 스크립트 구성 요소 디버깅](../../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)  
  
  

