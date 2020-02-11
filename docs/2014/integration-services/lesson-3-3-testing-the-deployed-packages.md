---
title: '3단계: 배포된 패키지 테스트 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 9159da3f-c9ca-4015-9e85-3bf4373a1349
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 92055ceb4226406fe26d7ce23491c81606f292c5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62891825"
---
# <a name="step-3-testing-the-deployed-packages"></a>3단계: 배포된 패키지 테스트
  이 태스크에서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스에 배포한 패키지를 테스트합니다.  
  
 다른 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 자습서에서는 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]디버그 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]메뉴의 **디버깅 시작** 옵션을 사용하여 **용 개발 환경인** 에서 패키지를 실행했습니다. 여기에서는 패키지를 다르게 실행합니다.  
  
 
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]는 테스트 및 프로덕션 환경에서 패키지를 실행하는 데 사용할 수 있는 명령 프롬프트 유틸리티 `dtexec` 및 패키지 실행 유틸리티와 같은 여러 도구를 제공합니다. 패키지 실행 유틸리티는 `dtexec`에서 작성된 그래픽 도구입니다. 이러한 두 도구는 모두 패키지를 즉시 실행합니다. 또한 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 는 SQL Server 에이전트 작업의 한 단계로 패키지 실행을 예약하기 위해 특별하게 디자인된 SQL Server 에이전트의 하위 시스템을 제공합니다.  
  
 패키지 실행 유틸리티를 사용하여 배포된 패키지를 실행할 수 있습니다. 패키지는 있는 그대로 사용됩니다. 따라서 대화 상자의 어떠한 페이지에서도 정보를 업데이트할 필요가 없습니다. 패키지 실행 유틸리티의 첫 번째 페이지인 일반 페이지에서 패키지를 실행합니다. 필요할 경우 다른 페이지를 클릭하여 각 패키지에 대해 포함된 정보를 볼 수 있습니다.  
  
> [!NOTE]  
>  이 자습서의 컨텍스트에서 패키지가 성공적으로 실행되도록 하려면 어떠한 옵션도 수정해서는 안 됩니다.  
  
 패키지 실행 유틸리티를 사용하여 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 에서 패키지를 실행하기 전에 Integration Services 서비스가 실행 중인지 확인합니다. Integration Services 서비스는 패키지 스토리지 및 실행을 위한 지원을 제공합니다. 이 서비스가 중지된 경우 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에 연결할 수 없으며 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 는 실행할 패키지를 나열하지 않습니다. 또한 패키지가 배포된 인스턴스에서 패키지를 실행할 수 있는 권한이 있어야 합니다. 자세한 내용은 [Integration Services 경로&#40;SSIS Service&#41;](security/integration-services-roles-ssis-service.md)를 참조하세요.  
  
 저장된 패키지 폴더 내의 최상위 폴더는 Integration Services 서비스가 모니터링하는 사용자 정의 폴더입니다. MsDtsSrvr.ini.xml 파일에서 많거나 적은 폴더를 원하는 대로 지정할 수 있습니다. 이 자습서에서는 기본 MsDtsSrvr.ini.xml 파일이 사용되고 있으며 저장된 패키지 내 최상위 폴더의 이름이 File System 및 MSDB라고 가정합니다.  
  
### <a name="to-connect-to-integration-services-in-sql-server-management-studio"></a>SQL Server Management Studio에서 Integration Services에 연결하려면  
  
1.  **시작**을 클릭하고 **모든 프로그램**, **Microsoft SQL Server**를 차례로 가리킨 다음 **SQL Server Management Studio**를 클릭합니다.  
  
2.  **서버에 연결** 대화 상자의 **서버 유형** 목록에서 **Integration Services** 를 선택하고 **서버 이름** 상자에 서버 이름을 입력한 다음 **연결**을 클릭합니다.  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]에 연결할 수 없으면 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스가 실행되고 있지 않는 것일 수 있습니다. 이 서비스의 상태를 확인하려면 **시작**을 클릭하고 **모든 프로그램**, **Microsoft SQL Server**, **구성 도구**를 차례로 가리킨 다음 **SQL Server 구성 관리자**를 클릭합니다. 왼쪽 창에서 **SQL Server 서비스**를 클릭하고 오른쪽 창에서 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스를 찾습니다. 서비스가 실행되지 않았으면 서비스를 시작합니다.  
  
     [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 가 열립니다. 기본적으로 개체 탐색기 창이 열리고 Studio의 오른쪽 상단 모서리에 위치합니다. 개체 탐색기가 열려 있지 않으면 **보기** 메뉴에서 **개체 탐색기** 를 클릭합니다.  
  
### <a name="to-run-the-packages-using-the-execute-package-utility"></a>패키지 실행 유틸리티를 사용하여 패키지를 실행하려면  
  
1.  개체 탐색기에서 저장된 패키지 폴더를 확장합니다.  
  
2.  MSDB 폴더를 확장합니다. 패키지를 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 배포했으므로 배포된 모든 패키지는 msdb [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스에 저장되고 MSDB 폴더에 표시됩니다. 패키지를 Deployment Tutorial 외부의 파일 시스템에 배포하지 않은 경우 File System 폴더는 비어 있습니다.  
  
3.  패키지 목록의 맨 위에서 시작하여 DataTransfer를 마우스 오른쪽 단추로 클릭하고 **패키지 실행**을 클릭합니다.  
  
4.  **패키지 실행 유틸리티** 대화 상자에서 **실행**을 클릭합니다.  
  
5.  **패키지 실행 유틸리티** 대화 상자에서 패키지의 진행률과 실행 결과를 확인합니다. **중지** 단추를 사용할 수 없게 되어 패키지가 완료되었다고 표시되면 **닫기**를 클릭합니다.  
  
    > [!IMPORTANT]  
    >  패키지가 실행되는 동안 **중지** 를 클릭할 경우 패키지가 완료되지 않습니다.  
  
6.  **패키지 실행 유틸리티** 대화 상자에서 **닫기**를 클릭합니다.  
  
7.  LoadXML 패키지에 대해 3 - 6단계를 반복합니다.  
  
8.  **파일** 메뉴에서 **끝내기**를 클릭합니다.  
  
### <a name="to-verify-the-results-of-the-datatransfer-package"></a>DataTransfer 패키지의 결과를 확인하려면  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]의 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
2.  **서버에 연결** 대화 상자의 **서버 유형** 목록에서 **데이터베이스 엔진** 을 선택하고 **서버 이름** 상자에 자습서 패키지를 설치한 서버의 이름을 제공하거나 (local)을 입력하고 인증 모드를 선택합니다. SQL Server 인증을 사용하는 경우 사용자 이름과 암호를 제공합니다.  
  
3.  **연결**을 클릭합니다.  
  
4.  쿼리 창에서 다음 SQL 문을 입력하거나 붙여 넣습니다.  
  
     `USE AdventureWorks`  
  
     `SELECT * FROM HighIncomeCustomers`  
  
5.  **F5** 키를 누르거나 도구 모음에서 실행 아이콘을 클릭합니다.  
  
     쿼리는 31개의 데이터 행을 반환합니다. 반환 결과에는 YearlyIncome 열의 100000보다 큰 값을 가지는 Customers.txt 텍스트 파일의 모든 행이 포함됩니다.  
  
6.  DeploymentTutorial 폴더를 찾아서 로그 XML 파일인 Deployment Tutorial Log를 마우스 오른쪽 단추로 클릭한 다음 **열기**를 클릭합니다. 메모장이나 원하는 텍스트/XML 편집기를 사용하여 파일을 열 수 있습니다.  
  
### <a name="to-verify-the-results-of-the-loadxmldata-package"></a>LoadXMLData 패키지의 결과를 확인하려면  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]의 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
2.  연결하라는 메시지가 다시 표시되면 **서버에 연결** 대화 상자의 **서버 유형** 목록에서 **데이터베이스 엔진** 을 선택하고 **서버 이름** 상자에 자습서 패키지를 설치한 서버의 이름을 제공하거나 (local)을 입력하고 인증 모드를 선택합니다. SQL Server 인증을 사용하는 경우 사용자 이름과 암호를 제공합니다.  
  
3.  **연결**을 클릭합니다.  
  
4.  쿼리 창에서 다음 SQL 문을 입력하거나 붙여 넣습니다.  
  
     `USE AdventureWorks`  
  
     `SELECT * FROM OrderDatesByCountryRegion`  
  
5.  **F5** 키를 누르거나 도구 모음에서 실행 아이콘을 클릭합니다.  
  
     쿼리는 21개의 데이터 행을 반환합니다. 반환 결과는 XML 데이터 파일 orders.xml의 행으로 구성됩니다. 각 행은 국가/지역별 요약이며 각 행에는 국가/지역의 이름, 각 국가/지역의 주문 수, 최신 주문과 가장 오래된 주문의 날짜가 나열됩니다.  
  
![Integration Services 아이콘 (작은 아이콘)](media/dts-16.gif "Integration Services 아이콘(작은 아이콘)")  **은 최신 상태로 유지 Integration Services**<br /> Microsoft의 최신 다운로드, 문서, 예제 및 비디오와 커뮤니티에서 선택된 솔루션을 보려면 MSDN의 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 페이지를 방문하세요.<br /><br /> [MSDN의 Integration Services 페이지 방문](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 이러한 업데이트에 대한 자동 알림을 받으려면 해당 페이지에서 제공하는 RSS 피드를 구독하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [dtexec 유틸리티](packages/dtexec-utility.md)  
  
  
