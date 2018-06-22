---
title: 패키지 워크플로에 데이터 프로파일링 태스크 포함 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Data Profiling task [Integration Services], using output in workflow
ms.assetid: 39a51586-6977-4c45-b80b-0157a54ad510
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 31c3d3bdcfc2a986fc62ba32e2df443d74d7a8fd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36079818"
---
# <a name="incorporate-a-data-profiling-task-in-package-workflow"></a>패키지 워크플로에 데이터 프로파일링 태스크 포함
  데이터 프로파일링과 정리는 초기 단계의 자동 처리 대상이 아닙니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서 데이터 프로파일링 태스크의 출력을 통해 보고된 위반이 의미 있거나 과도한지 확인하려면 일반적으로 시각적 분석과 사람의 판단이 필요합니다. 데이터 품질 문제를 인지한 이후에도 정리를 위한 최선의 방법을 찾기 위한 신중한 계획이 필요합니다.  
  
 일단 데이터 품질에 대한 조건을 정립하고 나면 데이터 원본에 대한 주기적인 분석과 정리를 자동화할 수 있습니다. 다음과 같은 시나리오를 고려해 보십시오.  
  
-   **증분 로드 전에 데이터 품질 확인**. 데이터 프로파일링 태스크를 사용하여 Customers 테이블의 CustomerName 열에 사용할 새 데이터의 열 Null 비율 프로필을 계산할 수 있습니다. Null 값의 비율이 20%를 초과하면 운영자에게 프로필 출력이 포함된 전자 메일 메시지를 보내고 패키지를 끝냅니다. 그렇지 않으면 증분 로드를 계속 수행합니다.  
  
-   **지정된 조건이 충족되는 경우 정리 자동화**. 데이터 프로파일링 태스크를 사용하여 상태 조회 테이블에 대한 State 열과 우편 번호 조회 테이블에 대한 ZIP Code/Postal Code 열의 값 포함 프로필을 계산합니다. 상태 값의 포함 수준이 80% 미만인데 ZIP Code/Postal Code 값의 포함 수준이 99%를 초과한다면 이는 두 가지를 의미합니다. 첫째, State 데이터가 잘못되었습니다. 둘째, ZIP Code/Postal Code 데이터는 올바릅니다. 현재 Zip Code/Postal Code 값에서 올바른 State 값을 조회하여 State 데이터를 정리하는 데이터 흐름 태스크를 시작합니다.  
  
 데이터 흐름 태스크를 통합할 수 있는 워크플로를 확보한 후에는 이 태스크를 추가하는 데 필요한 단계를 파악해야 합니다. 다음 섹션에서는 데이터 흐름 태스크를 통합하는 일반적인 프로세스에 대해 설명합니다. 마지막 두 개의 섹션에서는 데이터 흐름 태스크를 데이터 원본에 직접 연결하거나 데이터 흐름의 변환된 데이터에 연결하는 방법에 대해 설명합니다.  
  
## <a name="defining-a-general-workflow-for-the-data-flow-task"></a>데이터 흐름 태스크의 일반적인 워크플로 정의  
 다음 절차에서는 패키지의 워크플로에서 데이터 프로파일링 태스크의 출력을 사용하기 위한 일반적인 방법을 간단히 설명합니다.  
  
#### <a name="to-use-the-output-of-the-data-profiling-task-programmatically-in-a-package"></a>패키지에서 프로그래밍 방식으로 데이터 프로파일링 태스크의 출력을 사용하려면  
  
1.  패키지에 데이터 프로파일링 태스크를 추가하고 구성합니다.  
  
2.  프로필 결과에서 검색하려는 값을 보유하도록 패키지 변수를 구성합니다.  
  
3.  스크립트 태스크를 추가하고 구성합니다. 데이터 프로파일링 태스크에 스크립트 태스크를 연결합니다. 스크립트 태스크에서 데이터 프로파일링 태스크의 출력 파일로부터 원하는 값을 읽고 패키지 변수를 채우는 코드를 작성합니다.  
  
4.  워크플로의 다운스트림 분기에 스크립트 태스크를 연결하는 선행 제약 조건에서 변수의 값을 사용하여 워크플로를 제어하는 식을 작성합니다.  
  
 데이터 프로파일링 태스크를 패키지의 워크플로에 통합할 때 태스크의 다음 두 가지 특징을 유의하십시오.  
  
-   **태스크 출력**. 데이터 프로파일링 태스크는 DataProfile.xsd 스키마에 따라 파일 또는 패키지 변수에 XML 형식으로 출력을 작성합니다. 따라서 패키지의 조건부 워크플로에서 프로필 결과를 사용하려면 이 XML 출력을 쿼리해야 합니다. Xpath 쿼리 언어를 사용하면 이 XML 출력을 손쉽게 쿼리할 수 있습니다. 이 XML 출력의 구조를 살펴보려면 예제 출력 파일 또는 스키마 자체를 열면 됩니다. 출력 파일 또는 스키마를 열려면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], 다른 XML 편집기 또는 메모장과 같은 텍스트 편집기를 사용합니다.  
  
    > [!NOTE]  
    >  데이터 프로필 뷰어에 표시되는 프로필 결과의 일부는 출력에서 직접 찾을 수 없는 계산된 값입니다. 예를 들어 열 Null 비율 프로필에는 전체 행 개수와 Null 값이 있는 행 개수가 포함됩니다. 열 Null 비율을 구하려면 이 두 값을 쿼리한 다음 Null 값을 가진 행의 비율을 계산해야 합니다.  
  
-   **태스크 입력**. 데이터 프로파일링 태스크는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에서 입력을 읽습니다. 따라서 이미 로드되어 데이터 흐름에서 변환된 데이터를 프로파일링하려면 메모리에 있는 데이터를 준비 테이블에 저장해야 합니다.  
  
 다음 섹션에서는 외부 데이터 원본으로부터 직접 가져오거나 데이터 흐름 태스크에서 변환된 프로파일링 데이터에 이 일반 워크플로를 적용합니다. 또한 데이터 흐름 태스크의 입력 및 출력 요구 사항을 처리하는 방법을 보여 줍니다.  
  
## <a name="connecting-the-data-profiling-task-directly-to-an-external-data-source"></a>데이터 프로파일링 태스크를 외부 데이터 원본에 직접 연결  
 데이터 프로파일링 태스크는 데이터 원본에서 직접 가져온 데이터를 프로파일링할 수 있습니다.  다음 예에서는 이 기능을 설명하기 위해 데이터 프로파일링 태스크를 사용하여 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에 있는 Person.Address 테이블의 열에서 열 Null 비율 프로필을 계산합니다. 그런 다음 스크립트 태스크를 사용하여 출력 파일에서 결과를 검색하고, 워크플로를 제어하는 데 사용할 수 있는 패키지 변수를 채웁니다.  
  
> [!NOTE]  
>  이 간단한 예에서는 Null 값 비율이 높은 AddressLine2 열을 사용합니다.  
  
 이 예는 다음과 같은 단계로 구성됩니다.  
  
-   프로필 결과를 포함할 출력 파일과 외부 데이터 원본에 연결되는 연결 관리자를 구성합니다.  
  
-   데이터 프로파일링 태스크에 필요한 값을 보유할 패키지 변수를 구성합니다.  
  
-   열 Null 비율 프로필을 계산하도록 데이터 프로파일링 태스크를 구성합니다.  
  
-   데이터 프로파일링 태스크의 XML 출력을 사용하도록 스크립트 태스크를 구성합니다.  
  
-   데이터 프로파일링 태스크의 결과를 바탕으로 실행할 워크플로의 다운스트림 분기를 제어하는 선행 제약 조건을 구성합니다.  
  
### <a name="configure-the-connection-managers"></a>연결 관리자 구성  
 이 예에서는 다음과 같은 두 개의 연결 관리자가 사용됩니다.  
  
-   [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 데이터베이스에 연결되는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 연결 관리자  
  
-   데이터 프로파일링 태스크의 결과를 보유할 출력 파일을 만드는 파일 연결 관리자  
  
##### <a name="to-configure-the-connection-managers"></a>연결 관리자를 구성하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 새 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 만듭니다.  
  
2.  패키지에 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자를 추가합니다. .NET Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient)를 사용하고, 가용한 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스 인스턴스에 연결하도록 이 연결 관리자를 구성합니다.  
  
     기본적으로 연결 관리자의 이름은 \<server name>.AdventureWorks1입니다.  
  
3.  패키지에 파일 연결 관리자를 추가합니다. 데이터 프로파일링 태스크를 위한 출력 파일을 만들도록 이 연결 관리자를 구성합니다.  
  
     이 예에서는 파일 이름으로 DataProfile1.xml을 사용합니다. 기본적으로 연결 관리자의 이름은 파일과 동일합니다.  
  
### <a name="configure-the-package-variables"></a>패키지 변수 구성  
 이 예에서는 다음과 같은 두 개의 패키지 변수를 사용합니다.  
  
-   ProfileConnectionName 변수는 파일 연결 관리자의 이름을 스크립트 태스크에 전달합니다.  
  
-   AddressLine2NullRatio 변수는 이 열에 대해 계산된 Null 비율을 스크립트 태스크에서 패키지로 전달합니다.  
  
##### <a name="to-configure-the-package-variables-that-will-hold-profile-results"></a>프로필 결과를 보유할 패키지 변수를 구성하려면  
  
-   **변수** 창에서 다음 두 개의 패키지 변수를 추가하고 구성합니다.  
  
    -   이름을 입력 `ProfileConnectionName`, 변수 중 하나에 대 한이 변수를의 유형을 설정 하 고 **문자열**합니다.  
  
    -   이름을 입력 `AddressLine2NullRatio`, 다른 변수 및 설정에 대 한이 변수를 유형의 **Double**합니다.  
  
### <a name="configure-the-data-profiling-task"></a>데이터 프로파일링 태스크 구성  
 데이터 프로파일링 태스크는 다음과 같이 구성해야 합니다.  
  
-   [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자가 입력으로 제공하는 데이터를 사용하도록 구성  
  
-   입력 데이터에 대해 열 Null 비율 프로필을 수행하도록 구성  
  
-   파일 연결 관리자와 연관된 파일에 프로필 결과를 저장하도록 구성  
  
##### <a name="to-configure-the-data-profiling-task"></a>데이터 프로파일링 태스크를 구성하려면  
  
1.  제어 흐름에 데이터 프로파일링 태스크를 추가합니다.  
  
2.  **데이터 프로파일링 태스크 편집기** 를 열어 태스크를 구성합니다.  
  
3.  편집기 **일반** 페이지의 **대상**에서 이전에 구성한 파일 연결 관리자의 이름을 선택합니다.  
  
4.  편집기의 **프로필 요청** 페이지에서 새 열 Null 비율 프로필을 만듭니다.  
  
5.  **요청 속성** 창의 **ConnectionManager**에서 이전에 구성한 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자를 선택합니다. 그런 다음 **TableOrView**에서 Person.Address를 선택합니다.  
  
6.  데이터 프로파일링 태스크 편집기를 닫습니다.  
  
### <a name="configure-the-script-task"></a>스크립트 태스크 구성  
 스크립트 태스크는 출력 파일에서 결과를 검색하고 이전에 구성된 패키지 변수를 채우도록 구성되어야 합니다.  
  
##### <a name="to-configure-the-script-task"></a>스크립트 태스크를 구성하려면  
  
1.  제어 흐름에 스크립트 태스크를 추가합니다.  
  
2.  데이터 프로파일링 태스크에 스크립트 태스크를 연결합니다.  
  
3.  **스크립트 태스크 편집기** 를 열어 태스크를 구성합니다.  
  
4.  **스크립트** 페이지에서 선호하는 프로그래밍 언어를 선택합니다. 그런 다음 스크립트에서 사용할 수 있는 두 개의 패키지 변수를 만듭니다.  
  
    1.  에 대 한 `ReadOnlyVariables`선택, `ProfileConnectionName`합니다.  
  
    2.  에 대 한 **ReadWriteVariables**선택, `AddressLine2NullRatio`합니다.  
  
5.  **스크립트 편집** 을 선택하여 스크립트 개발 환경을 엽니다.  
  
6.  System.Xml 네임스페이스에 대한 참조를 추가합니다.  
  
7.  선택한 프로그래밍 언어에 해당하는 예제 코드를 입력합니다.  
  
    ```vb  
    Imports System  
    Imports Microsoft.SqlServer.Dts.Runtime  
    Imports System.Xml  
  
    Public Class ScriptMain  
  
      Private FILENAME As String = "C:\ TEMP\DataProfile1.xml"  
      Private PROFILE_NAMESPACE_URI As String = "http://schemas.microsoft.com/DataDebugger/"  
      Private NULLCOUNT_XPATH As String = _  
        "/default:DataProfile/default:DataProfileOutput/default:Profiles" & _  
        "/default:ColumnNullRatioProfile[default:Column[@Name='AddressLine2']]/default:NullCount/text()"  
      Private TABLE_XPATH As String = _  
        "/default:DataProfile/default:DataProfileOutput/default:Profiles" & _  
        "/default:ColumnNullRatioProfile[default:Column[@Name='AddressLine2']]/default:Table"  
  
      Public Sub Main()  
  
        Dim profileConnectionName As String  
        Dim profilePath As String  
        Dim profileOutput As New XmlDocument  
        Dim profileNSM As XmlNamespaceManager  
        Dim nullCountNode As XmlNode  
        Dim nullCount As Integer  
        Dim tableNode As XmlNode  
        Dim rowCount As Integer  
        Dim nullRatio As Double  
  
        ' Open output file.  
        profileConnectionName = Dts.Variables("ProfileConnectionName").Value.ToString()  
        profilePath = Dts.Connections(profileConnectionName).ConnectionString  
        profileOutput.Load(profilePath)  
        profileNSM = New XmlNamespaceManager(profileOutput.NameTable)  
        profileNSM.AddNamespace("default", PROFILE_NAMESPACE_URI)  
  
        ' Get null count for column.  
        nullCountNode = profileOutput.SelectSingleNode(NULLCOUNT_XPATH, profileNSM)  
        nullCount = CType(nullCountNode.Value, Integer)  
  
        ' Get row count for table.  
        tableNode = profileOutput.SelectSingleNode(TABLE_XPATH, profileNSM)  
        rowCount = CType(tableNode.Attributes("RowCount").Value, Integer)  
  
        ' Compute and return null ratio.  
        nullRatio = nullCount / rowCount  
        Dts.Variables("AddressLine2NullRatio").Value = nullRatio  
  
        Dts.TaskResult = Dts.Results.Success  
  
      End Sub  
  
    End Class  
    ```  
  
    ```csharp  
    using System;  
    using Microsoft.SqlServer.Dts.Runtime;  
    using System.Xml;  
  
    public class ScriptMain  
    {  
  
      private string FILENAME = "C:\\ TEMP\\DataProfile1.xml";  
      private string PROFILE_NAMESPACE_URI = "http://schemas.microsoft.com/DataDebugger/";  
      private string NULLCOUNT_XPATH = "/default:DataProfile/default:DataProfileOutput/default:Profiles" + "/default:ColumnNullRatioProfile[default:Column[@Name='AddressLine2']]/default:NullCount/text()";  
      private string TABLE_XPATH = "/default:DataProfile/default:DataProfileOutput/default:Profiles" + "/default:ColumnNullRatioProfile[default:Column[@Name='AddressLine2']]/default:Table";  
  
      public void Main()  
      {  
  
        string profileConnectionName;  
        string profilePath;  
        XmlDocument profileOutput = new XmlDocument();  
        XmlNamespaceManager profileNSM;  
        XmlNode nullCountNode;  
        int nullCount;  
        XmlNode tableNode;  
        int rowCount;  
        double nullRatio;  
  
        // Open output file.  
        profileConnectionName = Dts.Variables["ProfileConnectionName"].Value.ToString();  
        profilePath = Dts.Connections[profileConnectionName].ConnectionString;  
        profileOutput.Load(profilePath);  
        profileNSM = new XmlNamespaceManager(profileOutput.NameTable);  
        profileNSM.AddNamespace("default", PROFILE_NAMESPACE_URI);  
  
        // Get null count for column.  
        nullCountNode = profileOutput.SelectSingleNode(NULLCOUNT_XPATH, profileNSM);  
        nullCount = (int)nullCountNode.Value;  
  
        // Get row count for table.  
        tableNode = profileOutput.SelectSingleNode(TABLE_XPATH, profileNSM);  
        rowCount = (int)tableNode.Attributes["RowCount"].Value;  
  
        // Compute and return null ratio.  
        nullRatio = nullCount / rowCount;  
        Dts.Variables["AddressLine2NullRatio"].Value = nullRatio;  
  
        Dts.TaskResult = Dts.Results.Success;  
  
      }  
  
    }  
    ```  
  
    > [!NOTE]  
    >  이 절차에 사용되는 예제 코드는 파일에서 데이터 프로파일링 태스크의 출력을 로드하는 방법을 보여 줍니다. 파일이 아닌 패키지 변수에서 데이터 프로파일링 태스크의 출력을 로드하려면 이 절차 다음에 나오는 대체 예제 코드를 참조하십시오.  
  
8.  스크립트 개발 환경과 스크립트 태스크 편집기를 차례로 닫습니다.  
  
#### <a name="alternative-codereading-the-profile-output-from-a-variable"></a>대체 코드 - 변수에서 프로필 출력 읽기  
 앞의 절차는 파일에서 데이터 프로파일링 태스크의 출력을 로드하는 방법을 보여 줍니다. 대체 방법을 사용하여 패키지 변수에서 이 출력을 로드할 수 있습니다. 변수에서 출력을 로드하려면 예제 코드를 다음과 같이 변경해야 합니다.  
  
-   호출 된 `LoadXml` 의 메서드는 `XmlDocument` 클래스 대신는 `Load` 메서드.  
  
-   스크립트 태스크 편집기에서 작업의 프로필 출력이 포함 된 패키지 변수의 이름을 추가 `ReadOnlyVariables` 목록입니다.  
  
-   변수의 문자열 값을 전달는 `LoadXML` 메서드를 다음 코드 예제와 같이 합니다. 이 예에서는 프로필 출력이 포함된 패키지 변수의 이름으로 "ProfileOutput"을 사용합니다.  
  
    ```vb  
    Dim outputString As String  
    outputString = Dts.Variables("ProfileOutput").Value.ToString()  
    ...  
    profileOutput.LoadXml(outputString)  
    ```  
  
    ```csharp  
    string outputString;  
    outputString = Dts.Variables["ProfileOutput"].Value.ToString();  
    ...  
    profileOutput.LoadXml(outputString);  
    ```  
  
### <a name="configure-the-precedence-constraints"></a>선행 제약 조건 구성  
 선행 제약 조건은 데이터 프로파일링 태스크의 결과를 바탕으로 실행할 워크플로의 다운스트림 분기를 제어하도록 구성되어야 합니다.  
  
##### <a name="to-configure-the-precedence-constraints"></a>선행 제약 조건을 구성하려면  
  
-   워크플로의 다운스트림 분기에 스크립트 태스크를 연결하는 선행 제약 조건에서 변수의 값을 사용하여 워크플로를 제어하는 식을 작성합니다.  
  
     예를 들어 선행 제약 조건의 **식 연산** 을 **식 및 제약 조건**으로 설정할 수 있습니다. 그런 다음 `@AddressLine2NullRatio < .90` 을 식의 값으로 사용할 수 있습니다. 이렇게 하면 워크플로는 이전 태스크가 성공한 경우와 선택된 열의 Null 값 비율이 90% 미만인 경우 지정된 경로를 따릅니다.  
  
## <a name="connecting-the-data-profiling-task-to-transformed-data-from-the-data-flow"></a>데이터 흐름의 변환된 데이터에 데이터 프로파일링 태스크 연결  
 데이터 원본으로부터 직접 데이터를 프로파일링하는 대신 이미 로드되어 데이터 흐름에서 변환된 데이터를 프로파일링할 수 있습니다. 단, 데이터 프로파일링 태스크는 영구 데이터에 대해서만 작동하며 메모리 내 데이터에 대해서는 작동하지 않습니다. 따라서 먼저 대상 구성 요소를 사용하여 준비 테이블에 변환된 데이터를 저장해야 합니다.  
  
> [!NOTE]  
>  데이터 프로파일링 태스크를 구성할 때 기존 테이블과 열을 선택해야 합니다. 따라서 태스크를 구성하려면 먼저 디자인 타임에 준비 테이블을 만들어야 합니다. 즉, 이 시나리오에서는 런타임에 만들어지는 임시 테이블을 사용할 수 없습니다.  
  
 준비 테이블에 데이터를 저장한 후에는 다음 동작을 수행할 수 있습니다.  
  
-   데이터 프로파일링 태스크를 사용하여 데이터 프로파일링  
  
-   이 항목의 앞부분에서 설명한 대로 스크립트 태스크를 사용하여 결과 읽기  
  
-   이러한 결과를 사용하여 패키지의 후속 워크플로 제어  
  
 다음 절차에서는 데이터 흐름에 의해 변환된 데이터를 데이터 프로파일링 태스크를 사용하여 프로파일링하기 위한 일반적인 방법을 보여 줍니다. 이 단계는 앞에서 설명한 외부 데이터 원본에서 직접 가져온 데이터를 프로파일링하는 단계와 많이 비슷합니다. 다양한 구성 요소를 구성하는 방법은 앞의 단계를 참조하십시오.  
  
#### <a name="to-use-the-data-profiling-task-in-the-data-flow"></a>데이터 흐름에서 데이터 프로파일링 태스크를 사용하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 패키지를 만듭니다.  
  
2.  데이터 흐름에서 적절한 원본과 변환을 추가, 구성 및 연결합니다.  
  
3.  데이터 흐름에서 변환된 데이터를 준비 테이블에 저장하는 대상 구성 요소를 추가, 구성 및 연결합니다.  
  
4.  제어 흐름에서 준비 테이블의 변환된 데이터에 대해 원하는 프로파일을 계산하는 데이터 프로파일링 태스크를 추가하고 구성합니다. 데이터 프로파일링 태스크를 데이터 흐름 태스크에 연결합니다.  
  
5.  프로필 결과에서 검색하려는 값을 보유하도록 패키지 변수를 구성합니다.  
  
6.  스크립트 태스크를 추가하고 구성합니다. 데이터 프로파일링 태스크에 스크립트 태스크를 연결합니다. 스크립트 태스크에서 데이터 프로파일링 태스크의 출력으로부터 원하는 값을 읽고 패키지 변수를 채우는 코드를 작성합니다.  
  
7.  워크플로의 다운스트림 분기에 스크립트 태스크를 연결하는 선행 제약 조건에서 변수의 값을 사용하여 워크플로를 제어하는 식을 작성합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 프로 파일링 태스크 설정](data-profiling-task.md)   
 [데이터 프로필 뷰어](data-profile-viewer.md)  
  
  