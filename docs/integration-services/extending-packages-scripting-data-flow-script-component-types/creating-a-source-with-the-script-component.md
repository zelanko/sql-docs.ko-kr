---
title: "스크립트 구성 요소를 사용 하 여 원본 만들기 | Microsoft Docs"
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
- Script component [Integration Services], source components
- output columns [Integration Services]
- sources [Integration Services], components
ms.assetid: 547c4179-ea82-4265-8c6f-04a2aa77a3c0
caps.latest.revision: 59
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d4944c3d5752da21fed90f16a38a33b4fad41515
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="creating-a-source-with-the-script-component"></a>스크립트 구성 요소를 사용하여 원본 만들기
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지의 데이터 흐름에서 원본 구성 요소를 사용하여 데이터 원본의 데이터를 로드하고 다운스트림 변환 및 대상에 전달할 수 있습니다. 일반적으로 데이터 원본에 연결하는 데는 기존 연결 관리자를 사용합니다.  
  
 스크립트 구성 요소 개요를 참조 하십시오. [Extending the Data Flow with the Script](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)합니다.  
  
 스크립트 구성 요소 및 해당 구성 요소가 생성하는 인프라 코드를 사용하면 사용자 지정 데이터 흐름 구성 요소를 개발하는 과정이 훨씬 간단해집니다. 하지만 스크립트 구성 요소의 작동 방식을 이해하려면 사용자 지정 데이터 흐름 구성 요소를 개발하는 데 필요한 단계를 파악하는 것이 좋습니다. 섹션을 참조 [사용자 지정 데이터 흐름 구성 요소 개발](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md), 특히 [사용자 지정 원본 구성 요소 개발](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md)합니다.  
  
## <a name="getting-started-with-a-source-component"></a>원본 구성 요소 시작  
 데이터 흐름 창에 스크립트 구성 요소를 추가 하면 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너는 **스크립트 구성 요소 유형 선택** 대화 상자가 열리고 원본, 대상 또는 변환 스크립트를 선택 하 라는 메시지가 표시 됩니다. 이 대화 상자에서 선택 **소스**합니다.  
  
## <a name="configuring-a-source-component-in-metadata-design-mode"></a>메타데이터 디자인 모드에서 원본 구성 요소 구성  
 원본 구성 요소를 만들려면을 선택한 다음 구성 요소가 사용 하 여 구성한는 **스크립트 변환 편집기**합니다. 자세한 내용은 참조 [스크립트 구성 요소 편집기에서 스크립트 구성 요소 구성](../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)합니다.  
  
 데이터 흐름 원본 구성 요소는 입력을 사용하지 않으며 하나 이상의 출력을 지원합니다. 구성 요소를 사용 하 여 메타 데이터 디자인 모드에서 완료 해야 하는 단계 중 하나에 대 한 출력을 구성 된 **스크립트 변환 편집기**사용자 지정 스크립트를 작성 하기 전에, 합니다.  
  
 설정 하 여 스크립트 언어를 지정할 수도 있습니다는 **u a g e** 속성에는 **스크립트** 의 페이지는 **스크립트 변환 편집기**합니다.  
  
> [!NOTE]  
>  스크립트 구성 요소 및 스크립트 태스크에 대 한 기본 스크립트 언어를 설정 하려면는 **스크립트 언어** 옵션에 **일반** 의 페이지는 **옵션** 대화 상자. 자세한 내용은 [General Page](~/integration-services/control-flow/script-task-editor-general-page.md)을 참조하세요.  
  
### <a name="adding-connection-managers"></a>연결 관리자 추가  
 일반적으로 원본 구성 요소는 기존 연결 관리자를 사용하여 데이터 흐름으로 로드할 데이터가 있는 데이터 원본에 연결합니다. 에 **연결 관리자** 의 페이지는 **스크립트 변환 편집기**, 클릭 **추가** 적절 한 연결 관리자를 추가 합니다.  
  
 그러나 연결 관리자는 단지 특정 유형의 데이터 원본에 연결하는 데 필요한 정보를 캡슐화하고 저장하는 편리한 단위일 뿐입니다. 데이터를 로드하거나 저장하고 또한 데이터 원본에 대한 연결을 열고 닫는 사용자 지정 코드는 개발자가 직접 작성해야 합니다.  
  
 스크립트 구성 요소와 연결 관리자를 사용 하는 방법에 대 한 일반 정보를 참조 하십시오. [스크립트 구성 요소에서 데이터 원본에 연결](../../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md)합니다.  
  
 에 대 한 자세한 내용은 **연결 관리자** 의 페이지는 **스크립트 변환 편집기**, 참조 [스크립트 변환 편집기 &#40; 연결 관리자 페이지 &#41; ](../../integration-services/data-flow/transformations/script-transformation-editor-connection-managers-page.md).  
  
### <a name="configuring-outputs-and-output-columns"></a>출력 및 출력 열 구성  
 원본 구성 요소는 입력을 사용하지 않으며 하나 이상의 출력을 지원합니다. 에 **입 / 출력** 의 페이지는 **스크립트 변환 편집기**, 기본적으로 단일 출력이 생성 되었지만 생성 된 출력 열이 없습니다. 편집기의 이 페이지에서 다음과 같은 항목을 구성할 수 있습니다.  
  
-   각 출력에 대해 수동으로 출력 열을 추가하고 구성해야 합니다. 각 출력에 대 한 출력 열 폴더 선택 하 고 사용 하 여는 **열 추가** 및 **열 제거** 각 출력의 원본 구성 요소에 대 한 출력 열을 관리 하는 단추입니다. 나중에 스크립트에서는 자동 생성 코드에서 만들어진 형식화된 접근자 속성을 사용하여 출력을 여기에서 할당한 이름으로 참조합니다.  
  
-   예기치 않은 값이 포함된 행에 대한 시뮬레이션된 오류 출력과 같은 추가 출력을 하나 이상 만들 수 있습니다. 사용 하 여는 **출력 추가** 및 **출력 제거** 원본 구성 요소 출력을 관리 하는 단추입니다. 모든 입력된 행에 대 한 동일한 0이 아닌 값을 지정 하지 않으면 사용 가능한 모든 출력으로 전송 됩니다는 **ExclusionGroup** 각 행을 동일한 공유 하는 출력 중 하나로 전송 하려는 속성 **ExclusionGroup** 값입니다. 식별 하기 위해 선택한 특정 정수 값의 **ExclusionGroup** 는 중요 하지 않습니다.  
  
    > [!NOTE]  
    >  0이 아닌를 사용할 수도 있습니다 **ExclusionGroup** 모든 행을 출력 하지 않을 경우 단일 출력과 함께 속성 값입니다. 그러나이 경우 명시적으로 호출 해야는 **DirectRowTo\<outputbuffer >** 메서드 출력으로 전송 하려는 경우 각 행에 대 한 합니다.  
  
-   출력에 이름을 지정할 수 있습니다. 나중에 스크립트에서는 자동 생성 코드에서 만들어진 형식화된 접근자 속성을 사용하여 출력을 이름으로 참조합니다.  
  
-   일반적으로 여러 출력에 동일한 **ExclusionGroup** 동일한 출력 열이 있어야 합니다. 그러나 시뮬레이션된 오류 출력을 만드는 경우 오류 정보를 저장할 다른 열을 추가할 수 있습니다. 오류 행을 처리 하는 데이터 흐름 엔진이 하는 방법에 대 한 정보를 참조 [데이터 흐름 구성 요소의 오류 출력을 사용 하 여](../../integration-services/extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)합니다. 그러나 스크립트 구성 요소에서는 개발자가 직접 코드를 작성하여 추가 열을 적절한 오류 정보로 채워야 합니다. 자세한 내용은 참조 [스크립트 구성 요소에 대 한 오류 출력 시뮬레이션](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md)합니다.  
  
 에 대 한 자세한 내용은 **입 / 출력** 의 페이지는 **스크립트 변환 편집기**, 참조 [스크립트 변환 편집기 &#40; 입력 및 출력 페이지 &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md)합니다.  
  
### <a name="adding-variables"></a>변수 추가  
 스크립트에서 사용 하려는 값을 가진 모든 기존 변수가 없으면에 추가할 수 있습니다는 **ReadOnlyVariables** 및 **ReadWriteVariables** 속성 필드에 **스크립트** 의 페이지는 **스크립트 변환 편집기**합니다.  
  
 속성 필드에 여러 변수를 입력하는 경우 변수 이름을 쉼표로 구분합니다. 줄임표를 클릭 하 여 여러 변수를 입력할 수도 있습니다 (**...** ) 단추 옆에 **ReadOnlyVariables** 및 **ReadWriteVariables** 속성 필드에 변수를 선택 하 고 **변수 선택** 대화 상자 .  
  
 스크립트 구성 요소와 변수를 사용 하는 방법에 대 한 일반 정보를 참조 하십시오. [스크립트 구성 요소에서 변수를 사용 하 여](../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md)합니다.  
  
 에 대 한 자세한 내용은 **스크립트** 의 페이지는 **스크립트 변환 편집기**, 참조 [스크립트 변환 편집기 &#40; 스크립트 페이지 &#41; ](../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
## <a name="scripting-a-source-component-in-code-design-mode"></a>코드 디자인 모드에서 원본 구성 요소 스크립팅  
 구성 요소에 대 한 메타 데이터를 구성한 후에 열은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] VSTA Tools for Applications () 사용자 지정 스크립트를 코딩 하는 IDE. VSTA를 열려면 **스크립트 편집** 에 **스크립트** 의 페이지는 **스크립트 변환 편집기**합니다. 사용 하 여 스크립트를 작성할 수 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#에서 선택한 스크립트 언어에 따라는 **u a g e** 속성입니다.  
  
 모든 종류의 스크립트 구성 요소를 사용 하 여 만든 구성 요소에 적용 되는 중요 한 정보를 참조 하십시오. [코딩 및 스크립트 구성 요소 디버깅](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)합니다.  
  
### <a name="understanding-the-auto-generated-code"></a>자동 생성 코드 이해  
 만들고 원본 구성 요소를 편집 가능한를 구성한 후 VSTA IDE를 열면 **ScriptMain** 클래스가 코드 편집기에 표시 합니다. 사용자 지정 코드를 작성할는 **ScriptMain** 클래스입니다.  
  
 **ScriptMain** 클래스에 대 한 스텁을 포함 된 **CreateNewOutputRows** 메서드. **CreateNewOutputRows** 는 원본 구성 요소에서 가장 중요 한 메서드입니다.  
  
 여는 경우는 **프로젝트 탐색기** VSTA에서 창, 스크립트 구성 요소 읽기 전용 생성도을 확인할 수 있습니다 **BufferWrapper** 및 **ComponentWrapper** 프로젝트 항목입니다. **ScriptMain** 클래스에서 상속 **UserComponent** 클래스에 **ComponentWrapper** 프로젝트 항목입니다.  
  
 런타임 시 데이터 흐름 엔진 호출는 **PrimeOutput** 에서 메서드는 **UserComponent** 재정의 하는 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.PrimeOutput%2A> 의 메서드는 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 부모 클래스입니다. **PrimeOutput** 메서드 호출 하 여 다음 방법:  
  
1.  **CreateNewOutputRows** 에서 무시 하는 메서드를 **ScriptMain** 처음에 빈 이러한 버퍼에 행을 추가할 데이터 원본에서 출력 합니다.  
  
2.  **FinishOutputs** 메서드를 기본적으로 비어 있습니다. 이 메서드를 재정의 **ScriptMain** 출력을 완료 하는 데 필요한 처리를 수행할 수 있습니다.  
  
3.  개인 **MarkOutputsAsFinished** 메서드를 호출 하는 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer.SetEndOfRowset%2A> 의 메서드는 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> 부모 클래스 여 출력이 끝났음을 데이터 흐름 엔진에 알립니다. 호출할 필요가 없습니다 **SetEndOfRowset** 사용자 코드에서 명시적으로 합니다.  
  
### <a name="writing-your-custom-code"></a>사용자 지정 코드 작성  
 사용자 지정 원본 구성 요소를 만드는 끝나기를 사용할 수 있는 다음 메서드에서 스크립트를 작성 하려는 **ScriptMain** 클래스입니다.  
  
1.  재정의 **AcquireConnections** 메서드 외부 데이터 원본에 연결 합니다. 연결 관리자에서 연결 개체나 필요한 연결 정보를 추출합니다.  
  
2.  재정의 **PreExecute** 메서드를 한 번에 모든 원본 데이터를 로드할 수 있는 경우 데이터를 로드 합니다. 예를 들어 실행할 수 있습니다는 **SqlCommand** 에 대해는 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결을 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 동시에 모든 원본 데이터를 로드 하 고 데이터베이스는 **SqlDataReader**합니다. 행을 반복할 때 데이터를 로드할 수 (예: 텍스트 파일을 읽을 때) 한 번에 한 행씩 원본 데이터를 로드 해야 **CreateNewOutputRows**합니다.  
  
3.  재정의 된를 사용 하 여 **CreateNewOutputRows** 메서드 빈 출력 버퍼에 새 행을 추가 하 고 새 출력 행에 있는 각 열의 값을 입력 합니다. 사용 하 여는 **AddRow** 메서드의 각 출력 버퍼를 빈 새 행을 추가 하 고 각 열의 값을 설정 합니다. 일반적으로는 외부 원본에서 로드된 열의 값을 복사합니다.  
  
4.  재정의 **PostExecute** 메서드 데이터를 처리 합니다. 예를 들어 닫을 수 있습니다는 **SqlDataReader** 사용 하 여 데이터 로드를 합니다.  
  
5.  재정의 **ReleaseConnections** 메서드를 필요한 경우 외부 데이터 원본에서 연결을 끊습니다.  
  
## <a name="examples"></a>예  
 다음 예제에 필요한 사용자 지정 코드를 보여 줍니다.는 **ScriptMain** 원본 구성 요소를 만드는 클래스입니다.  
  
> [!NOTE]  
>  이러한 예에서 사용 된 **Person.Address** 테이블에 **AdventureWorks** 예제 데이터베이스를 해당 첫 번째 및 네 번째 열을 전달는 **intAddressID** 및  **nvarchar (30) 도시** 데이터 흐름을 통해 열입니다. 이 섹션의 원본, 변환 및 대상 예제에는 동일한 데이터가 사용됩니다. 각 예에 대해 필수 구성 요소 및 가정도 설명되어 있습니다.  
  
### <a name="adonet-source-example"></a>ADO.NET 원본 예  
 이 예제에서는 기존를 사용 하는 원본 구성 요소를 보여 줍니다. [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자에서 데이터를 로드 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 흐름에는 테이블입니다.  
  
 이 예제 코드를 실행하려면 다음과 같이 패키지와 구성 요소를 구성해야 합니다.  
  
1.  만들기는 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자를 사용 하는 **SqlClient** 공급자에 연결 하는 **AdventureWorks** 데이터베이스입니다.  
  
2.  데이터 흐름 디자이너 화면에 새 스크립트 구성 요소를 추가하고 이 구성 요소를 원본으로 구성합니다.  
  
3.  열기는 **스크립트 변환 편집기**합니다. 에 **입 / 출력** 페이지에서 기본와 같은 보다 알기 쉬운 이름으로 출력의 이름을 **MyAddressOutput**, 추가 및 두 개의 출력 열을 구성 하 고 **AddressID**및 **도시**합니다.  
  
    > [!NOTE]  
    >  데이터 형식을 변경 하는 **도시** DT_WSTR로 출력 열입니다.  
  
4.  에 **연결 관리자** 페이지를 추가 하거나 만들고는 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자 이름 지정 등 및 **MyADONETConnection**합니다.  
  
5.  에 **스크립트** 페이지 **스크립트 편집** 뒤에 스크립트를 입력 합니다. 다음 스크립트 개발 환경을 닫습니다 및 **스크립트 변환 편집기**합니다.  
  
6.  만들기 및 대상 구성 요소와 같은 구성는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대상 또는에서 보여 준 예제 대상 구성 요소 [스크립트 구성 요소를 사용 하 여 대상 만들기](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md), 예상 되는  **AddressID** 및 **도시** 열입니다. 그런 다음 원본 구성 요소를 대상에 연결합니다. 변환하지 않고 원본을 대상에 직접 연결할 수 있습니다. 다음 명령을 실행 하 여 대상 테이블을 만들 수 있습니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] 명령에 **AdventureWorks** 데이터베이스:  
  
    ```sql
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
7.  예제를 실행합니다.  
  
    ```vb  
    Imports System.Data.SqlClient  
    ...  
    Public Class ScriptMain  
        Inherits UserComponent  
  
        Dim connMgr As IDTSConnectionManager100  
        Dim sqlConn As SqlConnection  
        Dim sqlReader As SqlDataReader  
  
        Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
            connMgr = Me.Connections.MyADONETConnection  
            sqlConn = CType(connMgr.AcquireConnection(Nothing), SqlConnection)  
  
        End Sub  
  
        Public Overrides Sub PreExecute()  
  
            Dim cmd As New SqlCommand("SELECT AddressID, City, StateProvinceID FROM Person.Address", sqlConn)  
            sqlReader = cmd.ExecuteReader  
  
        End Sub  
  
        Public Overrides Sub CreateNewOutputRows()  
  
            Do While sqlReader.Read  
                With MyAddressOutputBuffer  
                    .AddRow()  
                    .AddressID = sqlReader.GetInt32(0)  
                    .City = sqlReader.GetString(1)  
                End With  
            Loop  
  
        End Sub  
  
        Public Overrides Sub PostExecute()  
  
            sqlReader.Close()  
  
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
        SqlDataReader sqlReader;  
  
        public override void AcquireConnections(object Transaction)  
        {  
            connMgr = this.Connections.MyADONETConnection;  
            sqlConn = (SqlConnection)connMgr.AcquireConnection(null);  
  
        }  
  
        public override void PreExecute()  
        {  
  
            SqlCommand cmd = new SqlCommand("SELECT AddressID, City, StateProvinceID FROM Person.Address", sqlConn);  
            sqlReader = cmd.ExecuteReader();  
  
        }  
  
        public override void CreateNewOutputRows()  
        {  
  
            while (sqlReader.Read())  
            {  
                {  
                    MyAddressOutputBuffer.AddRow();  
                    MyAddressOutputBuffer.AddressID = sqlReader.GetInt32(0);  
                    MyAddressOutputBuffer.City = sqlReader.GetString(1);  
                }  
            }  
  
        }  
  
        public override void PostExecute()  
        {  
  
            sqlReader.Close();  
  
        }  
  
        public override void ReleaseConnections()  
        {  
  
            connMgr.ReleaseConnection(sqlConn);  
  
        }  
  
    }  
    ```  
  
### <a name="flat-file-source-example"></a>플랫 파일 원본 예  
 이 예에서는 기존 플랫 파일 연결 관리자를 사용하여 플랫 파일의 데이터를 데이터 흐름으로 로드하는 원본 구성 요소를 보여 줍니다. 플랫 파일 원본 데이터는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터를 내보내는 방법으로 만듭니다.  
  
 이 예제 코드를 실행하려면 다음과 같이 패키지와 구성 요소를 구성해야 합니다.  
  
1.  사용 하 여는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내보내려면 가져오기 및 내보내기 마법사는 **Person.Address** 에서 테이블의 **AdventureWorks** 샘플 데이터베이스를 쉼표로 구분 된 플랫 파일. 이 예제에서는 파일 이름으로 ExportedAddresses.txt를 사용합니다.  
  
2.  내보낸 데이터 파일에 연결하는 플랫 파일 연결 관리자를 만듭니다.  
  
3.  데이터 흐름 디자이너 화면에 새 스크립트 구성 요소를 추가하고 이 구성 요소를 원본으로 구성합니다.  
  
4.  열기는 **스크립트 변환 편집기**합니다. 에 **입 / 출력** 페이지에서 기본와 같은 보다 알기 쉬운 이름으로 출력의 이름을, **MyAddressOutput**합니다. 추가 하 고 두 개의 출력 열 구성 **AddressID** 및 **도시**합니다.  
  
5.  에 **연결 관리자** 페이지를 추가 하거나 플랫 파일 연결 관리자와 같은 설명이 포함 된 이름을 사용 하 여 만들 **MyFlatFileSrcConnectionManager**합니다.  
  
6.  에 **스크립트** 페이지 **스크립트 편집** 뒤에 스크립트를 입력 합니다. 다음 스크립트 개발 환경을 닫습니다 및 **스크립트 변환 편집기**합니다.  
  
7.  만들기 및 대상 구성 요소와 같은 구성는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대상 또는에서 보여 준 예제 대상 구성 요소 [스크립트 구성 요소를 사용 하 여 대상 만들기](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)합니다. 그런 다음 원본 구성 요소를 대상에 연결합니다. 변환하지 않고 원본을 대상에 직접 연결할 수 있습니다. 다음 명령을 실행 하 여 대상 테이블을 만들 수 있습니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] 명령에 **AdventureWorks** 데이터베이스:  
  
    ```sql
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
8.  예제를 실행합니다.  
  
    ```vb  
    Imports System.IO  
    ...  
    Public Class ScriptMain  
        Inherits UserComponent  
  
        Private textReader As StreamReader  
        Private exportedAddressFile As String  
  
        Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
            Dim connMgr As IDTSConnectionManager100 = _  
                Me.Connections.MyFlatFileSrcConnectionManager  
            exportedAddressFile = _  
                CType(connMgr.AcquireConnection(Nothing), String)  
  
        End Sub  
  
        Public Overrides Sub PreExecute()  
            MyBase.PreExecute()  
            textReader = New StreamReader(exportedAddressFile)  
        End Sub  
  
        Public Overrides Sub CreateNewOutputRows()  
  
            Dim nextLine As String  
            Dim columns As String()  
  
            Dim delimiters As Char()  
            delimiters = ",".ToCharArray  
  
            nextLine = textReader.ReadLine  
            Do While nextLine IsNot Nothing  
                columns = nextLine.Split(delimiters)  
                With MyAddressOutputBuffer  
                    .AddRow()  
                    .AddressID = columns(0)  
                    .City = columns(3)  
                End With  
                nextLine = textReader.ReadLine  
            Loop  
  
        End Sub  
  
        Public Overrides Sub PostExecute()  
            MyBase.PostExecute()  
            textReader.Close()  
  
        End Sub  
  
    End Class  
    ```  
  
    ```csharp  
    using System.IO;  
    public class ScriptMain:  
        UserComponent  
  
    {  
        private StreamReader textReader;  
        private string exportedAddressFile;  
  
        public override void AcquireConnections(object Transaction)  
        {  
  
            IDTSConnectionManager100 connMgr = this.Connections.MyFlatFileSrcConnectionManager;  
            exportedAddressFile = (string)connMgr.AcquireConnection(null);  
  
        }  
  
        public override void PreExecute()  
        {  
            base.PreExecute();  
            textReader = new StreamReader(exportedAddressFile);  
        }  
  
        public override void CreateNewOutputRows()  
        {  
  
            string nextLine;  
            string[] columns;  
  
            char[] delimiters;  
            delimiters = ",".ToCharArray();  
  
            nextLine = textReader.ReadLine();  
            while (nextLine != null)  
            {  
                columns = nextLine.Split(delimiters);  
                {  
                    MyAddressOutputBuffer.AddRow();  
                    MyAddressOutputBuffer.AddressID = columns[0];  
                    MyAddressOutputBuffer.City = columns[3];  
                }  
                nextLine = textReader.ReadLine();  
            }  
  
        }  
  
        public override void PostExecute()  
        {  
  
            base.PostExecute();  
            textReader.Close();  
  
        }  
  
    }  
    ```  
  
## <a name="see-also"></a>관련 항목:  
 [스크립트 구성 요소를 사용 하 여 대상 만들기](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)   
 [사용자 지정 원본 구성 요소 개발](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md)  
  
  

