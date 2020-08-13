---
title: '6단원: 그룹화 및 합계 추가(Reporting Services) | Microsoft Docs'
description: Reporting Services 보고서에 그룹화 및 합계를 추가하여 데이터를 구성하고 요약하는 방법을 알아봅니다.
ms.date: 04/18/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: e3d61228-2aa4-42cc-955e-602dbf3406a7
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5d149bb85834ae9c775e414e405889631a81f288
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243267"
---
# <a name="lesson-6-adding-grouping-and-totals-reporting-services"></a>6단원: 그룹화 및 합계 추가(Reporting Services)

최종 자습서 단원에서는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 보고서에 그룹화 및 합계를 추가하여 데이터를 구성하고 합산하겠습니다.  

## <a name="to-group-data-in-a-report"></a>보고서에서 데이터를 그룹화하려면

1. **디자인** 탭을 선택합니다.
2. **행 그룹** 창이 표시되지 않는 경우 디자인 화면을 마우스 오른쪽 단추로 클릭하고 **보기** >**그룹화**를 선택합니다.
3. **보고서 데이터** 창에서 `[Date]` 필드를 **행 그룹** 창으로 끕니다. **= (자세히)** 로 표시되는 행 위에 놓습니다.

    > [!NOTE]
    > 이제 행 핸들 안에 대괄호가 포함되어 그룹임을 나타냅니다. 또한 테이블에서 세로 점선의 양쪽에 하나씩, 두 개의 `[Date]` 식 열이 있습니다.
    >
    >![날짜 그룹 추가됨](media/rs-basictablegroups1design.png "날짜 그룹 추가됨")
4. **보고서 데이터** 창에서 `[Order]` 필드를 **행 그룹** 창으로 끕니다. **Date** 아래, **= (자세히)** 위에 놓습니다.

    ![ssrs_ssdt_addorderfield](media/ssrs-ssdt-addorderfield.png)

    > [!NOTE]
    > 이제 행 핸들에 두 개의 대괄호가 포함되어(![ssrs_ssdt_rowgroupdoublehandles](media/ssrs-ssdt-rowgroupdoublehandles.png)) 두 개의 그룹을 나타냅니다. 또한 테이블에 두 개의 `[Order]` 식 열이 있습니다.

5. 이중선 오른쪽에 있는 원본 `[Date]` 및 `[Order]` 식 열을 삭제합니다. 두 열의 열 핸들을 선택하고 마우스 오른쪽 단추를 클릭한 다음, **열 삭제**를 선택합니다. 보고서 디자이너가 개별 행 식을 제거하여 그룹 식만 표시됩니다.

    ![삭제할 열 선택](media/rs-basictablegroupsdeletecols.gif "삭제할 열 선택")

6. 새 `[Date]` 열의 서식을 지정하려면 `[Date]` 식이 포함된 데이터 영역 셀을 마우스 오른쪽 단추로 클릭하고 **텍스트 상자 속성**을 선택합니다.
7. 맨 왼쪽 열 목록 상자에서 **숫자**를 선택하고 **범주** 목록 상자에서 **날짜**를 선택합니다.
8. **형식** 목록 상자에서 **January 31, 2000**을 선택합니다.
9. **확인**을 선택하여 서식을 적용합니다.
10. 다시 보고서를 미리 보기합니다. 아래와 같이 표시됩니다.

    ![rs_BasicTableGroupsPreview](media/rs-basictablegroupspreview.png)

## <a name="adding-totals-to-a-report"></a>보고서에 합계 추가

1. **디자인** 뷰로 전환합니다.
2. `[LineTotal]` 식이 포함된 데이터 영역 셀을 마우스 오른쪽 단추로 클릭하고 **합계 추가**를 선택합니다. 보고서 디자이너에서 각 주문의 달러 금액 합계가 포함된 행이 추가됩니다.
3. `[Qty]` 필드가 포함된 셀을 마우스 오른쪽 단추로 클릭하고 **합계 추가**를 선택합니다. 보고서 디자이너에서 각 주문의 수량 합계가 합계 행에 추가됩니다.
4. `Sum[Qty]` 셀의 왼쪽에 있는 빈 셀에 “Order Total” 문자열을 입력합니다.
5. 합계 행에 배경색을 추가할 수 있습니다. 두 합계 셀과 레이블 셀을 선택합니다.  
6. **서식** 메뉴에서 **배경색** > **연한 회색** 사각형을 선택합니다.
7. **확인**을 선택하여 서식을 적용합니다.

   ![디자인 뷰: 주문 합계가 있는 기본 테이블](media/rs-basictablesumlinetotaldesign.gif "디자인 뷰: 주문 합계가 있는 기본 테이블")

## <a name="add-the-daily-total-to-the-report"></a>보고서에 일별 합계 추가

1. `[Order]` 식 셀을 마우스 오른쪽 단추로 클릭하고 **합계 추가** > **이후**를 선택합니다. 보고서 디자이너에서 각 날짜의 `[Qty]` 및 `[Linetotal]` 값 합계가 포함된 새 행과 “Total” 문자열이 `[Order]` 식 열의 맨 아래에 추가됩니다.
2. 같은 셀에서 “Daily” 단어를 “Total” 단어 앞에 입력하여 “Daily Total”로 표시되도록 합니다.
3. 해당 셀과 오른쪽에 있는 두 개의 인접한 합계 셀, 그 사이에 있는 빈 셀을 선택합니다.
4. **서식** 메뉴에서 **배경색** > **주황** 사각형을 선택합니다.
5. **확인**을 선택하여 서식을 적용합니다.

   ![배경색을 주황색으로 설정](media/rs-basictablesumdaytotaldesign.gif "rs_BasicTableSumDayTotalDesign")

## <a name="add-the-grand-total-to-the-report"></a>보고서에 총합계 추가

1. `[Date]` 식 셀을 마우스 오른쪽 단추로 클릭하고 **합계 추가** > **이후**를 선택합니다. 보고서 디자이너에서 전체 보고서의 `[Qty]` 및 `[LineTotal]` 값 합계가 포함된 새 행과 “Total” 문자열이 `[Date]` 식 열의 맨 아래에 추가됩니다.
2. 같은 셀에서 “Grand” 문자열을 “Total” 단어 앞에 입력하여 “Grand Total”로 표시되도록 합니다.
3. “Grand Total”이 포함된 셀, 두 개의 `Sum()` 식 셀, 그 사이에 있는 빈 셀을 선택합니다.
4. **서식** 메뉴에서 **배경색** > **연한 파랑** 사각형을 선택합니다.
5. **확인**을 선택하여 서식을 적용합니다.

    ![디자인 뷰: 기본 테이블의 총합계](media/rs-basictablesumgrandtotaldesign.gif "디자인 뷰: 기본 테이블의 총합계")

## <a name="preview-the-report"></a>보고서 미리 보기

서식 변경 내용을 미리 보려면 **미리 보기** 탭을 선택합니다. **미리 보기** 도구 모음에서 **마지막 페이지** 단추(![ssrs_ssdt_viewertoolbar_lastpage](media/ssrs-ssdt-viewertoolbar-lastpage.png))를 선택합니다. 결과가 아래와 같이 표시됩니다.

   ![미리 보기: 총합계가 있는 기본 테이블](media/rs-basictablesumgrandtotalpreview.gif "미리 보기: 총합계가 있는 기본 테이블")

## <a name="publishing-the-report-to-the-report-server-optional"></a>‘보고서 서버’에 보고서 게시(선택 사항)

선택 단계로, 웹 포털에서 보고서를 볼 수 있도록 완성된 보고서를 보고서 서버에 게시할 수 있습니다.

1. **프로젝트** 메뉴 > **Tutorial 속성...** 을 선택합니다.
2. **TargetServerURL**에 보고서 서버의 이름을 입력합니다. 예:
    - `http:/<servername>/reportserver` 또는
    - `https://localhost/reportserver`는 보고서 서버에서 보고서를 디자인하는 경우에만 작동합니다.

3. **TargetReportFolder** 이름은 프로젝트 이름을 따라 Tutorial로 지정됩니다. 보고서 디자이너는 이 폴더에 보고서를 배포합니다.
4. **확인**을 선택합니다.
5. **빌드** 메뉴 > **Tutorial 배포**를 선택합니다.

    **출력** 창에 아래와 같은 메시지가 표시되는 경우 배포에 성공했음을 나타냅니다.

    > ------ 빌드 시작: 프로젝트: 자습서, 구성: 디버그 ------  
    > 'Sales Orders.rdl'을 건너뜁니다. 최신 항목입니다.  
    > 빌드 완료 -- 0개 오류, 0개 경고  
    > --- 배포 시작: 프로젝트: 자습서, 구성: 디버그 ------  
    > `https://[server name]/reportserver`에 배포하는 중  
    > '/tutorial/Sales Orders' 보고서를 배포하는 중  
    > 배포 완료 -- 0개 오류, 0개 경고  
    > ========== 빌드: 1개 성공 또는 최신, 0개 실패, 0개 건너뜀 ==========  
    > ========== 배포: 1개 성공, 0개 실패, 0개 생략 ==========  

    다음과 비슷한 오류 메시지가 표시되면 보고서 서버에서 적절한 권한이 있고, 관리자 권한으로 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]를 시작했는지 확인합니다.
    >
    > "'XXXXXXXX\\[your user name]' 사용자에게 부여된 권한으로는 이 작업을 수행할 수 없습니다."

6. 관리자 권한으로 브라우저를 엽니다. 예를 들어 Internet Explorer 아이콘을 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 선택합니다.
7. 웹 포털 URL로 이동합니다.
   - `https://<server name>/reports`.
   - `https://localhost/reports`는 보고서 서버에서 보고서를 디자인하는 경우에만 작동합니다.

8. Tutorial 폴더를 선택하고 “Sales Orders” 보고서를 선택하여 보고서를 봅니다.

    ![ssrs_tutorial_tutorialfolder](media/ssrs-tutorial-tutorialfolder.png)  

**기본 테이블 보고서 만들기 자습서**를 성공적으로 완료했습니다.

## <a name="see-also"></a>참고 항목

[데이터 필터링, 그룹화 및 정렬&#40;보고서 작성기 및 SSRS&#41;](report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)
