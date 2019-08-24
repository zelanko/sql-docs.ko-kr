---
title: 사용자 지정 워크플로 만들기(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 8e4403e9-595c-4b6b-9d0c-f6ae1b2bc99d
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 87090611cd294e1af72484c4b0c03fcec1fe4f04
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68033950"
---
# <a name="create-a-custom-workflow-master-data-services"></a>사용자 지정 워크플로 만들기(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]는 비즈니스 규칙을 사용하여 기본적인 워크플로 솔루션을 만듭니다. 이러한 솔루션을 사용하면 지정 조건에 따라 자동으로 데이터에 대해 업데이트 및 유효성 검사 작업을 수행하고 전자 메일 알림이 전송되게 할 수 있습니다. 기본 제공 워크플로 동작으로 가능한 것보다 복잡한 처리가 필요한 경우에는 사용자 지정 워크플로를 사용하십시오. 사용자 지정 워크플로는 사용자가 만드는 .NET 어셈블리입니다. 사용자 워크플로 어셈블리가 호출되면 상황에 따라 필요한 동작이 코드에 사용될 수 있습니다. 예를 들어, 워크플로에 다중 계층 승인 또는 복잡한 의사 결정 트리와 같은 CEP(복합 이벤트 처리)가 필요한 경우 데이터를 분석하고 어디로 데이터를 보내서 승인을 받을지를 결정하는 사용자 지정 워크플로를 시작하도록 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]를 구성할 수 있습니다.  
  
## <a name="how-custom-workflows-are-processed"></a>사용자 지정 워크플로가 처리되는 방법  
 사용자 지정 워크플로를 처리할 때는 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 애플리케이션, SQL Server MDS Workflow Integration Service 및 워크플로 처리기 어셈블리라는 세 가지 주요 구성 요소가 사용됩니다. 이러한 구성 요소는 사용자 지정 워크플로를 다음과 같이 처리합니다.  
  
1.  [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]를 사용하여 워크플로를 시작하는 엔터티의 유효성을 검사합니다.  
  
2.  [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]가 비즈니스 규칙 조건에 맞는 멤버를 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 데이터베이스의 Service Broker 큐로 보냅니다.  
  
3.  SQL Server MDS Workflow Integration Service가 정기적으로 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 데이터베이스의 저장 프로시저를 호출합니다.  
  
4.  이 저장 프로시저가 Service Broker 큐에서 레코드를 찾으면 SQL Server MDS Workflow Integration Service로 해당 레코드를 반환합니다.  
  
5.  SQL Server MDS Workflow Integration Services가 해당 데이터를 워크플로 처리기 어셈블리로 라우팅합니다.  
  
> [!NOTE]  
>  참고: SQL Server MDS Workflow Integration Service는 간단한 프로세스를 트리거하기 위한 것입니다. 사용자 지정 코드에 복잡한 처리가 필요한 경우 별도의 스레드나 워크플로 프로세스 외부에서 처리를 완료하십시오.  
  
## <a name="configure-master-data-services-for-custom-workflows"></a>사용자 지정 워크플로용 MDS(Master Data Services) 구성  
 사용자 지정 워크플로를 만들려면 사용자 지정 코드를 일부 작성하고 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]가 워크플로 데이터를 사용자 워크플로 처리기로 전달하도록 구성해야 합니다. 사용자 지정 워크플로 처리를 사용하려면 다음 단계를 수행하십시오.  
  
1.  <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender>를 구현하는 .NET 어셈블리를 만듭니다.  
  
2.  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 데이터베이스에 연결하고 사용자 워크플로 처리기에 태그를 연결하기 위해 SQL Server MDS Workflow Integration Service를 구성합니다.  
  
3.  SQL Server MDS Workflow Integration Service를 시작합니다.  
  
4.  [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]에서 사용자 워크플로 처리기의 이름으로 태그가 지정된 워크플로를 시작하는 비즈니스 규칙을 만듭니다.  
  
5.  사용자 지정 워크플로를 트리거하는 멤버에 비즈니스 규칙을 적용합니다.  
  
### <a name="create-the-workflow-handler-assembly"></a>워크플로 처리기 어셈블리 만들기  
 사용자 지정 워크플로는 <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender> 인터페이스를 구현하는 .NET 클래스 라이브러리 어셈블리입니다. SQL Server MDS Workflow Integration Service는 <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A> 메서드를 호출하여 사용자 코드를 실행합니다. <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A>를 구현하는 예제 코드는 [사용자 지정 워크플로 예제&#40;Master Data Services&#41;](../../master-data-services/develop/create-a-custom-workflow-example.md)를 참조하세요.  
  
 Visual Studio 2010을 사용하여 사용자 지정 워크플로를 처리하기 위해 SQL Server MDS Workflow Integration Service가 호출할 수 있는 어셈블리를 만들려면 다음 단계를 수행하십시오.  
  
1.  Visual Studio 2010에서 원하는 언어를 사용하는 새 **클래스 라이브러리** 프로젝트를 만듭니다. C# 클래스 라이브러리를 만들려면 **Visual C#\Windows** 프로젝트 형식을 선택하고 **클래스 라이브러리** 템플릿을 선택합니다. 프로젝트 이름(예: **MDSWorkflowTest**)을 입력하고 **확인**을 클릭합니다.  
  
2.  Microsoft.MasterDataServices.WorkflowTypeExtender.dll에 대한 참조를 추가합니다. 이 어셈블리는 \<설치 폴더>\Master Data Services\WebApplication\bin에 있습니다.  
  
3.  'using Microsoft.MasterDataServices.Core.Workflow;'를 C# 코드 파일에 추가합니다.  
  
4.  클래스 선언에 있는 <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender>에서 상속합니다. 클래스 선언 유사 해야 합니다. ' public class WorkflowTester: IWorkflowTypeExtender'.  
  
5.  <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender> 인터페이스를 구현합니다. SQL Server MDS Workflow Integration Service가 <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A> 메서드를 호출하여 워크플로를 시작합니다.  
  
6.  \<설치 폴더>\Master Data Services\WebApplication\bin에 있는 SQL Server MDS Workflow Integration Service 실행 파일인 Microsoft.MasterDataServices.Workflow.exe의 위치로 어셈블리를 복사합니다.  
  
### <a name="configure-sql-server-mds-workflow-integration-service"></a>SQL Server MDS Workflow Integration Service 구성  
 다음 단계에 따라 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 구성 파일을 편집하여 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 데이터베이스에 대한 연결 정보를 포함하고 사용자 워크플로 처리기 어셈블리에 태그를 연결하십시오.  
  
1.  \<설치 폴더>\Master Data Services\WebApplication\bin에서 Microsoft.MasterDataServices.Workflow.exe.config를 찾습니다.  
  
2.  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 데이터베이스 연결 정보를 "ConnectionString" 설정에 추가합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치에 대/소문자 구분 데이터 정렬이 사용되는 경우에는 데이터베이스에 사용된 것과 동일하게 대/소문자를 구분하여 데이터베이스 이름을 입력해야 합니다. 예를 들어, 완전한 설정 태그는 다음과 같습니다.  
  
    ```xml  
    <setting name="ConnectionString" serializeAs="String">  
        <value>Server=myServer;Database=myDatabase;Integrated Security=True</value>  
    </setting>  
    ```  
  
3.  "ConnectionString" 설정 아래에 "WorkflowTypeExtenders" 설정을 추가하여 사용자 워크플로 처리기 어셈블리에 태그 이름을 연결합니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
    ```xml  
    <setting name="WorkflowTypeExtenders" serializeAs="String">  
        <value>TEST=MDSWorkflowTestLib.WorkflowTester, MDSWorkflowTestLib</value>  
    </setting>  
    ```  
  
     \<value> 태그의 내부 텍스트 형식은 \<Workflow tag>=\<assembly-qualified workflow type name>입니다. \<Workflow tag>는 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]에서 비즈니스 규칙을 만들 때 워크플로 처리기 어셈블리를 식별하는 데 사용하는 이름입니다. \<assembly-qualified workflow type name>은 워크플로 클래스의 네임스페이스로 한정된 이름, 쉼표, 어셈블리의 표시 이름을 차례로 입력한 것입니다. 어셈블리가 강력한 이름으로 지정되어 있는 경우 버전 정보와 해당 PublicKeyToken도 포함해야 합니다. 서로 다른 워크플로에 대해 여러 워크플로 처리기를 만든 경우 여러 \<setting> 태그를 포함할 수 있습니다.  
  
> [!NOTE]  
>  서버 구성에 따라 Microsoft.MasterDataServices.Workflow.exe.config 파일을 저장할 때 "액세스가 거부되었습니다." 오류가 표시될 수 있습니다. 이 경우 서버에서 UAC(사용자 계정 컨트롤)를 일시적으로 비활성화하십시오. 이렇게 하려면 제어판을 열고 **시스템 및 보안**을 클릭합니다. **알림 센터**에서 **사용자 계정 컨트롤 설정 변경**을 클릭합니다. **사용자 계정 컨트롤 설정** 대화 상자에서 알림을 받지 않도록 막대를 맨 아래로 이동합니다. 컴퓨터를 다시 시작하고 이전 단계를 반복하여 구성 파일을 편집합니다. 파일을 저장한 후 UAC 설정을 기본 수준으로 다시 설정합니다.  
  
### <a name="start-sql-server-mds-workflow-integration-service"></a>SQL Server MDS Workflow Integration Service 시작  
 기본적으로 SQL Server MDS Workflow Integration Service는 설치되지 않습니다. 이 서비스를 사용하려면 먼저 서비스를 설치해야 합니다. 보안성을 높이려면 서비스의 로컬 사용자를 만들고 이 사용자에게 워크플로 작업을 수행하는 데 필요한 사용 권한만 부여해야 합니다. 사용자를 만들고, 서비스를 설치하고, 서비스를 시작하려면 다음 단계를 수행하십시오.  
  
1.  로컬 사용자 및 그룹 관리자를 사용하여 mds_workflow_service와 같은 이름이 지정된 로컬 사용자를 만듭니다.  
  
2.  SQL Server Management Studio를 사용하여 mds_workflow_service 사용자에게 [mdm].[udpExternalActionsGet] 저장 프로시저를 실행하는 데 필요한 사용 권한을 부여합니다. 이렇게 하려면 mds_workflow_service 계정을 위한 새 로그인을 만들고, [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 데이터베이스에서 새 사용자를 만들고, 이 사용자를 mds_workflow_service 로그인에 매핑하고, 이 사용자에게 [mdm].[udpExternalActionsGet] 저장 프로시저에 대한 EXECUTE 권한을 부여합니다.  
  
3.  mds_workflow_service 사용자에게 워크플로 처리기 어셈블리를 실행하기 위한 사용 권한을 부여합니다. 이렇게 하려면 mds_workflow_service 사용자를 워크플로 처리기 어셈블리의 **속성**에 대한 **보안** 탭에 추가하고 mds_workflow_service 사용자에게 READ 및 EXECUTE 권한을 부여합니다.  
  
4.  mds_workflow_service 사용자에게 SQL Server MDS Workflow Integration Service 실행 파일을 실행하기 위한 사용 권한을 부여합니다. 이렇게 하려면 mds_workflow_service 사용자를 \<설치 폴더>\Master Data Services\WebApplication\bin에 있는 Microsoft.MasterDataServices.Workflow.exe의 **속성**에 대한 **보안** 탭에 추가하고 mds_workflow_service 사용자에게 READ 및 EXECUTE 권한을 부여합니다.  
  
5.  InstallUtil.exe라는 .NET 설치 유틸리티를 사용하여 SQL Server MDS Workflow Integration Service를 설치합니다. InstallUtil.exe는 .NET 설치 폴더(예: C:\Windows\Microsoft.NET\Framework\v4.0.30319\\)에 있습니다. 높은 권한의 명령 프롬프트에 다음을 입력하여 SQL Server MDS Workflow Integration Service를 설치합니다.  
  
    ```  
    C:\Windows\Microsoft.NET\Framework\v4.0.30319\InstallUtil Microsoft.MasterDataServices.Workflow.exe  
    ```  
  
     설치하는 동안 메시지가 표시되면 mds_workflow_service 사용자를 지정합니다.  
  
6.  서비스 스냅인을 사용하여 SQL Server MDS Workflow Integration Service를 시작합니다. 이렇게 하려면 서비스 스냅인에서 SQL Server MDS Workflow Integration Service를 찾아 선택하고 **시작** 링크를 클릭합니다.  
  
### <a name="create-a-workflow-business-rule"></a>워크플로 비즈니스 규칙 만들기  
 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]를 사용하여 적용 시 워크플로를 시작하는 비즈니스 규칙을 만들고 게시할 수 있습니다. 이때 비즈니스 규칙에 특성 값을 변경하는 동작을 포함하여 규칙이 한 번 적용된 후 False가 되게 해야 합니다. 예를 들어, Price 특성 값이 500보다 크고 Approved 특성 값이 비어 있을 때 비즈니스 규칙이 True가 되는 경우 규칙에 Approved 특성 값을 Pending으로 설정하는 동작과 워크플로를 시작하는 동작을 포함할 수 있습니다. "이(가) 변경된 경우" 조건을 사용하고 추적 그룹을 변경하기 위해 사용자 특성을 추가하는 규칙을 만들 수도 있습니다. 비즈니스 규칙에 대한 자세한 내용은 [비즈니스 규칙&#40;Master Data Services&#41;](../../master-data-services/business-rules-master-data-services.md)을 참조하세요.  
  
 다음 단계를 수행하여 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]에서 사용자 지정 워크플로를 시작하는 비즈니스 규칙을 만드십시오.  
  
1.  [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]의 비즈니스 규칙 편집기에서 비즈니스 규칙의 조건을 지정한 후에 **외부 동작** 목록의 **워크플로 시작** 동작을 **THEN** 창의 **동작** 레이블로 끕니다.  
  
2.  **동작 편집** 창의 **워크플로 유형** 상자에 사용자 워크플로 처리기 어셈블리를 식별하는 태그를 입력합니다. 이 태그는 어셈블리의 구성 파일에 지정했던 태그(예: TEST)입니다.  
  
3.  필요에 따라 **멤버 데이터 포함** 확인란을 선택합니다. 워크플로 처리기에 전달되는 XML에 특성 이름 및 값을 포함하려면 이 확인란을 선택합니다.  
  
4.  **워크플로 사이트** 상자에 웹 사이트 이름을 입력합니다. 사용자 지정 워크플로의 경우 이 항목이 적용되지 않을 수 있지만 컨텍스트를 추가하기 위해 해당 항목을 사용할 수는 있습니다.  
  
5.  **워크플로 이름** 상자에 Visual Studio 워크플로 이름을 입력합니다. 사용자 지정 워크플로의 경우 이 항목이 적용되지 않을 수 있지만 컨텍스트를 추가하기 위해 해당 항목을 사용할 수는 있습니다.  
  
6.  비즈니스 규칙을 저장하고 게시합니다.  
  
### <a name="apply-business-rules-to-start-a-workflow"></a>비즈니스 규칙을 적용하여 워크플로 시작  
 워크플로를 시작하려면 데이터에 비즈니스 규칙을 적용해야 합니다. 이렇게 하려면 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]를 사용하여 유효성을 검사할 멤버가 포함된 엔터티를 편집하십시오. **비즈니스 규칙 적용**을 클릭합니다. [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]는 비즈니스 규칙에 대한 응답으로 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 데이터베이스의 Service Broker 큐를 채웁니다. SQL Server MDS Workflow Integration Service는 큐를 확인할 때 데이터를 지정된 워크플로 처리기 어셈블리로 보내고 큐를 지웁니다. 워크플로 처리기 어셈블리는 사용자가 작성한 코드에 따라 동작을 수행합니다.  
  
## <a name="troubleshoot-custom-workflows"></a>사용자 지정 워크플로 문제 해결  
 워크플로 처리기 어셈블리가 데이터를 받지 않는 경우 SQL Server MDS Workflow Integration Service를 디버깅하거나 Service Broker 큐를 볼 수 있습니다.  
  
### <a name="debug-sql-server-mds-workflow-integration-service"></a>SQL Server MDS Workflow Integration Service 디버깅  
 SQL Server Workflow Integration Service를 디버깅하려면 다음 단계를 수행하십시오.  
  
1.  서비스 스냅인을 사용하여 서비스를 중지합니다.  
  
2.  명령 프롬프트를 열고 서비스의 위치로 이동 입력 하 여 콘솔 모드에서 서비스를 실행 합니다. Microsoft.MasterDataServices.Workflow.exe -console.  
  
3.  [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]에서 멤버를 업데이트하고 비즈니스 규칙을 다시 적용합니다. 콘솔 창에 자세한 로그가 표시됩니다.  
  
### <a name="view-the-service-broker-queue"></a>Service Broker 큐 보기  
 워크플로의 일환으로 전달되는 마스터 데이터가 포함된 Service Broker 큐는 mdm.microsoft/mdm/queue/externalaction입니다. 큐는 SQL Management Studio의 **개체 탐색기**에서 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 데이터베이스의 Service Broker 노드에 있습니다. 이때 서비스가 큐를 제대로 지우면 이 큐가 비게 됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [사용자 지정 워크플로 예제&#40;Master Data Services&#41;](../../master-data-services/develop/create-a-custom-workflow-example.md)   
 [사용자 지정 워크플로 XML 설명&#40;Master Data Services&#41;](../../master-data-services/develop/create-a-custom-workflow-xml-description.md)  
  
  
