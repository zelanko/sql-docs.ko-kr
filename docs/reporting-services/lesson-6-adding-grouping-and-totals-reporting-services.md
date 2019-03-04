---
title: '6단원: 그룹화 및 합계 추가(Reporting Services) | Microsoft Docs'
ms.date: 05/23/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: e3d61228-2aa4-42cc-955e-602dbf3406a7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 24d21ae735b44a7068ca929515b66e8a33aade8d
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56290081"
---
# <a name="lesson-6-adding-grouping-and-totals-reporting-services"></a>6단원: 그룹화 및 합계 추가(Reporting Services)
이 자습서 단원에서는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 보고서에 그룹화 및 합계를 추가하여 데이터를 구성하고 요약합니다.  
  
  
## <a name="bkmk_groupdata"></a>보고서에서 데이터를 그룹화하려면  
  
1.  **디자인** 탭을 클릭합니다.  
  
2.  **행 그룹** 창이 표시되지 않는 경우 디자인 화면을 마우스 오른쪽 단추로 클릭하고 **보기** 를 클릭한 후 **그룹화**를 클릭합니다.  
  
3.  **보고서 데이터** 창에서 **Date** 필드를 **행 그룹** 창으로 끌어다 **(자세히)** 라는 행 위에 놓습니다.
  
    행 핸들 안에 대괄호가 표시되어 그룹임을 나타냅니다. 이제 테이블에 세로 점선의 양쪽에 하나씩 두 개의 Date 열이 있습니다.  
  
    ![추가된 날짜 그룹](../reporting-services/media/rs-basictablegroups1design.png "추가된 날짜 그룹")  
  
4.  **보고서 데이터** 창에서 **Order** 필드를 **행 그룹** 창으로 끌어다 Date 아래, **(자세히)** 위에 놓습니다.

    ![ssrs_ssdt_addorderfield](../reporting-services/media/ssrs-ssdt-addorderfield.png)   
  
    행 핸들에는 이제 두 개의 그룹을 표시하기 위해 ![ssrs_ssdt_rowgroupdoublehandles](../reporting-services/media/ssrs-ssdt-rowgroupdoublehandles.png)에 두 개의 대괄호가 있습니다. 테이블에도 두 개의 **Order** 열이 있습니다.  
  
5.  이중선 **오른쪽** 에서 원래 **Date** 및 **Order** 열을 삭제합니다. 그러면 이 개인 레코드 값이 제거되고 그룹 값만 표시됩니다. 두 열의 열 핸들을 선택하고 마우스 오른쪽 단추로 클릭한 다음 **열 삭제**를 클릭합니다.  
  
    ![삭제할 열 선택](../reporting-services/media/rs-basictablegroupsdeletecols.gif "삭제할 열 선택")  
  
6.  새 날짜 열에 서식을 지정하려면 `[Date]` 필드 식이 있는 셀을 마우스 오른쪽 단추로 클릭한 다음 **입력란 속성**을 클릭합니다.  
  
7.  **숫자**를 클릭한 다음 **범주** 필드에서 **날짜**를 클릭합니다.  
  
8.  **형식** 상자에서 **January 31, 2000**을 선택합니다.  
  
9.  [!INCLUDE[clickOK](../includes/clickok-md.md)]를 클릭합니다.  
  
10.  **미리 보기** 탭으로 전환하여 보고서를 미리 봅니다. 다음 그림과 비슷해야 합니다.  
    ![rs_BasicTableGroupsPreview](../reporting-services/media/rs-basictablegroupspreview.png) 
  
## <a name="bkmk_addtotals"></a>보고서에 합계를 추가하려면  
  
1.  디자인 뷰로 전환합니다.  
  
2.  `[LineTotal]`필드가 들어 있는 데이터 영역 셀을 마우스 오른쪽 단추로 클릭하고 **합계 추가**를 클릭합니다.  
  
    그러면 각 주문의 금액 합계가 표시되는 행이 추가됩니다.  
  
3.  `[Qty]`필드가 들어 있는 셀을 마우스 오른쪽 단추로 클릭하고 **합계 추가**를 클릭합니다.  
  
    그러면 각 주문의 수량 합계가 합계 행에 추가됩니다.  
  
4.  `Sum[Qty]`왼쪽의 빈 셀에 "**Order Total"** 이라는 레이블을 입력합니다.  
  
5.  합계 행에 배경색을 추가할 수 있습니다. 두 합계 셀과 레이블 셀을 선택합니다.  
  
6.  **서식** 메뉴에서 **배경색**, **밝은 회색**, **확인**을 차례로 클릭합니다.  
  
    ![디자인 뷰: 주문 합계가 있는 기본 테이블](../reporting-services/media/rs-basictablesumlinetotaldesign.gif "디자인 뷰: 주문 합계가 있는 기본 테이블")  
  
## <a name="bkmk_adddailytotal"></a>보고서에 일일 합계를 추가하려면  
  
1.  **Order** 셀을 마우스 오른쪽 단추로 클릭하고 **합계 추가**를 가리킨 후 **다음 이후**를 클릭합니다.  
  
    그러면 매일의 수량 및 금액 합계를 표시하는 새 행과 "**Total**" 레이블이 Order 열의 맨 아래에 추가됩니다.  
  
2.  같은 셀에서 **Daily** 라는 단어를 **Total** 이라는 단어 앞에 입력하여 **Daily Total**이라고 표시되도록 합니다.  
  
3.  **Daily Total** 셀, 두 개의 **Sum** 셀 및 이들 사이에 있는 빈 셀을 선택합니다.  
  
4.  **서식** 메뉴에서 **배경색**, **주황색**, **확인**을 차례로 클릭합니다.  
  
    ![배경색을 주황색으로 설정합니다](../reporting-services/media/rs-basictablesumdaytotaldesign.gif "rs_BasicTableSumDayTotalDesign")  
  
## <a name="bkmk_addgrandtotal"></a>보고서에 총합계를 추가하려면  
  
1.  Date 셀을 마우스 오른쪽 단추로 클릭하고 **합계 추가**를 가리킨 후 **다음 이후**를 클릭합니다.  
  
    그러면 전체 보고서의 수량 및 금액 합계를 표시하는 새 행과 **Total** 이라는 레이블이 **Date** 열에 추가됩니다.  
  
2.  같은 셀에서 **Grand** 라는 단어를 **Total** 이라는 단어 앞에 입력하여 **Grand Total**이라고 표시되도록 합니다.  
  
3.  **Grand Total** 셀, 두 개의 **Sum** 셀 및 이들 사이에 있는 빈 셀을 선택합니다.  
  
4.  **서식** 메뉴에서 **배경색**, **밝은 파란색**, **확인**을 차례로 클릭합니다.  
  
    ![디자인 뷰: 기본 테이블의 총합계](../reporting-services/media/rs-basictablesumgrandtotaldesign.gif "디자인 뷰: 기본 테이블의 총합계")  
  
5.  **미리 보기**를 클릭합니다.  
  
    마지막 페이지는 다음 그림과 비슷하게 표시됩니다. 도구 모음에서 마지막 페이지를 클릭합니다. ![ssrs_ssdt_viewertoolbar_lastpage](../reporting-services/media/ssrs-ssdt-viewertoolbar-lastpage.png)단추를 선택합니다.   
  
    ![미리 보기: 총합계가 있는 기본 테이블](../reporting-services/media/rs-basictablesumgrandtotalpreview.gif "미리 보기: 총합계가 있는 기본 테이블")  
  
## <a name="bkmk_publishreport"></a>보고서 서버에 보고서를 게시하려면(선택 사항)  
  
1.  선택 단계에서는 웹 포털에서 보고서를 볼 수 있도록 기본 모드 보고서 서버에 완료된 보고서를 게시합니다.  
  
2.  **프로젝트** 메뉴를 클릭한 다음 **자습서 속성...** 을 클릭합니다.  
  
3.  **TargetServerURL** 에 보고서 서버의 이름을 입력합니다. 예를 들면 다음과 같습니다.   
    - `http:/<servername>/reportserver`  
   
    - `https://localhost/reportserver` 은(는) 보고서 서버에서 보고서를 디자인하는 경우에만 작동합니다.  
  
  
4. TargetReportFolder는 프로젝트 이름인 tutorial이며,  다음 단계에서 보고서를 배포할 폴더의 이름입니다.  
5. **확인**을 클릭합니다.  
  
6.  **빌드** 메뉴를 클릭한 다음 **자습서 배포**를 클릭합니다.  
  
    출력 창에 다음과 비슷한 메시지가 표시되면 배포가 성공한 것입니다.  
  
    > ------ 빌드 시작: 프로젝트: 자습서, 구성: 디버그 ------  
    > 'Sales Orders.rdl'을 건너뜁니다. 최신 항목입니다.  
    > 빌드 완료 -- 0개 오류, 0개 경고  
    > --- 배포 시작: 프로젝트: 자습서, 구성: 디버그 ------  
    > https://[서버 이름]/reportserver에 배포하는 중  
    > '/tutorial/Sales Orders' 보고서를 배포하는 중  
    > 배포 완료 -- 0개 오류, 0개 경고  
    > ========== 빌드: 1개 성공 또는 최신, 0개 실패, 0개 건너뜀 ==========  
    > ========== 배포: 1개 성공, 0개 실패, 0개 생략 ==========  
  
    다음과 비슷한 오류 메시지가 표시되면 보고서 서버에 대한 권한이 있는지 확인하고 관리자 권한으로 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 를 시작했는지 확인합니다.  
  
    > "'XXXXXXXX\\[your user name]' 사용자에게 부여된 권한으로는 이 작업을 수행할 수 없습니다."  
  
7.  관리자 권한으로 웹 포털로 이동합니다. 예를 들어 Internet Explorer 아이콘을 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 클릭합니다.  
  
    [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 웹 포털 URL로 이동합니다.   
    **참고:** *포털* URL은 Report *Server* URL인 "Reportserver"가 아니라 "Reports"입니다.  예를 들어 다음과 같이 사용할 수 있습니다.   
    `https://<server name>/reports`을 참조하세요.  
    `https://localhost/reports`는 보고서 서버에서 보고서를 디자인하는 경우에만 작동합니다.  
  
8.  보고서가 포함된 폴더로 이동합니다. 기본 이름은 프로젝트 이름인 *tutorial*또는 프로젝트 속성의 TargetReportFolder 필드에 입력한 이름입니다.   
**Sales Orders** 보고서의 이름을 클릭하여 브라우저에서 렌더링된 보고서를 봅니다.  
  
    ![ssrs_tutorial_tutorialfolder](../reporting-services/media/ssrs-tutorial-tutorialfolder.png)  
 
기본 테이블 보고서 만들기 자습서를 성공적으로 완료했습니다.  
  
## <a name="see-also"></a>참고 항목  
[데이터 필터링, 그룹화 및 정렬&#40;보고서 작성기 및 SSRS&#41;](../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  
  

