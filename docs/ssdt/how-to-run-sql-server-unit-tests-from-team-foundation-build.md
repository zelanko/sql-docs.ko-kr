---
title: '방법: Team Foundation Build에서 SQL Server 단위 테스트 실행 | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 24f5b85d-d6f9-415f-b09f-933b78dc0b67
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1857f503abe300127d92c26ba5591407b863ebc0
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52527917"
---
# <a name="how-to-run-sql-server-unit-tests-from-team-foundation-build"></a>방법: Team Foundation Build에서 SQL Server 단위 테스트 실행
Team Foundation Build를 사용하여 BVT(빌드 확인 테스트)의 일부로 SQL Server 단위 테스트를 실행할 수 있습니다. 데이터베이스를 배포하도록 단위 테스트를 구성하고, 테스트 데이터를 생성하고, 선택한 테스트를 실행할 수 있습니다. Team Foundation Build에 익숙하지 않으면 이 항목의 절차를 수행하기 전에 다음 정보를 검토하십시오.  
  
-   [SQL Server 단위 테스트 만들기 및 정의](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
  
-   [방법: 응용 프로그램을 빌드한 후 예약된 테스트 구성 및 실행](https://msdn.microsoft.com/library/ms182465(VS.100).aspx)  
  
-   [기본 빌드 정의 만들기](https://msdn.microsoft.com/library/ms181716(VS.100).aspx)  
  
절차를 사용하기 전에 먼저 다음 작업을 수행하여 작업 환경을 구성해야 합니다.  
  
-   Team Foundation Build와 Team Foundation 버전 제어를 설치합니다. 대개 Team Foundation Build와 Team Foundation 버전 제어를 서로 다른 컴퓨터에 설치해야 합니다.  
  
-   Team Foundation Build와 동일한 컴퓨터에 Microsoft SQL Server Data Tools 빌드 유틸리티를 설치합니다. SQL Server Data Tools 빌드 유틸리티를 설치하려면 먼저 관리 설치 지점을 수행합니다. 관리 설치 지점에 대한 자세한 내용은 [SQL Server Data Tools 설치](../ssdt/install-sql-server-data-tools.md)를 참조하세요. 그런 다음 관리 설치 지점에 사용되는 위치(/location)에서 빌드 서버에 SSDTBuildUtilties.msi를 설치합니다.  
  
-   Visual Studio Team Foundation Server 인스턴스에 연결합니다.  
  
작업 환경을 구성한 후에는 다음 단계를 수행해야 합니다.  
  
1.  데이터베이스 프로젝트를 만듭니다.  
  
2.  데이터베이스 프로젝트에 대한 스키마 및 개체를 가져오거나 만듭니다.  
  
3.  빌드 및 배포를 위한 데이터베이스 프로젝트 속성을 구성합니다.  
  
4.  하나 이상의 단위 테스트를 만듭니다.  
  
5.  데이터베이스 프로젝트와 단위 테스트 프로젝트를 포함하는 솔루션을 버전 제어에 추가하고 모든 파일을 체크 인합니다.  
  
이 항목의 절차에서는 자동화된 테스트 실행의 일부로 단위 테스트를 실행하기 위한 빌드 정의를 만드는 방법에 대해 설명합니다.  
  
1.  [x64 빌드 에이전트에서 데이터베이스 단위 테스트를 실행하도록 테스트 설정 구성](#ConfigureX64)  
  
2.  [테스트 범주에 테스트 지정(선택 사항)](#CreateATestList)  
  
3.  [테스트 프로젝트 수정](#ModifyTestProject)  
  
4.  [솔루션 체크 인](#CheckInTheTestList)  
  
5.  [빌드 정의 만들기](#CreateBuildDef)  
  
6.  [새 빌드 정의 실행](#RunBuild)  
  
**빌드 컴퓨터에서 SQL Server 단위 테스트 실행**  
  
빌드 컴퓨터에서 단위 테스트를 실행하면 단위 테스트가 데이터베이스 프로젝트 파일(.sqlproj)을 찾지 못할 수 있습니다. 이 문제는 app.config 파일이 상대 경로를 사용해서 해당 파일을 참조하기 때문에 발생합니다. 또한 SQL Server 단위 테스트를 실행하기 위해 사용하려는 SQL Server 인스턴스를 찾을 수 없는 경우에도 단위 테스트가 실패할 수 있습니다. 이 문제는 app.config 파일에 저장된 연결 문자열이 빌드 컴퓨터에서 유효하지 않은 경우에 발생할 수 있습니다.  
  
이러한 문제를 해결하기 위해서는 Team Foundation Build 환경과 관련된 구성 파일로 app.config를 재정의하는 재정의 섹션을 app.config에 지정해야 합니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [테스트 프로젝트 수정](#ModifyTestProject)을 참조하세요.  
  
## <a name="ConfigureX64"></a>x64 빌드 에이전트에서 SQL Server 단위 테스트를 실행하도록 테스트 설정 구성  
x64 빌드 에이전트에서 단위 테스트를 실행하려면 먼저 호스트 프로세스 플랫폼을 변경하도록 테스트 설정을 구성해야 합니다.  
  
#### <a name="to-specify-the-host-process-platform"></a>호스트 프로세스 플랫폼을 지정하려면  
  
1.  설정을 구성하려는 테스트 프로젝트가 포함된 솔루션을 엽니다.  
  
2.  **솔루션 탐색기**의 **솔루션 항목** 폴더에서 **Local.testsettings** 파일을 두 번 클릭합니다.  
  
    **테스트 설정** 대화 상자가 표시됩니다.  
  
3.  목록에서 **호스트**를 클릭합니다.  
  
4.  [세부 정보] 창의 **호스트 프로세스 플랫폼**에서 **MSIL**을 클릭하여 x64 빌드 에이전트에서 실행하도록 테스트를 구성합니다.  
  
5.  **적용**을 클릭합니다.  
  
## <a name="CreateATestList"></a>테스트 범주에 테스트 지정(선택 사항)  
일반적으로 단위 테스트를 실행할 빌드 정의를 만들 때는 하나 이상의 테스트 범주를 지정합니다. 빌드를 실행하면 지정된 범주의 모든 테스트가 실행됩니다.  
  
#### <a name="to-assign-tests-to-a-test-category"></a>테스트 범주에 테스트를 지정하려면  
  
1.  **테스트 뷰** 창을 엽니다.  
  
2.  테스트를 선택합니다.  
  
3.  속성 창에서 **테스트 범주**를 클릭한 다음, 오른쪽 끝 열에서 줄임표(...)를 클릭합니다.  
  
4.  **테스트 범주** 창의 **새 범주 추가** 상자에 새 테스트 범주의 이름을 입력합니다.  
  
5.  **추가**를 클릭한 후 **확인**을 클릭합니다.  
  
    새 테스트 범주가 테스트에 지정되고 해당 속성을 통해 다른 테스트에서도 사용할 수 있습니다.  
  
## <a name="ModifyTestProject"></a>테스트 프로젝트 수정  
기본적으로 Team Foundation Build는 단위 테스트 프로젝트를 빌드할 때 프로젝트의 app.config 파일로부터 구성 파일을 만듭니다. 데이터베이스 프로젝트의 경로가 app.config 파일에 상대 경로로 저장됩니다. Team Foundation Build는 사용자가 단위 테스트를 실행할 때와 다른 위치에 빌드 파일을 저장하기 때문에 Visual Studio에서 작동하는 상대 경로가 작동하지 않습니다. 또한 app.config 파일에는 사용자가 테스트하려는 데이터베이스를 지정하는 연결 문자열이 포함됩니다. 또한 테스트 프로젝트를 만들 때 사용한 것과 다른 데이터베이스에 단위 테스트를 연결해야 할 경우 Team Foundation Build에 대해 별도의 app.config 파일이 필요합니다. 다음 절차에서 항목을 수정하여 Team Foundation Build가 다른 구성을 사용하도록 테스트 프로젝트 및 빌드 서버를 설정할 수 있습니다.  
  
> [!IMPORTANT]  
> 이 절차는 각 테스트 프로젝트(.vbproj 또는 .vsproj)에 대해 수행해야 합니다.  
  
#### <a name="to-specify-an-appconfig-file-for-team-foundation-build"></a>Team Foundation Build에 대해 app.config 파일을 지정하려면  
  
1.  **솔루션 탐색기**에서 app.config 파일을 마우스 오른쪽 단추로 클릭하고 **복사**를 클릭합니다.  
  
2.  테스트 프로젝트를 마우스 오른쪽 단추로 클릭한 후 **붙여넣기**를 클릭합니다.  
  
3.  **app.config의 복사본**으로 표시된 파일을 마우스 오른쪽 단추로 클릭하고 이름 바꾸기를 클릭합니다.  
  
4.  _BuildComputer_**.sqlunitttest.config**를 입력하고 Enter 키를 누릅니다. 여기서 *BuildComputer*는 빌드 에이전트가 실행되는 컴퓨터의 이름입니다.  
  
5.  *BuildComputer*.sqlunitttest.config를 두 번 클릭합니다.  
  
    구성 파일이 편집기에서 열립니다.  
  
6.  Sources 폴더 및 하위 폴더에 대한 폴더 수준을 추가하여 .sqlproj 파일에 대한 상대 경로를 솔루션과 동일한 이름으로 변경합니다. 예를 들어 처음에 구성 파일에 다음 항목이 포함된 경우  
  
    ```  
    <DatabaseDeployment DatabaseProjectFileName="..\..\..\Database3\Database3.sqlproj"      Configuration="Debug" />  
    ```  
  
    파일을 다음과 같이 업데이트합니다.  
  
    ```  
    <DatabaseDeployment DatabaseProjectFileName="..\..\..\Database3\Database3.sqlproj"      Configuration="Debug" />  
    ```  
  
    작업을 마쳤으면 *BuildComputer*.sqlunitttest.config 파일이 Visual Studio 2010에 대한 다음 예와 비슷하게 표시되어야 합니다.  
  
    ```  
    <SqlUnitTesting_VS2010>  
        <DatabaseDeployment DatabaseProjectFileName="..\..\..\Database4\Database4.sqlproj"  
            Configuration="Debug" />  
        <DataGeneration ClearDatabase="true" />  
        <ExecutionContext Provider="System.Data.SqlClient" ConnectionString="Data Source=(localdb)\Projects;Initial Catalog=Database4;Integrated Security=True;Pooling=False"  
            CommandTimeout="30" />  
        <PrivilegedContext Provider="System.Data.SqlClient" ConnectionString="Data Source=(localdb)\Projects;Initial Catalog=Database4;Integrated Security=True;Pooling=False"  
            CommandTimeout="30" />  
    </SqlUnitTesting_VS2010>  
    ```  
  
    또는 Visual Studio 2012를 사용하는 경우에는 다음과 같습니다.  
  
    ```  
    <SqlUnitTesting_VS2012>  
            <DatabaseDeployment DatabaseProjectFileName="..\..\..\Database4\Database4.sqlproj"  
                Configuration="Debug" />  
            <DataGeneration ClearDatabase="true" />  
            <ExecutionContext Provider="System.Data.SqlClient" ConnectionString="Data Source=(localdb)\Projects;Initial Catalog=Database4;Integrated Security=True;Pooling=False"  
                CommandTimeout="30" />  
            <PrivilegedContext Provider="System.Data.SqlClient" ConnectionString="Data Source=(localdb)\Projects;Initial Catalog=Database4;Integrated Security=True;Pooling=False"  
                CommandTimeout="30" />  
        </SqlUnitTesting_VS2012>  
    ```  
  
7.  배포하려는 대상 데이터베이스에 대한 연결을 지정하도록 ExecutionContext 및 PrivilegedContext에 대한 ConnectionString 특성을 업데이트합니다.  
  
8.  **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
9. 솔루션 탐색기에서 app.config를 두 번 클릭합니다.  
  
10. 편집기에서 각 \<SqlUnitTesting_*VSVersion*> 노드에 `AllowConfigurationOverride="true"`를 추가합니다. 예를 들어 다음과 같이 사용할 수 있습니다.  
  
    ```  
    -- Update SqlUnitTesting_VS2010 node to:  
    <SqlUnitTesting_VS2010 AllowConfigurationOverride="true">   
  
    -- Update SqlUnitTesting_VS2012 node to:  
    <SqlUnitTesting_VS2012 AllowConfigurationOverride="true">  
    ```  
  
    이 항목을 변경하면 Team Foundation Build가 사용자가 만든 대체 구성 파일을 사용할 수 있습니다.  
  
11. **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
    이제 사용자 지정된 구성 파일을 포함하도록 Local.testsettings를 업데이트해야 합니다.  
  
#### <a name="to-customize-localtestsettings-to-deploy-the-customized-configuration-file"></a>사용자 지정된 구성 파일을 배포하도록 Local.testsettings를 사용자 지정하려면  
  
1.  솔루션 탐색기에서 Local.testsettings를 두 번 클릭합니다.  
  
    **테스트 설정** 대화 상자가 표시됩니다.  
  
2.  범주 목록에서 **배포**를 클릭합니다.  
  
3.  **배포 사용** 확인란을 선택합니다.  
  
4.  **파일 추가**를 클릭합니다.  
  
5.  **배포 파일 추가** 대화 상자에서 사용자가 만든 *BuildComputer*.sqlunitttest.config 파일을 지정합니다.  
  
6.  **적용**을 클릭합니다.  
  
7.  **닫기**를 클릭합니다.  
  
8.  **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
    이제 솔루션을 버전 제어에 체크 인합니다.  
  
## <a name="CheckInTheTestList"></a>솔루션 체크 인  
이 절차에서는 솔루션의 모든 파일을 체크 인합니다. 이러한 파일에는 테스트 범주 연결 및 테스트를 포함하는 솔루션의 테스트 메타데이터 파일이 포함됩니다. 테스트 콘텐츠를 추가, 삭제, 재구성 또는 변경할 때마다 테스트 메타데이터 파일이 해당 변경 사항을 반영하도록 자동으로 업데이트됩니다.  
  
> [!NOTE]  
> 이 절차에서는 Team Foundation 버전 제어를 사용하는 경우의 단계를 설명합니다. 다른 버전 제어 소프트웨어를 사용할 경우 해당 소프트웨어에 적합한 절차를 수행해야 합니다.  
  
#### <a name="to-check-in-the-solution"></a>솔루션을 체크 인하려면  
  
1.  Team Foundation Server를 실행하는 컴퓨터에 연결합니다.  
  
    자세한 내용은 [소스 제어 탐색기 사용](https://msdn.microsoft.com/library/ms181370(VS.100).aspx)을 참조하세요.  
  
2.  솔루션이 아직 소스 제어에 없으면 소스 제어에 추가합니다.  
  
    자세한 내용은 [버전 제어에 프로젝트 또는 솔루션 추가](https://msdn.microsoft.com/library/ms181374(VS.100).aspx)를 참조하세요.  
  
3.  **보기**를 클릭한 후 **보류 중인 체크 인**을 클릭합니다.  
  
4.  솔루션의 모든 파일을 체크 인합니다.  
  
    자세한 내용은 [보류 중인 변경 내용 체크 인](https://msdn.microsoft.com/library/ms181411(VS.100).aspx)을 참조하세요.  
  
    > [!NOTE]  
    > 자동화된 테스트를 만들고 관리하는 방법을 제어하는 특정 팀 프로세스가 있을 수 있습니다. 예를 들어 프로세스에 따라 코드를 해당 코드로 실행되는 테스트와 함께 체크 인하기 전에 빌드를 로컬로 확인해야 할 수 있습니다.  
  
    **솔루션 탐색기**에서 체크 인되었음을 나타내는 자물쇠 아이콘이 각 파일 옆에 나타납니다. 자세한 내용은 [버전 제어 파일 및 폴더 속성 보기](https://msdn.microsoft.com/library/ms245468(VS.100).aspx)를 참조하세요.  
  
    Team Foundation Build에서 테스트를 사용할 수 있게 되었습니다. 이제 실행하려는 테스트가 포함된 빌드 정의를 만들 수 있습니다.  
  
## <a name="CreateBuildDef"></a>빌드 정의 만들기  
  
#### <a name="to-create-a-build-definition"></a>빌드 정의를 만들려면  
  
1.  팀 탐색기에서 팀 프로젝트를 클릭하고 **빌드** 노드를 마우스 오른쪽 단추로 클릭한 후 **새 빌드 정의**를 클릭합니다.  
  
    **새 빌드 정의** 창이 나타납니다.  
  
2.  **빌드 정의 이름**에 빌드 정의에 사용할 이름을 입력합니다.  
  
3.  탐색 모음에서 **빌드 기본값**을 클릭합니다.  
  
4.  **다음 저장 폴더에 빌드 출력 복사(UNC 경로, 예: \\server\share)** 에 빌드 출력을 포함할 폴더를 지정합니다.  
  
    빌드 프로세스가 권한을 갖는 로컬 컴퓨터 또는 네트워크 위치에서 공유 폴더를 지정할 수 있습니다.  
  
5.  탐색 모음에서 **프로세스**를 클릭합니다.  
  
6.  **필수** 그룹의 **빌드할 항목**에서 찾아보기(...) 단추를 클릭합니다.  
  
7.  **프로젝트 목록 빌드 편집기** 대화 상자에서 **추가**를 클릭합니다.  
  
8.  이 연습의 앞부분에서 버전 제어에 추가한 솔루션 파일(.sln)을 지정하고 **확인**을 클릭합니다.  
  
    솔루션이 **빌드할 프로젝트 또는 솔루션 파일** 목록에 표시됩니다.  
  
9. **확인**을 클릭합니다.  
  
10. **기본** 그룹의 **자동화된 테스트**에서 실행하려는 테스트를 지정합니다. 기본적으로 솔루션에서 이름이 *test\*.dll로 지정된 파일에 포함된 테스트가 실행됩니다.  
  
11. **파일** 메뉴에서 *ProjectName* **저장**을 클릭합니다.  
  
    빌드 정의를 만들었습니다. 이제 테스트 프로젝트를 수정합니다.  
  
## <a name="RunBuild"></a>새 빌드 정의 실행  
  
#### <a name="to-run-the-new-build-type"></a>새 빌드 유형을 실행하려면  
  
1.  팀 탐색기에서 팀 프로젝트 노드와 빌드 노드를 차례로 확장하고 실행하려는 빌드 정의를 마우스 오른쪽 단추로 클릭한 다음 새 빌드 큐 대기를 클릭합니다.  
  
    **빌드 {**_TeamProjectName_**} 큐에 대기** 대화 상자에 기존의 모든 빌드 유형 목록이 표시됩니다.  
  
2.  필요에 따라 **빌드 정의**에서 새 빌드 정의를 클릭합니다.  
  
3.  **빌드 정의**, **빌드 에이전트** 및 **이 빌드의 저장 폴더** 필드의 값이 모두 적합한지 확인한 후 **큐**를 클릭합니다.  
  
    **빌드 탐색기**의 **큐 대기** 탭이 표시됩니다. 자세한 내용은 [완료된 빌드 관리 및 보기(Visual Studio 2010)](https://msdn.microsoft.com/library/ms181730(VS.100).aspx) 또는 [빌드 탐색기에서 빌드 관리(Visual Studio 2012)](https://msdn.microsoft.com/library/ms181732.aspx)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server 단위 테스트 실행](../ssdt/running-sql-server-unit-tests.md)  
[기본 빌드 정의 만들기](https://msdn.microsoft.com/library/ms181716(VS.100).aspx)  
[큐에 빌드 대기](https://msdn.microsoft.com/library/ms181722(VS.100).aspx)  
[실행 중인 빌드의 진행률 모니터링](https://msdn.microsoft.com/library/ms181724(VS.100).aspx)  
  
