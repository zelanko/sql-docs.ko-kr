---
title: '1단원: 보고서 서버 프로젝트 만들기 | Microsoft Docs'
description: 이 단원에서는 보고서 디자이너를 사용하여 보고서 서버 프로젝트 및 보고서 정의(.rdl) 파일을 만듭니다.
ms.date: 12/09/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 675671ca-e6c9-48a2-82e9-386778f3a49f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ac84fb8cf355103b28fbac8f5411943aa4ee51a8
ms.sourcegitcommit: 22e97435c8b692f7612c4a6d3fe9e9baeaecbb94
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2020
ms.locfileid: "92679050"
---
# <a name="lesson-1-create-a-report-server-project-reporting-services"></a>1단원: 보고서 서버 프로젝트 만들기(Reporting Services)

이 단원에서는 ‘보고서 디자이너’를 사용하여 ‘보고서 서버 프로젝트’ 및 ‘보고서 정의(.rdl)’ 파일을 만듭니다.   

> [!NOTE]
> [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]는 비즈니스 인텔리전스 솔루션을 만들기 위한 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 환경입니다. SSDT에서는 페이지를 매긴 [!INCLUDE[ssrsnoversion_md](../includes/ssrsnoversion-md.md)] 보고서 정의, 공유 데이터 원본, 공유 데이터 세트 및 보고서 파트를 열고 수정하고 미리 보고 저장하고 배포할 수 있는 보고서 디자이너 제작 환경을 사용할 수 있습니다.

보고서 디자이너에서 보고서를 만들면, 보고서 파일과 보고서에 사용되는 기타 리소스 파일이 포함된 보고서 서버 프로젝트가 만들어집니다.

## <a name="to-create-a-report-server-project"></a>보고서 서버 프로젝트를 만들려면
  
1. **파일** 메뉴에서 **새로 만들기** > **프로젝트** 를 선택합니다.  

    ![파일 > 새로 만들기 > 프로젝트가 선택된 경우를 보여 주는 Visual Studio의 스크린샷](../reporting-services/media/ssrs-ssdt-file-01-new-project.png)
  
2. 맨 왼쪽 열의 **설치됨** 아래에서 **Reporting Services** 를 선택합니다. **비즈니스 인텔리전스** 그룹 아래에 표시되는 경우도 있습니다.

    ![Reporting Services가 선택되고 보고서 서버 프로젝트 템플릿이 강조 표시된 경우를 보여 주는 새 프로젝트 대화 상자의 스크린샷](../reporting-services/media/lesson-1-creating-a-report-server-project-reporting-services/select-report-server-project-template.png)

    > [!IMPORTANT]
    > VS에서 왼쪽 열에 Reporting Services가 표시되지 않는 경우, SSDT 워크로드를 설치하여 보고서 디자이너를 추가합니다. **도구** 메뉴에서 **도구 및 기능 가져오기...** 를 선택한 다음, 표시되는 워크로드에서 **SQL Server Data Tools** 를 선택합니다. 가운데 열에 Report Services 개체가 표시되지 않는 경우 Reporting Services 확장을 추가합니다. **도구** 메뉴에서 **확장 및 업데이트** > **온라인** 을 선택합니다. 가운데 열에 표시된 확장에서 **Microsoft Reporting Services Projects** > **다운로드** 를 선택합니다. SSDT의 경우 [SSDT(SQL Server Data Tools) 다운로드](../ssdt/download-sql-server-data-tools-ssdt.md)를 참조하세요. Visual Studio 2019에서 위의 단계가 작동하지 않는 경우 [Microsoft 보고 서비스 프로젝트 확장](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftReportProjectsforVisualStudio)을 설치해 보세요.


3. **새 프로젝트** 대화 상자의 가운데 열에서 **보고서 서버 프로젝트** 아이콘 &nbsp;&nbsp;![ssrs_ssdt_report_server_project](media/ssrs-ssdt-report-server-project.png)를 선택합니다.&nbsp;&nbsp;

4. **이름** 텍스트 상자에 프로젝트 이름으로 “Tutorial”을 입력합니다. 기본적으로, **위치** 텍스트 상자에는 "Documents\Visual Studio 20xx\Projects\" 폴더의 경로가 표시됩니다. 보고서 디자이너는 이 경로 아래에 Tutorial이라는 폴더를 만들고, 이 폴더에 Tutorial 프로젝트를 만듭니다. 프로젝트가 VS 솔루션에 속하지 않는 경우 VS도 솔루션 파일(.sln)을 만듭니다.

5. **확인** 을 선택하여 프로젝트를 만듭니다. 오른쪽의 **솔루션 탐색기** 창에 Tutorial 프로젝트가 표시됩니다.
  
## <a name="creating-a-report-definition-file-rdl"></a>보고서 정의 파일(RDL) 만들기  
  
1. **솔루션 탐색기** 창에서 **보고서** 폴더를 마우스 오른쪽 단추로 클릭합니다. **솔루션 탐색기** 창이 표시되지 않는 경우 **보기** 메뉴 > **솔루션 탐색기** 를 선택합니다.

2. **추가** > **새 항목** 을 선택합니다.

    ![보고서 > 추가 > 새 항목이 선택된 경우를 보여 주는 솔루션 탐색기의 스크린샷](../reporting-services/media/ssrs-ssdt-add-report.png)

3. **새 항목 추가** 창에서 **보고서** 아이콘을 선택합니다.

4. **이름** 텍스트 상자에 “Sales Orders.rdl”을 입력합니다.

5. **새 항목 추가** 대화 상자의 오른쪽 아래에 있는 **단추 추가** 를 선택하여 프로세스를 완료합니다. 보고서 디자이너가 열리고 Sales Orders 보고서 파일이 디자인 뷰에 표시됩니다.

    ![디자인 뷰의 보고서 디자이너 및 Sales Orders 보고서를 보여 주는 Visual Studio의 스크린샷](media/ssrs-ssdt-01-new-report-designer.png)

## <a name="next-steps"></a>다음 단계

지금까지 Tutorial 보고서 프로젝트와 Sales Orders 보고서를 만들었습니다. 나머지 단원에서는 다음 작업을 수행하는 방법을 알아보겠습니다.

- 보고서에 대한 데이터 원본 구성
- 데이터 원본에서 데이터 세트 만들기
- 보고서 레이아웃 디자인 및 서식 지정

[2단원: 연결 정보 지정 &#40;Reporting Services&#41;](../reporting-services/lesson-2-specifying-connection-information-reporting-services.md)에서 계속 진행하세요.
