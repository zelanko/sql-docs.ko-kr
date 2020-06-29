---
title: '2단계: 패키지 설치 마법사 실행 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: f91fbb89-4626-4c47-b96d-56052dc45861
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b9565b6afa321081bd843d68dcecca4e4678da79
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85440530"
---
# <a name="step-2-running-the-package-installation-wizard"></a>2단계: 패키지 설치 마법사 실행
  이 태스크에서는 패키지 설치 마법사를 실행하여 Deployment Tutorial 프로젝트의 패키지를 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스에 배포합니다. 패키지만 msdb [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스의 sysssispackages 테이블에 설치할 수 있고 배포 번들에 포함된 지원 파일은 파일 시스템에 배포됩니다.  
  
 패키지 설치 마법사는 패키지를 설치하고 구성하는 단계를 안내합니다. 배포 번들을 복사한 컴퓨터인 대상 컴퓨터의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 패키지를 설치합니다. 또한 패키지가 아닌 파일을 마법사에서 설치하는 C:\DeploymentTutorialInstall 폴더를 만듭니다.  
  
 이전 단원에서는 구성을 사용하도록 자습서의 패키지를 수정했습니다. 설치되는 환경에서 패키지가 성공적으로 실행될 수 있도록 패키지 설치 마법사를 사용하여 이러한 구성을 편집합니다.  
  
### <a name="to-install-the-packages"></a>패키지를 설치하려면  
  
1.  대상 컴퓨터에서 배포 번들을 찾습니다.  
  
     배포 유틸리티의 위치로 기본값인 bin\Deployment를 사용한 경우 배포 번들은 Deployment Tutorial 프로젝트의 Deployment 폴더입니다.  
  
2.  Deployment 폴더에서 매니페스트 파일인 Deployment Tutorial.SSISDeploymentManifest를 두 번 클릭합니다.  
  
3.  패키지 설치 마법사 시작 페이지에서 **다음**을 클릭합니다.  
  
4.  SSIS 패키지 배포 페이지에서 **SQL Server 배포** 옵션을 선택하고 **설치 후 패키지 유효성 검사** 확인란을 선택한 후 **다음**을 클릭합니다.  
  
5.  대상 SQL Server 지정 페이지에서 **서버 이름**상자에 **(local)** 을 지정합니다.  
  
6.  SQL Server 인스턴스에서 Windows 인증이 지원될 경우에는 **Windows 인증 사용**을 선택하고 지원되지 않을 경우에는 **SQL Server 인증 사용** 을 선택하고 사용자 이름과 암호를 제공합니다.  
  
7.  **암호화에 서버 스토리지 사용** 확인란의 선택이 취소되었는지 확인합니다.  
  
8.  **다음**을 클릭합니다.  
  
9. 설치 폴더 선택 페이지에서 **찾아보기**를 클릭합니다.  
  
10. **폴더 찾아보기** 대화 상자에서 **내 컴퓨터** 를 확장한 다음 **로컬 디스크(C:)** 를 클릭합니다.  
  
11. **새 폴더 만들기** 를 클릭하고 새 폴더의 기본 이름인 **새 폴더**를 **DeploymentTutorialInstall**로 바꿉니다.  
  
    > [!IMPORTANT]  
    >  이 이름은 구성이 사용하는 환경 변수 값에서 참조됩니다. 폴더 이름과 참조가 일치해야 하며 그렇지 않으면 패키지를 실행할 수 없습니다.  
  
12. **확인**을 클릭합니다.  
  
13. 설치 폴더 선택 페이지에서 폴더 상자에 **C:\DeploymentTutorialInstall** 이 있는지 확인한 후 **다음**을 클릭합니다.  
  
14. 설치 확인 페이지에서 **다음**을 클릭합니다.  
  
     마법사는 패키지를 설치합니다. 설치가 완료된 후 패키지 구성 페이지가 열립니다.  
  
15. 패키지 구성 페이지에서 **구성 파일** 상자에 datatransferconfig.dtsconfig 및 loadxmldataconfig.dtsconfig가 나열되는지 확인합니다.  
  
16. **구성 파일** 목록에서 **datatransferconfig.dtsconfig**를 클릭하고 **구성** 상자의 **경로** 열에서 속성을 확장한 후 **값** 열을 다음 값으로 업데이트합니다.  
  
    |속성|값|업데이트된 값|  
    |--------------|-----------|-------------------|  
    |\Package.Connections[Deployment Tutorial Log].Properties[ConnectionString]|C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services\Tutorial\Deploying Packages\Completed Packages\Deployment Tutorial Log|C:\DeploymentTutorialInstall\Deployment Tutorial Log|  
    |\Package.Connections[NewCustomers].Properties[ConnectionString]|C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services\Tutorial\Deploying Packages\Sample Data\NewCustomers.txt|C:\DeploymentTutorialInstall\NewCustomers.txt|  
  
17. **구성 파일** 목록에서 loadxmldataconfig.dtsconfig를 클릭하고 **구성** 상자의 **경로** 열에서 속성을 확장한 후 **값** 열을 다음 값으로 업데이트합니다.  
  
    |속성|값|업데이트된 값|  
    |--------------|-----------|-------------------|  
    |\Package.LoadXMLData.Properties[[XML Source].[XMLData]]|C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services\Tutorial\Deploying Packages\Sample Data\orders.xml|C:\DeploymentTutorialInstall\orders.xml|  
    |\Package.LoadXMLData.Properties[[XML Source].[XMLSchemaDefinition]]|C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services\Tutorial\Deploying Packages\Sample Data\orders.xsd|C:\DeploymentTutorialInstall\orders.xsd|  
  
18. 패키지 유효성 검사 페이지에서 설치된 각 패키지의 유효성 검사 결과를 확인한 후 **다음**을 클릭합니다.  
  
     대상 컴퓨터의 환경 변수 값이 개발 컴퓨터의 환경 변수 값과 다르므로 패키지 유효성 검사 페이지에 여러 경고가 표시됩니다. 다음 4개의 경고를 예상해야 합니다.  
  
    -   구성 파일 "C:\DeploymentTutorial\DataTransferConfig.dtsConfig"가 유효하지 않습니다. 구성 파일 이름을 확인하십시오.  
  
    -   패키지에 대한 구성 항목을 적어도 하나 이상 로드하지 못했습니다. 구성 항목과 이전 경고를 검사하여 실패한 구성에 대한 설명을 확인하십시오.  
  
    -   구성 파일 "C:\DeploymentTutorial\LoadXMLDataConfig.dtsConfig"가 유효하지 않습니다. 구성 파일 이름을 확인하십시오.  
  
    -   패키지에 대한 구성 항목을 적어도 하나 이상 로드하지 못했습니다. 구성 항목과 이전 경고를 검사하여 실패한 구성에 대한 설명을 확인하십시오.  
  
     이러한 경고는 패키지 설치에 영향을 주지 않습니다.  
  
     SSIS 패키지 배포 페이지에서 **설치 후 패키지 유효성 검사** 옵션을 선택하지 않은 경우 패키지 유효성 검사 페이지가 열리지 않고 유효성 검사에 대한 사후 설치 정보가 표시되지 않습니다.  
  
19. 패키지 설치 마법사 마침 페이지에서 설치 요약을 읽은 다음 **마침**을 클릭합니다.  
  
    > [!NOTE]  
    >  패키지 유효성 검사에 사용되는 임시 로그 파일이 생성됩니다. 이 파일은 패키지가 실행될 때 사용되지 않습니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [3단계: 배포된 패키지 테스트](../integration-services/lesson-3-3-testing-the-deployed-packages.md)  
  
![Integration Services 아이콘 (작은 아이콘)](media/dts-16.gif "Integration Services 아이콘(작은 아이콘)")  **은 최신 상태로 유지 Integration Services**<br /> Microsoft의 최신 다운로드, 문서, 예제 및 비디오와 커뮤니티에서 선택된 솔루션을 보려면 MSDN의 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 페이지를 방문하세요.<br /><br /> [MSDN의 Integration Services 페이지를 방문하세요.](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 이러한 업데이트에 대한 자동 알림을 받으려면 해당 페이지에서 제공하는 RSS 피드를 구독하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SSIS 서비스 &#40;Integration Services 서비스&#41;](service/integration-services-service-ssis-service.md)   
 [Integration Services 서비스 관리](../../2014/integration-services/manage-the-integration-services-service.md)  
  
  
