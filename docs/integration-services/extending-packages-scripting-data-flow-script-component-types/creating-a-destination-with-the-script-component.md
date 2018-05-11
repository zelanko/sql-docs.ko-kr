---
title: 스크립트 구성 요소를 사용하여 대상 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: extending-packages-scripting-data-flow-script-component-types
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
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
manager: craigg
ms.openlocfilehash: 36effe6bcb6ffc2e6b5045e25640cdc96a76447f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="creating-a-destination-with-the-script-component"></a>스크립트 구성 요소를 사용하여 대상 만들기
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지의 데이터 흐름에서 대상 구성 요소를 사용하여 업스트림 원본 및 변환에서 받은 데이터를 데이터 원본에 저장할 수 있습니다. 일반적으로 대상 구성 요소는 기존 연결 관리자를 통해 데이터 원본에 연결합니다.  
  
 스크립트 구성 요소에 대한 개요는 [스크립트 구성 요소를 사용하여 데이터 흐름 확장](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)을 참조하세요.  
  
 스크립트 구성 요소 및 해당 구성 요소가 생성하는 인프라 코드를 사용하면 사용자 지정 데이터 흐름 구성 요소를 개발하는 과정이 훨씬 간단해집니다. 그러나 스크립트 구성 요소의 작동 방식을 이해하려면 [사용자 지정 데이터 흐름 구성 요소 개발](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md) 섹션, 특히 [사용자 지정 대상 구성 요소 개발](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md)에서 사용자 지정 데이터 흐름 구성 요소를 개발하는 단계를 파악하는 것이 유용할 수 있습니다.  
  
## <a name="getting-started-with-a-destination-component"></a>대상 구성 요소 시작  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너의 [데이터 흐름] 탭에 스크립트 구성 요소를 추가하면, **스크립트 구성 요소 유형 선택** 대화 상자가 열려 **원본**, **대상** 또는 **변환** 스크립트를 선택하도록 요구합니다. 이 대화 상자에서 **대상**을 선택합니다.  
  
 그런 다음 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 변환의 출력을 대상 구성 요소에 연결합니다. 테스트를 위해 변환하지 않고 원본을 대상에 직접 연결할 수 있습니다.  
  
## <a name="configuring-a-destination-component-in-metadata-design-mode"></a>메타데이터 디자인 모드에서 대상 구성 요소 구성  
 대상 구성 요소를 만드는 옵션을 선택한 후 **스크립트 변환 편집기**를 사용하여 구성 요소를 구성합니다. 자세한 내용은 [스크립트 구성 요소 편집기에서 스크립트 구성 요소 구성](../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)을 참조하세요.  
  
 스크립트 대상에서 사용할 스크립트 언어를 선택하려면 **스크립트 변환 편집기** 대화 상자의 **스크립트** 페이지에서 **ScriptLanguage** 속성을 설정합니다.  
  
> [!NOTE]  
>  스크립트 구성 요소에 대한 기본 스크립트 언어를 설정하려면 **옵션** 대화 상자의 **일반** 페이지에서 **스크립트 언어** 옵션을 사용합니다. 자세한 내용은 [General Page](https://msdn.microsoft.com/library/ms189436(v=sql.110).aspx)을 참조하세요.  
  
 데이터 흐름 대상 구성 요소에는 하나의 입력이 포함되며 출력은 포함되지 않습니다. 구성 요소에 대한 입력 구성은 사용자 지정 스크립트를 작성하기 전에 **스크립트 변환 편집기**를 사용하여 메타데이터 디자인 모드에서 완료해야 하는 단계 중 하나입니다.  
  
### <a name="adding-connection-managers"></a>연결 관리자 추가  
 일반적으로 대상 구성 요소는 기존 연결 관리자를 사용하여 데이터 흐름에서 받은 데이터를 저장할 데이터 원본에 연결합니다. **스크립트 변환 편집기**의 **연결 관리자** 페이지에서 **추가**를 클릭하여 적절한 연결 관리자를 추가합니다.  
  
 그러나 연결 관리자는 단지 특정 유형의 데이터 원본에 연결하는 데 필요한 정보를 캡슐화하고 저장하는 편리한 단위일 뿐입니다. 데이터를 로드하거나 저장하고 데이터 원본에 대한 연결을 열고 닫는 사용자 지정 코드는 사용자가 직접 작성해야 합니다.  
  
 스크립트 구성 요소에서 연결 관리자를 사용하는 방법에 대한 일반적은 내용은 [스크립트 구성 요소에서 데이터 원본에 연결](../../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md)을 참조하세요.  
  
 **스크립트 변환 편집기**의 **연결 관리자** 페이지에 대한 자세한 내용은 [스크립트 변환 편집기&#40;연결 관리자 페이지&#41;](../../integration-services/data-flow/transformations/script-transformation-editor-connection-managers-page.md)를 참조하세요.  
  
### <a name="configuring-inputs-and-input-columns"></a>입력 및 입력 열 구성  
 대상 구성 요소에는 하나의 입력이 포함되며 출력은 포함되지 않습니다.  
  
 **스크립트 변환 편집기**의 **입력 열** 페이지에서 열 목록에는 데이터 흐름에 있는 업스트림 구성 요소의 출력에서 사용 가능한 열이 표시됩니다. 이 목록에서 저장할 열을 선택합니다.  
  
 **스크립트 변환 편집기**의 **입력 열** 페이지에 대한 자세한 내용은 [스크립트 변환 편집기&#40;입력 열 페이지&#41;](../../integration-services/data-flow/transformations/script-transformation-editor-input-columns-page.md)를 참조하세요.  
  
 **스크립트 변환 편집기**의 **입/출력** 페이지에는 이름을 바꿀 수 있는 단일 입력이 표시됩니다. 스크립트에서는 자동 생성 코드에서 만들어진 접근자 속성을 사용하여 입력을 이름으로 참조합니다.  
  
 **스크립트 변환 편집기**의 **입/출력** 페이지에 대한 자세한 내용은 [스크립트 변환 편집기&#40;입/출력 페이지&#41;](../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md)를 참조하세요.  
  
### <a name="adding-variables"></a>변수 추가  
 스크립트에서 기존 변수를 사용하려는 경우 **스크립트 변환 편집기**의 **스크립트** 페이지에 있는 **ReadOnlyVariables** 및 **ReadWriteVariables** 속성 필드에서 해당 변수를 추가할 수 있습니다.  
  
 속성 필드에 여러 변수를 추가하는 경우 변수 이름을 쉼표로 구분하십시오. **ReadOnlyVariables** 및 **ReadWriteVariables** 속성 필드 옆에 있는 줄임표(**…**) 단추를 클릭한 다음 **변수 선택** 대화 상자에서 여러 개의 변수를 선택할 수도 있습니다.  
  
 스크립트 구성 요소에서 변수를 사용하는 방법에 대한 일반적인 내용은 [스크립트 구성 요소에서 변수 사용](../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md)을 참조하세요.  
  
 **스크립트 변환 편집기**의 **스크립트** 페이지에 대한 자세한 내용은 [스크립트 변환 편집기&#40;스크립트 페이지&#41;](../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md)를 참조하세요.  
  
## <a name="scripting-a-destination-component-in-code-design-mode"></a>코드 디자인 모드에서 대상 구성 요소 스크립팅  
 구성 요소에 대한 메타데이터를 구성한 후에는 사용자 지정 스크립트를 작성할 수 있습니다. **스크립트 변환 편집기**의 **스크립트** 페이지에서 **스크립트 편집**을 클릭하여 사용자 지정 스크립트를 추가할 수 있는 VSTA([!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications) IDE를 엽니다. 사용하는 스크립트 언어는 **스크립트** 페이지에서 **ScriptLanguage** 속성에 대한 스크립트 언어로 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# 중에서 선택한 언어에 따라 달라집니다.  
  
 스크립트 구성 요소를 사용하여 만든 모든 종류의 구성 요소에 적용되는 중요한 정보는 [스크립트 구성 요소 코딩 및 디버깅](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)을 참조하세요.  
  
### <a name="understanding-the-auto-generated-code"></a>자동 생성 코드 이해  
 대상 구성 요소를 만들고 구성한 후 VSTA IDE를 열면, 편집 가능한 **ScriptMain** 클래스가 **ProcessInputRow** 메서드에 대한 스텁과 함께 코드 편집기에 표시됩니다. **ScriptMain** 클래스는 사용자 지정 코드를 작성하는 위치이며, **ProcessInputRow**는 대상 구성 요소에서 가장 중요한 메서드입니다.  
  
 VSTA에서 **프로젝트 탐색기** 창을 열면 스크립트 구성 요소에서 읽기 전용 **BufferWrapper** 및 **ComponentWrapper** 프로젝트 항목도 생성했음을 확인할 수 있습니다. **ScriptMain** 클래스는 **ComponentWrapper** 프로젝트 항목의 **UserComponent** 클래스에서 상속됩니다.  
  
 런타임에 데이터 흐름 엔진에서 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 부모 클래스의 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ProcessInput%2A> 메서드를 재정의하는 **UserComponent** 클래스의 **ProcessInput** 메서드를 호출합니다. 그러면 **ProcessInput** 메서드에서 입력 버퍼의 행을 반복하고 각 행에 대해 **ProcessInputRow** 메서드를 한 번씩 호출합니다.  
  
### <a name="writing-your-custom-code"></a>사용자 지정 코드 작성  
 사용자 지정 대상 구성 요소 만들기를 완료하려면 **ScriptMain** 클래스에서 사용할 수 있는 다음 메서드에 스크립트를 작성해야 합니다.  
  
1.  외부 데이터 원본에 연결하도록 **AcquireConnections** 메서드를 재정의합니다. 연결 관리자에서 연결 개체나 필요한 연결 정보를 추출합니다.  
  
2.  데이터 저장을 준비하도록 **PreExecute** 메서드를 재정의합니다. 예를 들어 이 메서드에 **SqlCommand** 및 해당 매개 변수를 만들고 구성할 수 있습니다.  
  
3.  재정의된 **ProcessInputRow** 메서드를 사용하여 각 입력 행을 외부 데이터 원본에 복사합니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대상의 경우 열 값을 **SqlCommand**의 매개 변수에 복사하고 각 행에 대해 이 명령을 한 번씩 실행할 수 있습니다. 플랫 파일 대상의 경우 각 열의 값을 열 구분 기호로 구분하여 **StreamWriter**에 쓸 수 있습니다.  
  
4.  필요한 경우 외부 데이터 원본과의 연결을 끊고 필요한 다른 모든 정리 작업을 수행하도록 **PostExecute** 메서드를 재정의합니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 **ScriptMain** 클래스에서 대상 구성 요소를 만드는 데 필요한 코드를 보여 줍니다.  
  
> [!NOTE]  
>  이 예제에서는 **AdventureWorks** 샘플 데이터베이스의 **Person.Address** 테이블을 사용하고, 이 테이블의 첫 번째 및 네 번째 열인 **int*AddressID*** 및 **nvarchar(30)City**를 데이터 흐름을 통해 전달합니다. 이 섹션의 원본, 변환 및 대상 예제에는 동일한 데이터가 사용됩니다. 각 예에 대해 필수 구성 요소 및 가정도 설명되어 있습니다.  
  
### <a name="adonet-destination-example"></a>ADO.NET 대상 예  
 이 예제에서는 기존 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자를 사용하여 데이터 흐름의 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 저장하는 대상 구성 요소를 보여 줍니다.  
  
 이 예제 코드를 실행하려면 다음과 같이 패키지와 구성 요소를 구성해야 합니다.  
  
1.  **SqlClient** 공급자를 사용하여 **AdventureWorks** 데이터베이스에 연결하는 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자를 만듭니다.  
  
2.  **AdventureWorks** 데이터베이스에서 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 명령을 실행하여 대상 테이블을 만듭니다.  
  
    ```sql
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
3.  데이터 흐름 디자이너 화면에 새 스크립트 구성 요소를 추가하고 이 구성 요소를 대상으로 구성합니다.  
  
4.  업스트림 원본 또는 변환의 출력을 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너의 대상 구성 요소에 연결합니다. 변환하지 않고 원본을 대상에 직접 연결할 수 있습니다. 이 출력은 **AdventureWorks** 샘플 데이터베이스에 있는 **Person.Address** 테이블의 데이터를 제공해야 하며, 이 데이터에는 적어도 **AddressID** 및 **City** 열이 포함됩니다.  
  
5.  **스크립트 변환 편집기**를 엽니다. **입력 열** 페이지에서 **AddressID** 및 **City** 입력 열을 선택합니다.  
  
6.  **입/출력** 페이지에서 입력의 이름을 **MyAddressInput**과 같이 더 알기 쉬운 이름으로 바꿉니다.  
  
7.  **연결 관리자** 페이지에서 **MyADONETConnectionManager**와 같은 이름으로 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자를 추가하거나 만듭니다.  
  
8.  **스크립트** 페이지에서 **스크립트 편집**을 클릭하고 다음 스크립트를 입력합니다. 그런 다음 스크립트 개발 환경을 닫습니다.  
  
9. **스크립트 변환 편집기**를 닫고 샘플을 실행합니다.  
  
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
  
1.  대상 파일에 연결하는 플랫 파일 연결 관리자를 만듭니다. 대상 파일이 없는 경우에는 대상 구성 요소가 대상 파일을 만듭니다. 대상 파일을 **AddressID** 및 **City** 열이 포함되고 쉼표로 구분된 파일로 구성합니다.  
  
2.  데이터 흐름 디자이너 화면에 새 스크립트 구성 요소를 추가하고 이 구성 요소를 대상으로 구성합니다.  
  
3.  업스트림 원본 또는 변환의 출력을 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너의 대상 구성 요소에 연결합니다. 변환하지 않고 원본을 대상에 직접 연결할 수 있습니다. 이 출력은 **AdventureWorks** 샘플 데이터베이스에 있는 **Person.Address** 테이블의 데이터를 제공해야 하며, 이 데이터에는 적어도 **AddressID** 및 **City** 열이 포함되어야 합니다.  
  
4.  **스크립트 변환 편집기**를 엽니다. **입력 열** 페이지에서 **AddressID** 및 **City** 열을 선택합니다.  
  
5.  **입/출력** 페이지에서 입력의 이름을 **MyAddressInput**과 같이 더 알기 쉬운 이름으로 바꿉니다.  
  
6.  **연결 관리자** 페이지에서 **MyFlatFileDestConnectionManager**와 같이 알기 쉬운 이름으로 플랫 파일 연결 관리자를 추가하거나 만듭니다.  
  
7.  **스크립트** 페이지에서 **스크립트 편집**을 클릭하고 다음 스크립트를 입력합니다. 그런 다음 스크립트 개발 환경을 닫습니다.  
  
8.  **스크립트 변환 편집기**를 닫고 샘플을 실행합니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [스크립트 구성 요소를 사용하여 원본 만들기](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-source-with-the-script-component.md)   
 [사용자 지정 대상 구성 요소 개발](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md)  
  
  
