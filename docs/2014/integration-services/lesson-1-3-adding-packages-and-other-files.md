---
title: '3단계: 패키지 및 기타 파일 추가 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: a7e6ec9c-d31d-4613-9525-8947a7b358f7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7db3e293c95b358d78e445e6b7534f90ea7b9310
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62892212"
---
# <a name="step-3-adding-packages-and-other-files"></a>3단계: 패키지 및 기타 파일 추가
  이 태스크에서는 기존 패키지, 개별 패키지를 지원하는 보조 파일 및 추가 정보를 이전 태스크에서 만든 Deployment Tutorial 프로젝트에 추가합니다. 예를 들어 패키지에 대한 데이터가 포함된 XML 데이터 파일과 프로젝트의 모든 패키지에 대한 추가 정보를 제공하는 텍스트 파일을 추가합니다.  
  
 패키지를 테스트 또는 프로덕션 환경에 배포할 경우 일반적으로 데이터 파일을 배포에 포함하는 대신에 데이터 파일 또는 데이터베이스의 테스트 또는 프로덕션 버전에 액세스하도록 구성을 사용하여 데이터 원본의 경로를 업데이트합니다. 지침을 제공하기 위해 이 자습서에는 패키지 배포에 데이터 파일이 포함되어 있습니다.  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 예제를 설치하면 패키지 및 패키지가 사용하는 예제 데이터가 설치됩니다. 다음 패키지를 Deployment Tutorial 프로젝트에 추가합니다.  
  
-   **DataTransfer.** 플랫 파일에서 데이터를 추출하고 데이터 세트의 행을 조건부로 유지하기 위해 열 값을 평가하며 AdventureWorks 데이터베이스의 테이블에 데이터를 로드하는 기본 패키지입니다.  
  
-   **LoadXMLData.** XML 데이터 파일에서 데이터를 추출하고 열 값을 평가 및 집계하며 AdventureWorks 데이터베이스의 테이블에 데이터를 로드하는 데이터 전송 패키지입니다.  
  
 이러한 패키지의 배포를 지원하기 위해 다음 보조 파일을 Deployment Tutorial 프로젝트에 추가합니다.  
  
|패키지|파일|  
|-------------|----------|  
|DataTransfer|NewCustomers.txt|  
|LoadXMLData|orders.xml 및 orders.xsd|  
  
 또한 Deployment Tutorial 프로젝트에 대한 정보를 제공하는 텍스트 파일인 추가 정보 파일을 추가합니다.  
  
 다음 절차에 사용되는 경로에서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 예제가 기본 위치인 [!INCLUDE[ssSampPathIS](../includes/sssamppathis-md.md)]에 설치되었다고 가정합니다. 예제를 다른 위치에 설치한 경우 절차에서 해당 위치를 사용해야 합니다.  
  
 다음 태스크에서는 DataTransfer 및 LoadXMLData 패키지에 구성을 추가합니다. 모든 구성은 XML 파일에 저장되며 시스템 환경 변수를 사용하여 파일의 위치를 지정합니다. 구성 파일을 만든 후에 프로젝트에 추가합니다.  
  
### <a name="to-add-packages-to-the-deployment-tutorial-project"></a>Deployment Tutorial 프로젝트에 패키지를 추가하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 를 아직 열지 않은 경우 **시작**을 클릭하고 **모든 프로그램**, **Microsoft SQL Server**를 차례로 가리킨 다음 **SQL Server Data Tools**를 클릭합니다.  
  
2.  **파일** 메뉴에서 **열기**, **프로젝트/솔루션**, **Deployment Tutorial** 폴더, **열기**를 차례로 클릭한 다음 **Deployment Tutorial.sln**을 두 번 클릭합니다.  
  
3.  솔루션 탐색기에서 Deployment Tutorial을 마우스 오른쪽 단추로 클릭하고 **추가**를 클릭한 다음 **기존 패키지**를 클릭합니다.  
  
4.  **기존 패키지의 복사본 추가** 대화 상자의 **패키지 위치**에서 **파일 시스템**을 선택합니다.  
  
5.  찾아보기 단추 **(...)** 를 클릭하고 C:\Program Files\Microsoft SQL Server\100\Samples\Integration ServicesTutorial\Deploying Packages\Completed Packages로 이동하여 **DataTransfer.dtsx**를 선택한 다음, **열기**를 클릭합니다.  
  
6.  **확인**을 클릭합니다.  
  
7.  3-6단계를 반복하되 이번에는 C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services\Tutorial\Deploying Packages\Completed Packages에 있는 LoadXMLData.dtsx를 추가합니다.  
  
### <a name="to-add-ancillary-files-to-the-deployment-tutorial-project"></a>Deployment Tutorial 프로젝트에 보조 파일을 추가하려면  
  
1.  솔루션 탐색기에서 Deployment Tutorial을 마우스 오른쪽 단추로 클릭하고 **추가**를 클릭한 다음 **기존 항목**을 클릭합니다.  
  
2.  **기존 항목 추가 - Deployment Tutorial** 대화 상자에서 C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services\Tutorial\Deployment Packages\Sample Data로 이동하여 orders.xml, orders.xsd 및 NewCustomers.txt를 선택한 다음 **추가**를 클릭합니다.  
  
3.  **기존 항목 추가 - Deployment Tutorial** 대화 상자에서 C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services\Tutorial\Deployment Packages\\로 이동하여 Readme.txt를 선택한 다음 **추가**를 클릭합니다.  
  
4.  파일 메뉴에서 **모두 저장**을 클릭합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [4단계: 패키지 구성 추가](../integration-services/lesson-1-4-adding-package-configurations.md)  
  
![Integration Services 아이콘 (작은 아이콘)](media/dts-16.gif "Integration Services 아이콘(작은 아이콘)")  **은 최신 상태로 유지 Integration Services**<br /> Microsoft의 최신 다운로드, 문서, 예제 및 비디오와 커뮤니티에서 선택된 솔루션을 보려면 MSDN의 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 페이지를 방문하세요.<br /><br /> [MSDN의 Integration Services 페이지 방문](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 이러한 업데이트에 대한 자동 알림을 받으려면 해당 페이지에서 제공하는 RSS 피드를 구독하십시오.  
  
  
