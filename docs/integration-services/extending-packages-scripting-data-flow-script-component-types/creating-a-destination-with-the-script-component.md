---
title: "스크립트 구성 요소를 사용 하 여 대상 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- Script component [Integration Services], destination components
- destinations [Integration Services], components
- input columns [Integration Services]
ms.assetid: 214e22e8-7e7d-4876-b690-c138e5721b81
caps.latest.revision: 57
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 7680aac73590f92eadd615b9d164967e61877664
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="creating-a-destination-with-the-script-component"></a>스크립트 구성 요소를 사용하여 대상 만들기
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지의 데이터 흐름에서 대상 구성 요소를 사용하여 업스트림 원본 및 변환에서 받은 데이터를 데이터 원본에 저장할 수 있습니다. 일반적으로 대상 구성 요소는 기존 연결 관리자를 통해 데이터 원본에 연결합니다.  
  
 스크립트 구성 요소 개요를 참조 하십시오. [Extending the Data Flow with the Script](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)합니다.  
  
 스크립트 구성 요소 및 해당 구성 요소가 생성하는 인프라 코드를 사용하면 사용자 지정 데이터 흐름 구성 요소를 개발하는 과정이 훨씬 간단해집니다. 그러나 스크립트 구성 요소의 작동 방식을 이해 하려면 있습니다 유용할 수의 사용자 지정 데이터 흐름 구성 요소를 개발 하기 위한 단계를 읽을 수는 [사용자 지정 데이터 흐름 구성 요소 개발](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md) 섹션, 특히 [사용자 지정 대상 구성 요소 개발](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md)합니다.  
  
## <a name="getting-started-with-a-destination-component"></a>대상 구성 요소 시작  
 데이터 흐름 탭에 스크립트 구성 요소를 추가 하면 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너는 **스크립트 구성 요소 유형 선택** 대화 상자가 열리고 선택 하 라는 메시지가 표시 된 **소스**, **대상** , 또는 **변환** 스크립트입니다. 이 대화 상자에서 선택 **대상**합니다.  
  
 그런 다음 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 변환의 출력을 대상 구성 요소에 연결합니다. 테스트를 위해 변환하지 않고 원본을 대상에 직접 연결할 수 있습니다.  
  
## <a name="configuring-a-destination-component-in-metadata-design-mode"></a>메타데이터 디자인 모드에서 대상 구성 요소 구성  
 사용 하 여 구성 요소를 구성 하는 대상 구성 요소를 만드는 옵션을 선택한 후는 **스크립트 변환 편집기**합니다. 자세한 내용은 참조 [스크립트 구성 요소 편집기에서 스크립트 구성 요소 구성](../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)합니다.  
  
 설정 스크립트 대상에서 사용할 스크립트 언어를 선택 하려면는 **u a g e** 속성에는 **스크립트** 의 페이지는 **스크립트 변환 편집기** 대화 상자입니다.  
  
> [!NOTE]  
>  스크립트 언어 스크립트 구성 요소에 대 한 기본값을 설정 하려면는 **스크립트 언어** 옵션에 **일반** 의 페이지는 **옵션** 대화 상자. 자세한 내용은 [General Page](https://msdn.microsoft.com/library/ms189436(v=sql.110).aspx)을 참조하세요.  
  
 데이터 흐름 대상 구성 요소에는 하나의 입력이 포함되며 출력은 포함되지 않습니다. 구성 요소가 사용 하 여 메타 데이터 디자인 모드에서 완료 해야 하는 단계 중 하나에 대 한 입력 구성에서 **스크립트 변환 편집기**사용자 지정 스크립트를 작성 하기 전에, 합니다.  
  
### <a name="adding-connection-managers"></a>연결 관리자 추가  
 일반적으로 대상 구성 요소는 기존 연결 관리자를 사용하여 데이터 흐름에서 받은 데이터를 저장할 데이터 원본에 연결합니다. 에 **연결 관리자** 의 페이지는 **스크립트 변환 편집기**, 클릭 **추가** 적절 한 연결 관리자를 추가 합니다.  
  
 그러나 연결 관리자는 단지 특정 유형의 데이터 원본에 연결하는 데 필요한 정보를 캡슐화하고 저장하는 편리한 단위일 뿐입니다. 데이터를 로드하거나 저장하고 데이터 원본에 대한 연결을 열고 닫는 사용자 지정 코드는 사용자가 직접 작성해야 합니다.  
  
 스크립트 구성 요소와 연결 관리자를 사용 하는 방법에 대 한 일반 정보를 참조 하십시오. [스크립트 구성 요소에서 데이터 원본에 연결](../../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md)합니다.  
  
 에 대 한 자세한 내용은 **연결 관리자** 의 페이지는 **스크립트 변환 편집기**, 참조 [스크립트 변환 편집기 &#40; 연결 관리자 페이지 &#41; ](../../integration-services/data-flow/transformations/script-transformation-editor-connection-managers-page.md).  
  
### <a name="configuring-inputs-and-input-columns"></a>입력 및 입력 열 구성  
 대상 구성 요소에는 하나의 입력이 포함되며 출력은 포함되지 않습니다.  
  
 에 **입력 열** 의 페이지는 **스크립트 변환 편집기**, 열 목록 데이터 흐름의 업스트림 구성 요소의 출력에서 사용 가능한 열을 표시 합니다. 이 목록에서 저장할 열을 선택합니다.  
  
 에 대 한 자세한 내용은 **입력 열** 의 페이지는 **스크립트 변환 편집기**, 참조 [스크립트 변환 편집기 &#40; 입력 열 페이지 &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-input-columns-page.md)합니다.  
  
 **입 / 출력** 의 페이지는 **스크립트 변환 편집기** 이름을 바꿀 수는 단일 입력을 보여 줍니다. 스크립트에서는 자동 생성 코드에서 만들어진 접근자 속성을 사용하여 입력을 이름으로 참조합니다.  
  
 에 대 한 자세한 내용은 **입 / 출력** 의 페이지는 **스크립트 변환 편집기**, 참조 [스크립트 변환 편집기 &#40; 입력 및 출력 페이지 &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md)합니다.  
  
### <a name="adding-variables"></a>변수 추가  
 스크립트에서 기존 변수를 사용 하려는 경우에 추가할 수 있습니다는 **ReadOnlyVariables** 및 **ReadWriteVariables** 속성 필드에 **스크립트** 의 페이지는 **스크립트 변환 편집기**합니다.  
  
 속성 필드에 여러 변수를 추가하는 경우 변수 이름을 쉼표로 구분하십시오. 줄임표를 클릭 하 여 여러 변수를 선택할 수도 있습니다 (**...** ) 단추 옆에 **ReadOnlyVariables** 및 **ReadWriteVariables** 속성 필드를 한 다음 변수를 선택 하 고 **변수 선택** 대화 상자입니다.  
  
 스크립트 구성 요소와 변수를 사용 하는 방법에 대 한 일반 정보를 참조 하십시오. [스크립트 구성 요소에서 변수를 사용 하 여](../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md)합니다.  
  
 에 대 한 자세한 내용은 **스크립트** 의 페이지는 **스크립트 변환 편집기**, 참조 [스크립트 변환 편집기 &#40; 스크립트 페이지 &#41; ](../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
## <a name="scripting-a-destination-component-in-code-design-mode"></a>코드 디자인 모드에서 대상 구성 요소 스크립팅  
 구성 요소에 대한 메타데이터를 구성한 후에는 사용자 지정 스크립트를 작성할 수 있습니다. 에 **스크립트 변환 편집기**의 **스크립트** 페이지 **스크립트 편집** 열려는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] VSTA Tools for Applications () IDE 여기서 사용자 지정 스크립트를 추가할 수 있습니다. 사용 하는 스크립팅 언어 선택 여부에 따라 달라 집니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#에 대 한 스크립트 언어로 **u a g e** 속성에는 **스크립트** 페이지입니다.  
  
 모든 종류의 스크립트 구성 요소를 사용 하 여 만든 구성 요소에 적용 되는 중요 한 정보를 참조 하십시오. [코딩 및 스크립트 구성 요소 디버깅](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)합니다.  
  
### <a name="understanding-the-auto-generated-code"></a>자동 생성 코드 이해  
 대상 구성 요소를 편집 가능한 구성과 만들고 구성한 후 VSTA IDE를 열 때 **ScriptMain** 클래스에 대 한 스텁과 함께 코드 편집기에 표시 된 **ProcessInputRow** 메서드. **ScriptMain** 클래스는 사용자 지정 코드를 작성 해야 하 고 **ProcessInputRow** 는 대상 구성 요소에서 가장 중요 한 메서드입니다.  
  
 여는 경우는 **프로젝트 탐색기** VSTA에서 창, 스크립트 구성 요소 읽기 전용 생성도을 확인할 수 있습니다 **BufferWrapper** 및 **ComponentWrapper** 프로젝트 항목입니다. **ScriptMain** 클래스에서 상속 **UserComponent** 클래스에 **ComponentWrapper** 프로젝트 항목입니다.  
  
 런타임 시 데이터 흐름 엔진 호출는 **ProcessInput** 에서 메서드는 **UserComponent** 재정의 하는 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ProcessInput%2A> 의 메서드는 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 부모 클래스입니다. **ProcessInput** 메서드를 차례로 호출 고 입력된 버퍼에서 행을 반복 하는 **ProcessInputRow** 메서드를 각 행에 대해 한 번입니다.  
  
### <a name="writing-your-custom-code"></a>사용자 지정 코드 작성  
 사용자 지정 대상 구성 요소를 만드는 끝나기를 사용할 수 있는 다음 메서드에서 스크립트를 작성 하려는 **ScriptMain** 클래스입니다.  
  
1.  재정의 **AcquireConnections** 메서드 외부 데이터 원본에 연결 합니다. 연결 관리자에서 연결 개체나 필요한 연결 정보를 추출합니다.  
  
2.  재정의 **PreExecute** 메서드 데이터를 저장 하려면 준비를 합니다. 예를 들어를 만들고 구성 경우가 **SqlCommand** 및이 메서드의 해당 매개 변수입니다.  
  
3.  재정의 된를 사용 하 여 **ProcessInputRow** 메서드를 외부 데이터 원본에 각 입력된 행을 복사 합니다. 예는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대상으로 복사할 수 열 값의 매개 변수는 **SqlCommand** 명령을 각 행에 대해 한 번 실행 합니다. 플랫 파일 대상에 대 한 각 열에 대 한 값을 작성할 수 있습니다는 **StreamWriter**, 열 구분 기호로 구분 합니다.  
  
4.  재정의 **PostExecute** 메서드, 필요한 경우 외부 데이터 원본에서 연결을 끊을 하 고 그 밖에 필요한 정리를 수행 합니다.  
  
## <a name="examples"></a>예  
 이 예제에서는 필요한 코드를 보여 줍니다.는 **ScriptMain** 대상 구성 요소를 만드는 클래스입니다.  
  
> [!NOTE]  
>  이러한 예에서 사용 된 **Person.Address** 테이블에 **AdventureWorks** 예제 데이터베이스를 해당 첫 번째 및 네 번째 열을 전달는  **int*AddressID* * * 및 **nvarchar (30) 도시** 데이터 흐름을 통해 열입니다. 이 섹션의 원본, 변환 및 대상 예제에는 동일한 데이터가 사용됩니다. 각 예에 대해 필수 구성 요소 및 가정도 설명되어 있습니다.  
  
### <a name="adonet-destination-example"></a>ADO.NET 대상 예  
 이 예제에서는 기존를 사용 하는 대상 구성 요소를 보여 줍니다. [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자에 데이터 흐름에서 데이터를 저장 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블입니다.  
  
 이 예제 코드를 실행하려면 다음과 같이 패키지와 구성 요소를 구성해야 합니다.  
  
1.  만들기는 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자를 사용 하는 **SqlClient** 공급자에 연결 하는 **AdventureWorks** 데이터베이스입니다.  
  
2.  다음을 실행 하 여 대상 테이블을 만들려면 [!INCLUDE[tsql](../../includes/tsql-md.md)] 명령에 **AdventureWorks** 데이터베이스:  
  
    ```sql
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
3.  데이터 흐름 디자이너 화면에 새 스크립트 구성 요소를 추가하고 이 구성 요소를 대상으로 구성합니다.  
  
4.  업스트림 원본 또는 변환의 출력을 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너의 대상 구성 요소에 연결합니다. 변환하지 않고 원본을 대상에 직접 연결할 수 있습니다. 이 출력 데이터를 제공 해야는 **Person.Address** 목차는 **AdventureWorks** 예제 데이터베이스에 포함 된 적어도 **AddressID** 및  **도시** 열입니다.  
  
5.  열기는 **스크립트 변환 편집기**합니다. 에 **입력 열** 선택 페이지는 **AddressID** 및 **도시** 입력 열입니다.  
  
6.  에 **입 / 출력** 페이지에서 같은 보다 알기 쉬운 이름을 사용 하 여 입력의 이름을 바꿀 **MyAddressInput**합니다.  
  
7.  에 **연결 관리자** 페이지를 추가 하거나 만들고는 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자와 같은 이름 가진 **MyADONETConnectionManager**합니다.  
  
8.  에 **스크립트** 페이지 **스크립트 편집** 뒤에 스크립트를 입력 합니다. 그런 다음 스크립트 개발 환경을 닫습니다.  
  
9. 닫기는 **스크립트 변환 편집기** 해당 샘플을 실행 합니다.  
  
```vb  
Imports System.Data.SqlClient  
...  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Dim connMgr As IDTSConnectionManager100  
    Dim sqlConn As SqlConnection  
    Dim sqlCmd As SqlCommand  
    Dim sqlParam As SqlParameter  
  
    Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
        connMgr = Me.Connections.MyADONETConnectionManager  
        sqlConn = CType(connMgr.AcquireConnection(Nothing), SqlConnection)  
  
    End Sub  
  
    Public Overrides Sub PreExecute()  
  
        sqlCmd = New SqlCommand("INSERT INTO Person.Address2(AddressID, City) " & _  
            "VALUES(@addressid, @city)", sqlConn)  
        sqlParam = New SqlParameter("@addressid", SqlDbType.Int)  
        sqlCmd.Parameters.Add(sqlParam)  
        sqlParam = New SqlParameter("@city", SqlDbType.NVarChar, 30)  
        sqlCmd.Parameters.Add(sqlParam)  
  
    End Sub  
  
    Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
        With sqlCmd  
            .Parameters("@addressid").Value = Row.AddressID  
            .Parameters("@city").Value = Row.City  
            .ExecuteNonQuery()  
        End With  
    End Sub  
  
    Public Overrides Sub ReleaseConnections()  
  
        connMgr.ReleaseConnection(sqlConn)  
  
    End Sub  
  
End Class  
```  
  
```csharp  
using System.Data.SqlClient;  
public class ScriptMain:  
    UserComponent  
  
{  
    IDTSConnectionManager100 connMgr;  
    SqlConnection sqlConn;  
    SqlCommand sqlCmd;  
    SqlParameter sqlParam;  
  
    public override void AcquireConnections(object Transaction)  
    {  
  
        connMgr = this.Connections.MyADONETConnectionManager;  
        sqlConn = (SqlConnection)connMgr.AcquireConnection(null);  
  
    }  
  
    public override void PreExecute()  
    {  
  
        sqlCmd = new SqlCommand("INSERT INTO Person.Address2(AddressID, City) " +  
            "VALUES(@addressid, @city)", sqlConn);  
        sqlParam = new SqlParameter("@addressid", SqlDbType.Int);  
        sqlCmd.Parameters.Add(sqlParam);  
        sqlParam = new SqlParameter("@city", SqlDbType.NVarChar, 30);  
        sqlCmd.Parameters.Add(sqlParam);  
  
    }  
  
    public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
    {  
        {  
            sqlCmd.Parameters["@addressid"].Value = Row.AddressID;  
            sqlCmd.Parameters["@city"].Value = Row.City;  
            sqlCmd.ExecuteNonQuery();  
        }  
    }  
  
    public override void ReleaseConnections()  
    {  
  
        connMgr.ReleaseConnection(sqlConn);  
  
    }  
  
}  
```  
  
### <a name="flat-file-destination-example"></a>플랫 파일 대상의 예  
 이 예에서는 기존 플랫 파일 연결 관리자를 사용하여 데이터 흐름에서 받은 데이터를 플랫 파일에 저장하는 대상 구성 요소를 보여 줍니다.  
  
 이 예제 코드를 실행하려면 다음과 같이 패키지와 구성 요소를 구성해야 합니다.  
  
1.  대상 파일에 연결하는 플랫 파일 연결 관리자를 만듭니다. 대상 파일이 없는 경우에는 대상 구성 요소가 대상 파일을 만듭니다. 대상 파일이 포함 된 쉼표로 구분 된 파일로 구성 된 **AddressID** 및 **도시** 열입니다.  
  
2.  데이터 흐름 디자이너 화면에 새 스크립트 구성 요소를 추가하고 이 구성 요소를 대상으로 구성합니다.  
  
3.  업스트림 원본 또는 변환의 출력을 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너의 대상 구성 요소에 연결합니다. 변환하지 않고 원본을 대상에 직접 연결할 수 있습니다. 이 출력 데이터를 제공 해야는 **Person.Address** 목차는 **AdventureWorks** 예제 데이터베이스를 포함 해야 하 고 최소한 **AddressID** 및 **도시** 열입니다.  
  
4.  열기는 **스크립트 변환 편집기**합니다. 에 **입력 열** 선택 페이지는 **AddressID** 및 **도시** 열입니다.  
  
5.  에 **입 / 출력** 페이지에서 같은 보다 알기 쉬운 이름으로 입력의 이름을 바꿀 **MyAddressInput**합니다.  
  
6.  에 **연결 관리자** 페이지를 추가 하거나 플랫 파일 연결 관리자 설명적인 이름으로 같은 만들 **MyFlatFileDestConnectionManager**합니다.  
  
7.  에 **스크립트** 페이지 **스크립트 편집** 뒤에 스크립트를 입력 합니다. 그런 다음 스크립트 개발 환경을 닫습니다.  
  
8.  닫기는 **스크립트 변환 편집기** 해당 샘플을 실행 합니다.  
  
```vb  
Imports System.IO  
...  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Dim copiedAddressFile As String  
    Private textWriter As StreamWriter  
    Private columnDelimiter As String = ","  
  
    Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
        Dim connMgr As IDTSConnectionManager100 = _  
            Me.Connections.MyFlatFileDestConnectionManager  
        copiedAddressFile = CType(connMgr.AcquireConnection(Nothing), String)  
  
    End Sub  
  
    Public Overrides Sub PreExecute()  
  
        textWriter = New StreamWriter(copiedAddressFile, False)  
  
    End Sub  
  
    Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
  
        With textWriter  
            If Not Row.AddressID_IsNull Then  
                .Write(Row.AddressID)  
            End If  
            .Write(columnDelimiter)  
            If Not Row.City_IsNull Then  
                .Write(Row.City)  
            End If  
            .WriteLine()  
        End With  
  
    End Sub  
  
    Public Overrides Sub PostExecute()  
  
        textWriter.Close()  
  
    End Sub  
  
End Class  
```  
  
```csharp  
using System.IO;  
public class ScriptMain:  
    UserComponent  
  
{  
    string copiedAddressFile;  
    private StreamWriter textWriter;  
    private string columnDelimiter = ",";  
  
    public override void AcquireConnections(object Transaction)  
    {  
  
        IDTSConnectionManager100 connMgr = this.Connections.MyFlatFileDestConnectionManager;  
        copiedAddressFile = (string) connMgr.AcquireConnection(null);  
  
    }  
  
    public override void PreExecute()  
    {  
  
        textWriter = new StreamWriter(copiedAddressFile, false);  
  
    }  
  
    public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
    {  
  
        {  
            if (!Row.AddressID_IsNull)  
            {  
                textWriter.Write(Row.AddressID);  
            }  
            textWriter.Write(columnDelimiter);  
            if (!Row.City_IsNull)  
            {  
                textWriter.Write(Row.City);  
            }  
            textWriter.WriteLine();  
        }  
  
    }  
  
    public override void PostExecute()  
    {  
  
        textWriter.Close();  
  
    }  
  
}  
```  
  
## <a name="see-also"></a>관련 항목:  
 [스크립트 구성 요소를 사용 하 여 원본 만들기](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-source-with-the-script-component.md)   
 [사용자 지정 대상 구성 요소 개발](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md)  
  
  

