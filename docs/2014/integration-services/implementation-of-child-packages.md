---
title: 자식 패키지 구현 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- child packages
ms.assetid: ab0c09d7-ce2e-487d-a1ed-a4b5adb6cc01
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 04ad145d23cfcd158cf68ac941606e1c3bd0114a
ms.sourcegitcommit: aa4f594ec6d3e85d0a1da6e69fa0c2070d42e1d8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2019
ms.locfileid: "59242171"
---
# <a name="implementation-of-child-packages"></a>자식 패키지 구현
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]를 사용하여 로그 균형 조정을 구현하면 사용 가능한 CPU 또는 서버 시간을 사용할 다른 서버에 자식 패키지가 설치됩니다. 자식 패키지를 만들고 실행하려면 다음 단계를 수행하십시오.  
  
-   자식 패키지 디자인  
  
-   원격 서버로 패키지 이동  
  
-   자식 패키지를 실행하는 단계가 포함된 원격 서버에 SQL Server 에이전트 작업 만들기  
  
-   SQL Server 에이전트 작업 및 자식 패키지 테스트와 디버깅  
  
 자식 패키지를 디자인하는 경우 패키지를 디자인하는 데 제한이 없으므로 원하는 모든 기능을 제공할 수 있습니다. 그러나 패키지에서 데이터에 액세스하는 경우 해당 데이터에 액세스할 권한이 패키지를 실행하는 서버에 있어야 합니다.  
  
 자식 패키지를 실행하는 부모 패키지를 확인하려면 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 의 솔루션 탐색기에서 패키지를 마우스 오른쪽 단추로 클릭한 다음 **진입점 패키지**를 클릭합니다.  
  
 자식 패키지가 디자인되면 원격 서버에 해당 패키지를 배포합니다.  
  
## <a name="moving-the-child-package-to-the-remote-instance"></a>원격 인스턴스로 자식 패키지 이동  
 여러 가지 방법으로 패키지를 다른 서버로 이동할 수 있는데 그 중 다음 두 가지 방법이 권장됩니다.  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]를 사용하여 패키지를 내보냅니다.  
  
-   배포할 패키지를 포함하는 프로젝트의 배포 유틸리티를 작성한 다음 패키지를 파일 시스템 또는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스에 설치하기 위해 패키지 설치 마법사를 실행하여 패키지를 배포합니다. 자세한 내용은 [패키지 배포 &#40;SSIS&#41;](packages/legacy-package-deployment-ssis.md)합니다.  
  
 사용할 원격 서버마다 배포를 반복하여 수행해야 합니다.  
  
## <a name="creating-the-sql-server-agent-jobs"></a>SQL Server 에이전트 작업 만들기  
 자식 패키지가 여러 서버에 배포되면 자식 패키지가 포함된 서버마다 SQL Server 에이전트 작업을 만듭니다. SQL Server 에이전트 작업에는 작업 에이전트 호출 시 자식 패키지를 실행하는 단계가 포함됩니다. SQL Server 에이전트 작업은 예약된 작업이 아니며 부모 패키지에서 호출 시에만 자식 패키지를 실행합니다. 부모 패키지로 다시 전달되는 작업 성공 또는 실패 알림은 자식 패키지의 성공 또는 실패나 실행 여부가 아니라 SQL Server 에이전트 작업의 성공 또는 실패와 호출 성공 여부를 반영합니다.  
  
## <a name="debugging-the-sql-server-agent-jobs-and-child-packages"></a>SQL Server 에이전트 작업 및 자식 패키지 디버깅  
 다음 방법 중 하나를 사용하여 SQL Server 에이전트 작업 및 해당 자식 패키지를 테스트할 수 있습니다.  
  
-   **디버그** / **디버깅하지 않고 시작**을 클릭하여 SSIS 디자이너에서 각 자식 패키지를 실행합니다.  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]를 사용하여 원격 컴퓨터에서 개별 SQL Server 에이전트 작업을 실행하여 패키지가 실행되는지 확인합니다.  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에이전트 작업에서 실행한 패키지의 문제를 해결하는 방법은 [지원 기술 자료에서](https://support.microsoft.com/kb/918760) SQL Server 에이전트 작업 단계에서 SSIS 패키지를 호출할 때 SSIS 패키지가 실행하지 않는다 [!INCLUDE[msCoName](../includes/msconame-md.md)] 를 참조하십시오.  
  
 SQL Server 에이전트는 프록시에 대한 하위 시스템 액세스 권한을 확인하고 작업 단계가 실행될 때마다 프록시에 대한 액세스 권한을 부여합니다.  
  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 프록시를 만들 수 있습니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
-   [SQL Server Management Studio를 사용하여 SSIS 서버에서 패키지 실행](run-a-package-on-the-ssis-server-using-sql-server-management-studio.md)  
  
## <a name="related-content"></a>관련 내용  
  
-   블로그 항목, [SSIS: 부모 패키지의 변수 액세스](https://andyleonard.blog/2015/08/ssis-design-pattern-access-parent-variables-from-a-child-package-in-the-ssis-catalog/), andyleonard.blog에 있습니다.  
  
-   문서 [패키지 실행 태스크](../integration-services/control-flow/execute-package-task.md)합니다.  
  
  
