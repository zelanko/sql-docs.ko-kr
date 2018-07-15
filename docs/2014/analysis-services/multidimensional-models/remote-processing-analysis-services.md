---
title: 원격 처리 (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d58bcb3c-0b3f-4ab0-81eb-4fdcc86153af
caps.latest.revision: 4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: eddc902acb9d3e1d2339f9d8efe2c62a9c07ad54
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37274149"
---
# <a name="remote-processing-analysis-services"></a>원격 처리(Analysis Services)
  원격 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 대해 예약된 처리 또는 무인 모드 처리를 실행할 수 있습니다. 여기서 처리 요청은 한 컴퓨터에서 시작되지만 동일한 네트워크상의 다른 컴퓨터에서 실행됩니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
  
-   각 컴퓨터에서 서로 다른 버전의 SQL Server를 실행하는 경우 클라이언트 라이브러리는 모델을 처리하는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 버전과 일치해야 합니다. 예를 들어 처리가 [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] 인스턴스에서 수행되는 경우 요청이 시작되는 컴퓨터에는 [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)]에 해당하는 클라이언트 라이브러리가 있어야 합니다. [Analysis Services 연결에 사용되는 데이터 공급자](../instances/data-providers-used-for-analysis-services-connections.md)를 참조하세요.  
  
-   원격 서버에서 **이 컴퓨터에 대한 원격 연결 허용** 을 사용해야 하고 처리 요청을 실행하는 계정이 허용된 사용자로 나열되어야 합니다.  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 대한 인바운드 연결을 허용하도록 Windows 방화벽 규칙을 구성해야 합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 를 사용하여 원격 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]인스턴스에 연결할 수 있는지 확인합니다. [Configure the Windows Firewall to Allow Analysis Services Access](../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)을 참조하세요.  
  
-   원격 처리를 시도하기 전에 모든 기존 로컬 처리 오류를 해결합니다. 처리 요청이 로컬인 경우 외부 관계형 데이터 원본에서 데이터를 검색할 수 있는지 확인합니다. 데이터 검색에 사용되는 자격 증명 지정에 대한 지침은 [가장 옵션 설정&#40;SSAS - 다차원&#41;](set-impersonation-options-ssas-multidimensional.md)을 참조하세요.  
  
## <a name="on-demand-remote-processing"></a>요청 시 원격 처리  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 관리자 권한이 있는 사용자 또는 응용 프로그램 계정의 처리 요청을 수락합니다. 관리자인 경우 원격 인스턴스에 연결하고 원격 연결을 통해 데이터베이스를 수동으로 처리할 수 있는지 확인하세요.  
  
1.  처리를 예약하는 데 사용할 컴퓨터에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 시작하고 원격 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 연결합니다.  
  
2.  데이터베이스를 마우스 오른쪽 단추로 클릭하고 **처리**를 선택한 후 **스크립트** 를 가리키고 **새 쿼리 창 동작 스크립팅**을 선택합니다. 처리를 호출하는 데 사용되는 명령이 쿼리 창에 나타납니다.  
  
3.  **확인** 을 클릭하여 처리를 시작합니다.  
  
     이 작업이 완료되면 예약된 작업에 포함할 수 있는 XMLA 쿼리가 제공됩니다. 또한 연결 문제가 없는지 확인합니다.  
  
## <a name="schedule-remote-processing-using-sql-server-agent-service"></a>SQL Server 에이전트 서비스를 사용하여 원격 처리 예약  
 기본적으로 SQL Server 에이전트 서비스는 컴퓨터 계정을 사용하여 설정된 네트워크 연결을 통해 가상 계정으로 실행됩니다. 컴퓨터 계정에 원격 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 대한 관리 권한을 부여하지 않으려면 SQL Server 에이전트 서비스 계정을 최소 권한 도메인 사용자 계정으로 실행되도록 변경해야 합니다.  
  
 **sysadmin** 계정에 서비스를 제공하는 데이터베이스 엔진 인스턴스에 대한 권한을 부여하는 것을 비롯하여 필요한 모든 권한을 부여해야 합니다.  
  
 다음 링크를 사용하여 권한을 설정하세요.  
  
-   [SQL Server 에이전트 구성](../../ssms/agent/configure-sql-server-agent.md)  
  
-   [SQL Server Agent Components](../../ssms/agent/sql-server-agent.md#Components) 는 **sysadmin** 권한을 부여하는 것이 불가능한 경우 대체 고정 서버 역할을 제안합니다.  
  
 계정 권한을 구성한 후 다음 단계를 계속하세요.  
  
#### <a name="grant-the-sql-server-agent-account-administrator-permission-on-ssas"></a>SSAS에 대한 SQL Server 에이전트 계정 관리자 권한 부여  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]를 사용하여 원격 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 연결합니다.  
  
2.  서버 이름을 마우스 오른쪽 단추로 클릭하고**속성**을 클릭한 후 **보안**을 클릭합니다.  
  
3.  **추가** 를 클릭하여 SQL Server 에이전트 계정을 추가합니다.  
  
#### <a name="create-the-job"></a>작업 만들기  
  
1.  Management Studio에서 로컬 데이터베이스 엔진 인스턴스에 연결합니다. SQL Server 에이전트는 개체 탐색기의 마지막 항목입니다. 필요한 경우 서비스를 시작합니다.  
  
2.  **작업**을 마우스 오른쪽 단추로 클릭하고 **새 작업** 을 클릭한 후 이름을 입력합니다.  
  
3.  단계에서 **새로 만들기** 를 클릭한 후 이름을 입력합니다.  
  
4.  유형에서 **SQL Server Analysis Services 명령**을 선택합니다.  
  
5.  서버에 원격 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 이름을 입력합니다.  
  
6.  명령에 데이터베이스를 처리하기 위한 XMLA 명령을 붙여넣습니다. 이 명령은 요청 시 원격 처리에 대한 확인 단계에서 생성한 XMLA 스크립트입니다. **확인** 을 클릭하여 작업을 저장합니다.  
  
#### <a name="start-sql-server-profiler"></a>SQL Server Profiler 시작  
  
1.  원격 컴퓨터에서 SQL Server Profiler를 시작합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 연결하고 **실행** 을 클릭하여 기본 이벤트를 사용한 추적을 시작합니다.  
  
     SQL Server Profiler를 사용하여 처리 이벤트를 발생하는 대로 모니터링합니다.  
  
2.  선택적으로 파일 또는 데이터베이스의 테이블로 추적을 보내도록 추적 속성을 설정할 수 있습니다.  
  
#### <a name="run-the-job"></a>작업 실행  
  
1.  작업을 실행하는 데 사용되는 컴퓨터에서 작업이 기본 작업을 수행할 수 있는지 확인합니다. 개체 탐색기의 SQL Server 에이전트에서 **작업**을 확장하고 방금 만든 작업을 마우스 오른쪽 단추로 클릭한 후 **작업 시작 단계**를 클릭합니다. 작업이 즉시 시작됩니다. SQL Server Profiler에서 진행률을 모니터링할 수 있습니다.  
  
2.  마지막 단계로, 정의하는 일정으로 실행되도록 작업을 수정하고 작업을 관리하는 데 필요한 경고 또는 알림을 추가합니다. 또한 처리 스크립트를 구체화하거나 개체를 독립적으로 처리하기 위해 작업에 여러 단계를 만들 수도 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 에이전트 구성 요소](../../ssms/agent/sql-server-agent.md#Components)   
 [SQL Server 에이전트를 사용 하 여 SSAS 관리 태스크 예약](../instances/schedule-ssas-administrative-tasks-with-sql-server-agent.md)   
 [일괄 처리 &#40;Analysis Services&#41;](batch-processing-analysis-services.md)   
 [다차원 모델 개체 처리](processing-a-multidimensional-model-analysis-services.md)   
 [개체 처리 &#40;XMLA&#41;](../xmla/xml-elements-objects.md)  
  
  
