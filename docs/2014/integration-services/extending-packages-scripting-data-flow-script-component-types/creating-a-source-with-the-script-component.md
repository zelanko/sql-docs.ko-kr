---
title: 스크립트 구성 요소를 사용하여 원본 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script component [Integration Services], source components
- output columns [Integration Services]
- sources [Integration Services], components
ms.assetid: 547c4179-ea82-4265-8c6f-04a2aa77a3c0
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 8b82b7776bf9a56e5c72b5ffabdf6d8398b5d183
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84968587"
---
# <a name="creating-a-source-with-the-script-component"></a>스크립트 구성 요소를 사용하여 원본 만들기
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지의 데이터 흐름에서 원본 구성 요소를 사용하여 데이터 원본의 데이터를 로드하고 다운스트림 변환 및 대상에 전달할 수 있습니다. 일반적으로 데이터 원본에 연결하는 데는 기존 연결 관리자를 사용합니다.

 스크립트 구성 요소에 대 한 개요를 보려면 [스크립트 구성 요소를 사용 하 여 데이터 흐름 확장] (. /extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md.

 스크립트 구성 요소 및 해당 구성 요소가 생성하는 인프라 코드를 사용하면 사용자 지정 데이터 흐름 구성 요소를 개발하는 과정이 훨씬 간단해집니다. 하지만 스크립트 구성 요소의 작동 방식을 이해하려면 사용자 지정 데이터 흐름 구성 요소를 개발하는 데 필요한 단계를 파악하는 것이 좋습니다. [사용자 지정 데이터 흐름 구성 요소 개발](../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md) 섹션과 이 섹션의 [사용자 지정 원본 구성 요소 개발](../extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md) 항목을 참조하세요.

## <a name="getting-started-with-a-source-component"></a>원본 구성 요소 시작
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너의 데이터 흐름 창에 스크립트 구성 요소를 추가하면 원본, 대상 또는 변환 스크립트를 선택하기 위한 **스크립트 구성 요소 유형 선택** 대화 상자가 열립니다. 이 대화 상자에서 **원본**을 선택합니다.

## <a name="configuring-a-source-component-in-metadata-design-mode"></a>메타데이터 디자인 모드에서 원본 구성 요소 구성
 원본 구성 요소를 만들도록 선택한 후에는 **스크립트 변환 편집기**를 사용하여 구성 요소를 구성합니다. 자세한 내용은 [스크립트 구성 요소 편집기에서 스크립트 구성 요소 구성](../extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)을 참조하세요.

 데이터 흐름 원본 구성 요소는 입력을 사용하지 않으며 하나 이상의 출력을 지원합니다. 구성 요소의 출력을 구성하는 것은 사용자 지정 스크립트를 작성하기 전에 메타데이터 디자인 모드에서 **스크립트 변환 편집기**를 사용하여 완료해야 하는 단계 중 하나입니다.

 **스크립트 변환 편집기**의 **스크립트** 페이지에서 **ScriptLanguage** 속성을 설정하여 스크립트 언어를 지정할 수도 있습니다.

> [!NOTE]
>  스크립트 구성 요소 및 스크립트 태스크에 대한 기본 스크립트 언어를 설정하려면 **옵션** 대화 상자의 **일반** 페이지에서 **스크립트 언어** 옵션을 사용합니다. 자세한 내용은 [General Page](../general-page-of-integration-services-designers-options.md)을 참조하세요.

### <a name="adding-connection-managers"></a>연결 관리자 추가
 일반적으로 원본 구성 요소는 기존 연결 관리자를 사용하여 데이터 흐름으로 로드할 데이터가 있는 데이터 원본에 연결합니다. **스크립트 변환 편집기**의 **연결 관리자** 페이지에서 **추가**를 클릭하여 적절한 연결 관리자를 추가합니다.

 그러나 연결 관리자는 단지 특정 유형의 데이터 원본에 연결하는 데 필요한 정보를 캡슐화하고 저장하는 편리한 단위일 뿐입니다. 데이터를 로드하거나 저장하고 또한 데이터 원본에 대한 연결을 열고 닫는 사용자 지정 코드는 개발자가 직접 작성해야 합니다.

 스크립트 구성 요소에서 연결 관리자를 사용하는 방법에 대한 일반적은 내용은 [스크립트 구성 요소에서 데이터 원본에 연결](../extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md)을 참조하세요.

 **스크립트 변환 편집기**의 **연결 관리자** 페이지에 대한 자세한 내용은 [스크립트 변환 편집기&#40;연결 관리자 페이지&#41;](../script-transformation-editor-connection-managers-page.md)를 참조하세요.

### <a name="configuring-outputs-and-output-columns"></a>출력 및 출력 열 구성
 원본 구성 요소는 입력을 사용하지 않으며 하나 이상의 출력을 지원합니다. **스크립트 변환 편집기**의 **입/출력** 페이지에는 기본적으로 단일 출력이 만들어져 있지만 출력 열은 만들어져 있지 않습니다. 편집기의 이 페이지에서 다음과 같은 항목을 구성할 수 있습니다.

-   각 출력에 대해 수동으로 출력 열을 추가하고 구성해야 합니다. 각 출력에 대한 출력 열 폴더를 선택하고 **열 추가** 및 **열 제거** 단추를 사용하여 원본 구성 요소의 각 출력에 대한 출력 열을 관리합니다. 나중에 스크립트에서는 자동 생성 코드에서 만들어진 형식화된 접근자 속성을 사용하여 출력을 여기에서 할당한 이름으로 참조합니다.

-   예기치 않은 값이 포함된 행에 대한 시뮬레이션된 오류 출력과 같은 추가 출력을 하나 이상 만들 수 있습니다. 원본 구성 요소의 출력을 관리하려면 **출력 추가** 및 **출력 제거** 단추를 사용합니다. 각 행을 동일한 `ExclusionGroup` 값을 공유하는 출력 중 하나로만 전송하려는 경우 사용 가능한 모든 출력의 `ExclusionGroup` 속성에 0이 아닌 동일한 값을 지정하지 않으면 모든 입력 행이 사용 가능한 모든 출력으로 전송됩니다. `ExclusionGroup`을 식별하기 위해 선택한 특정 정수 값은 중요하지 않습니다.

    > [!NOTE]
    >  모든 행을 출력하지 않으려는 경우 단일 출력과 함께 0이 아닌 `ExclusionGroup` 속성 값을 사용할 수도 있습니다. 그러나이 경우 출력으로 보낼 각 행에 대해 **Directrowto \<outputbuffer> ** 메서드를 명시적으로 호출 해야 합니다.

-   출력에 이름을 지정할 수 있습니다. 나중에 스크립트에서는 자동 생성 코드에서 만들어진 형식화된 접근자 속성을 사용하여 출력을 이름으로 참조합니다.

-   일반적으로 동일한 `ExclusionGroup`의 여러 출력에는 동일한 출력 열이 있습니다. 그러나 시뮬레이션된 오류 출력을 만드는 경우 오류 정보를 저장할 다른 열을 추가할 수 있습니다. 데이터 흐름 엔진에서 오류 행을 처리하는 방법은 [데이터 흐름 구성 요소에서 오류 출력 사용](../extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)을 참조하세요. 그러나 스크립트 구성 요소에서는 개발자가 직접 코드를 작성하여 추가 열을 적절한 오류 정보로 채워야 합니다. 자세한 내용은 [스크립트 구성 요소의 오류 출력 시뮬레이션](../extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md)을 참조하세요.

 **스크립트 변환 편집기**의 **입/출력** 페이지에 대한 자세한 내용은 [스크립트 변환 편집기&#40;입/출력 페이지&#41;](../script-transformation-editor-inputs-and-outputs-page.md)를 참조하세요.

### <a name="adding-variables"></a>변수 추가
 스크립트에 사용 하려는 값이 포함 된 기존 변수가 있는 경우 스크립트 `ReadOnlyVariables` `ReadWriteVariables` **변환 편집기**의 **스크립트** 페이지에서 및 속성 필드에 해당 변수를 추가할 수 있습니다.

 속성 필드에 여러 변수를 입력하는 경우 변수 이름을 쉼표로 구분합니다. 및 속성 필드 옆의 줄임표 (**...**) 단추를 클릭 하 `ReadOnlyVariables` `ReadWriteVariables` 고 **변수 선택** 대화 상자에서 변수를 선택 하 여 여러 개의 변수를 입력할 수도 있습니다.

 스크립트 구성 요소에서 변수를 사용하는 방법에 대한 일반적인 내용은 [스크립트 구성 요소에서 변수 사용](../extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md)을 참조하세요.

 **스크립트 변환 편집기**의 **스크립트** 페이지에 대한 자세한 내용은 [스크립트 변환 편집기&#40;스크립트 페이지&#41;](../script-transformation-editor-script-page.md)를 참조하세요.

## <a name="scripting-a-source-component-in-code-design-mode"></a>코드 디자인 모드에서 원본 구성 요소 스크립팅
 구성 요소에 대한 메타데이터를 구성한 후에는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] VSTA([!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications) IDE를 열고 사용자 지정 스크립트를 코딩합니다. VSTA를 열려면 **스크립트 변환 편집기**의 **스크립트** 페이지에서 **스크립트 편집**을 클릭합니다. **ScriptLanguage** 속성에서 선택한 스크립트 언어에 따라 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# 중 하나를 사용하여 스크립트를 작성할 수 있습니다.

 스크립트 구성 요소를 사용하여 만든 모든 종류의 구성 요소에 적용되는 중요한 정보는 [스크립트 구성 요소 코딩 및 디버깅](../extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)을 참조하세요.

### <a name="understanding-the-auto-generated-code"></a>자동 생성 코드 이해
 원본 구성 요소를 만들고 구성한 후 VSTA IDE를 열면 편집 가능한 `ScriptMain` 클래스가 코드 편집기에 나타납니다. 이 `ScriptMain` 클래스에서 사용자 지정 코드를 작성합니다.

 `ScriptMain` 클래스에는 `CreateNewOutputRows` 메서드에 대한 스텁이 포함되어 있습니다. `CreateNewOutputRows`는 원본 구성 요소에서 가장 중요한 메서드입니다.

 VSTA에서 **프로젝트 탐색기** 창을 열면 스크립트 구성 요소가 읽기 전용 `BufferWrapper` 및 프로젝트 항목도 생성 한 것을 볼 수 있습니다 `ComponentWrapper` . `ScriptMain` 클래스는 `UserComponent` 프로젝트 항목의 `ComponentWrapper` 클래스에서 상속됩니다.

 런타임에 데이터 흐름 엔진은 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponentHost.PrimeOutput%2A> 부모 클래스의 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 메서드를 재정의하는 `PrimeOutput` 클래스의 `UserComponent` 메서드를 호출합니다. 그러면 `PrimeOutput` 메서드는 다음 메서드를 호출합니다.

1.  `CreateNewOutputRows` 메서드: 처음에는 비어 있는 출력 버퍼에 데이터 원본의 행을 추가하려면 `ScriptMain`에서 이 메서드를 재정의합니다.

2.  `FinishOutputs` 메서드: 이 메서드는 기본적으로 비어 있습니다. 출력을 완료하는 데 필요한 처리를 수행하려면 `ScriptMain`에서 이 메서드를 재정의합니다.

3.  프라이빗 `MarkOutputsAsFinished` 메서드: 이 메서드는 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer.SetEndOfRowset%2A> 부모 클래스의 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> 메서드를 호출하여 출력이 끝났음을 데이터 흐름 엔진에 알립니다. 따라서 개발자가 작성하는 코드에서 `SetEndOfRowset`을 명시적으로 호출할 필요가 없습니다.

### <a name="writing-your-custom-code"></a>사용자 지정 코드 작성
 사용자 지정 원본 구성 요소 만들기를 마치기 위해 `ScriptMain` 클래스에서 사용할 수 있는 다음 메서드에서 스크립트를 작성할 수 있습니다.

1.  `AcquireConnections` 메서드를 재정의하여 외부 데이터 원본에 연결합니다. 연결 관리자에서 연결 개체나 필요한 연결 정보를 추출합니다.

2.  모든 원본 데이터를 동시에 로드할 수 있는 경우 `PreExecute` 메서드를 재정의하여 데이터를 로드합니다. 예를 들어 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 데이터베이스에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결에 대해 `SqlCommand`를 실행하고 모든 원본 데이터를 동시에 `SqlDataReader`로 로드할 수 있습니다. 텍스트 파일을 읽는 경우와 같이 원본 데이터를 한 번에 한 행씩 로드해야 하는 경우에는 `CreateNewOutputRows`에서 행을 반복할 때 데이터를 로드할 수 있습니다.

3.  재정의된 `CreateNewOutputRows` 메서드를 사용하여 빈 출력 버퍼에 새 행을 추가하고 새 출력 행의 각 열 값을 채웁니다. 각 출력 버퍼의 `AddRow` 메서드를 사용하여 비어 있는 새 행을 추가한 다음 각 열의 값을 설정합니다. 일반적으로는 외부 원본에서 로드된 열의 값을 복사합니다.

4.  `PostExecute` 메서드를 재정의하여 데이터 처리를 마칩니다. 예를 들어 데이터를 로드하는 데 사용한 `SqlDataReader`를 닫을 수 있습니다.

5.  필요한 경우 `ReleaseConnections` 메서드를 재정의하여 외부 데이터 원본과의 연결을 끊습니다.

## <a name="examples"></a>예
 다음 예에서는 `ScriptMain` 클래스에서 원본 구성 요소를 만드는 데 필요한 사용자 지정 코드를 보여 줍니다.

> [!NOTE]
>  이 예에서는 예제 데이터베이스의 **Person. Address** 테이블을 사용 `AdventureWorks` 하 여 데이터 흐름을 통해 첫 번째 및 네 번째 열인 **intaddressid** 와 **nvarchar (30) City** 열을 전달 합니다. 이 섹션의 원본, 변환 및 대상 예제에는 동일한 데이터가 사용됩니다. 각 예에 대해 필수 구성 요소 및 가정도 설명되어 있습니다.

### <a name="adonet-source-example"></a>ADO.NET 원본 예
 이 예에서는 기존 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블의 데이터를 데이터 흐름으로 로드하는 원본 구성 요소를 보여 줍니다.

 이 예제 코드를 실행하려면 다음과 같이 패키지와 구성 요소를 구성해야 합니다.

1.  `SqlClient` 공급자를 사용하여 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 데이터베이스에 연결하는 `AdventureWorks` 연결 관리자를 만듭니다.

2.  데이터 흐름 디자이너 화면에 새 스크립트 구성 요소를 추가하고 이 구성 요소를 원본으로 구성합니다.

3.  **스크립트 변환 편집기**를 엽니다. **입/출력** 페이지에서 기본 출력의 이름을 **MyAddressOutput**과 같이 보다 알기 쉬운 이름으로 바꾼 다음 **AddressID**와 **City**라는 두 개의 출력 열을 추가하고 구성합니다.

    > [!NOTE]
    >  **City** 출력 열의 데이터 형식을 반드시 DT_WSTR로 변경합니다.

4.  **연결 관리자** 페이지에서 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자를 추가하거나 만들고 해당 이름을 **MyADONETConnection**과 같은 이름으로 지정합니다.

5.  **스크립트** 페이지에서 **스크립트 편집**을 클릭하고 다음 스크립트를 입력합니다. 그런 다음 스크립트 개발 환경 및 **스크립트 변환 편집기**를 닫습니다.

6.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대상이나 [스크립트 구성 요소를 사용하여 대상 만들기](../extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)에서 보여 준 예제 대상 구성 요소와 같이 **AddressID** 및 **City** 열을 필요로 하는 대상 구성 요소를 만들고 구성합니다. 그런 다음 원본 구성 요소를 대상에 연결합니다. 변환을 사용 하지 않고 소스를 대상에 직접 연결할 수 있습니다. 데이터베이스에서 다음 명령을 실행 하 여 대상 테이블을 만들 수 있습니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] `AdventureWorks` .

    ```
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

1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가져오기 및 내보내기 마법사를 사용 하 여 예제 데이터베이스의 **Person. Address** 테이블을 `AdventureWorks` 쉼표로 구분 된 플랫 파일로 내보냅니다. 이 예제에서는 파일 이름으로 ExportedAddresses.txt를 사용합니다.

2.  내보낸 데이터 파일에 연결하는 플랫 파일 연결 관리자를 만듭니다.

3.  데이터 흐름 디자이너 화면에 새 스크립트 구성 요소를 추가하고 이 구성 요소를 원본으로 구성합니다.

4.  **스크립트 변환 편집기**를 엽니다. **입/출력** 페이지에서 기본 출력의 이름을 **MyAddressOutput**과 같이 보다 알기 쉬운 이름으로 바꿉니다. **AddressID** 및 **City**라는 두 개의 출력 열을 추가하고 구성합니다.

5.  **연결 관리자** 페이지에서 **MyFlatFileSrcConnectionManager**와 같이 알기 쉬운 이름을 사용하여 플랫 파일 연결 관리자를 추가하거나 만듭니다.

6.  **스크립트** 페이지에서 **스크립트 편집**을 클릭하고 다음 스크립트를 입력합니다. 그런 다음 스크립트 개발 환경 및 **스크립트 변환 편집기**를 닫습니다.

7.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대상이나 [스크립트 구성 요소를 사용하여 대상 만들기](../extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)에서 보여 준 예제 대상 구성 요소와 같은 대상 구성 요소를 만들고 구성합니다. 그런 다음 원본 구성 요소를 대상에 연결합니다. 변환을 사용 하지 않고 소스를 대상에 직접 연결할 수 있습니다. 데이터베이스에서 다음 명령을 실행 하 여 대상 테이블을 만들 수 있습니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] `AdventureWorks` .

    ```
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

![Integration Services 아이콘 (작은 아이콘)](../media/dts-16.gif "Integration Services 아이콘(작은 아이콘)")  **은 최신 상태로 유지 Integration Services**<br /> Microsoft의 최신 다운로드, 문서, 예제 및 비디오와 커뮤니티에서 선택된 솔루션을 보려면 MSDN의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 페이지를 방문하세요.<br /><br /> [MSDN의 Integration Services 페이지를 방문하세요.](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 이러한 업데이트에 대한 자동 알림을 받으려면 해당 페이지에서 제공하는 RSS 피드를 구독하세요.

## <a name="see-also"></a>참고 항목
 [스크립트 구성 요소를 사용 하 여 대상 만들기](../extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md) [사용자 지정 원본 구성 요소 개발](../extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md)


