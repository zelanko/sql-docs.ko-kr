---
title: '1단원: 보고서 서버 프로젝트 만들기(Reporting Services) | Microsoft Docs'
ms.date: 11/30/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 675671ca-e6c9-48a2-82e9-386778f3a49f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 741621c22d8abcc9420b40afa07f4707bc1418ae
ms.sourcegitcommit: b1990ec4491b5a8097c3675334009cb2876673ef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2018
ms.locfileid: "49383658"
---
# <a name="lesson-1-creating-a-report-server-project-reporting-services"></a>1단원: 보고서 서버 프로젝트 만들기(Reporting Services)

이 섹션에서는Visual Studio 내의 *에서* 보고서 서버 프로젝트 *및* 보고서 정의(.rdl) [!INCLUDE[ssBIDevStudio_md](../includes/ssbidevstudio-md.md)] 파일을 만듭니다. 

[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 보고서를 만들려면 먼저 보고서 정의 파일(.rdl) 및 보고서에 필요한 다른 리소스 파일을 저장할 수 있는 보고서 서버 프로젝트가 필요합니다. 

다음 단원에서는 실제 보고서 정의 파일을 만들고 보고서에 대한 데이터 원본, 데이터 집합 및 보고서 레이아웃을 정의합니다. 보고서를 실행하면 데이터가 검색되어 레이아웃과 결합된 후 화면에 렌더링됩니다. 여기에서 보고서를 내보내거나 인쇄하거나 저장할 수 있습니다.  
  
  
  
## <a name="to-create-a-report-server-project"></a>보고서 서버 프로젝트를 만들려면  
  
1.  [!INCLUDE[ssBIDevStudio_md](../includes/ssbidevstudio-md.md)]를 엽니다.  
  
2.  **파일** 메뉴 > **새로 만들기** > **프로젝트**를 클릭합니다.  

    ![ssrs-ssdt-file-01-new-project](../reporting-services/media/ssrs-ssdt-file-01-new-project.png)
  
3.  **설치됨** > **템플릿** > **비즈니스 인텔리전스**에서 **Reporting Services**를 클릭합니다.

    ![ssrs-ssdt-01-new-rs-project](../reporting-services/media/ssrs-ssdt-01-new-rs-project.png)

5. **보고서 서버 프로젝트** ![ssrs_ssdt_report_server_project](../reporting-services/media/ssrs-ssdt-report-server-project.png)를 클릭합니다. 

   >**참고**: **비즈니스 인텔리전스** 또는 **보고서 서버 프로젝트** 옵션이 표시되지 않는 경우 SSDT를 비즈니스 인텔리전스 템플릿으로 업데이트해야 합니다. [SSDT(SQL Server Data Tools) 다운로드](../ssdt/download-sql-server-data-tools-ssdt.md)를 참조하세요.  
  
5.  **이름**에 **Tutorial**을 입력합니다.  

    기본적으로 새 디렉터리에 Visual Studio 2015\Projects 폴더가 만들어집니다.
    
    ![ssrs-ssdt-01-solution-location](../reporting-services/media/ssrs-ssdt-01-solution-location.png)
  
6.  **확인** 을 클릭하여 프로젝트를 만듭니다.  
  
    오른쪽의 솔루션 탐색기 페이지에 Tutorial 프로젝트가 표시됩니다.  
  
## <a name="to-create-a-new-report-definition-file"></a>새 보고서 정의 파일을 만들려면  
  
1.  **솔루션 탐색기** 창에서 **보고서** > **추가** > **새 항목**을 마우스 오른쪽 단추로 클릭합니다. 

    >**팁**: **솔루션 탐색기** 창이 열리지 않은 경우 **보기** 메뉴에서 **솔루션 탐색기**를 클릭합니다. 

    ![ssrs_ssdt_add_report](../reporting-services/media/ssrs-ssdt-add-report.png)
  
2.  **새 항목 추가** 창에서 **보고서** ![ssrs_ssdt_report](../reporting-services/media/ssrs-ssdt-report.png)를 클릭합니다.  
  
3.  **이름**에 **Sales Orders.rdl** 을 입력한 후 **추가**를 클릭합니다.  
  
    보고서 디자이너가 열리고 새 .rdl 파일이 디자인 뷰에 표시됩니다.  
    
    ![ssrs-ssdt-01-new-report-designer](../reporting-services/media/ssrs-ssdt-01-new-report-designer.png)
  
     보고서 디자이너는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 에서 실행되는 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]구성 요소로, 두 개의 뷰, 즉 **디자인** 및 **미리 보기**뷰가 있습니다. 뷰를 변경하려면 각 탭을 클릭해야 합니다.  
  
    **보고서 데이터** 창에서 데이터를 정의합니다. **디자인** 뷰에서는 보고서 레이아웃을 정의합니다. 보고서를 실행하고 **미리 보기** 뷰에서 보고서의 모양을 볼 수 있습니다.  
  
## <a name="next-lesson"></a>다음 단원  
"Tutorial" 보고서 프로젝트를 만들고 보고서 정의 파일(.rdl)을 보고서 프로젝트에 추가했습니다. 다음 단원에서는 보고서에 사용할 데이터 원본을 지정합니다. [2단원: 연결 정보 지정&#40;Reporting Services&#41;](../reporting-services/lesson-2-specifying-connection-information-reporting-services.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[기본 테이블 보고서 만들기&#40;SSRS 자습서&#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)  
  

