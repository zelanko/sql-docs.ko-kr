---
title: '6단원: 그룹화 및 합계 (Reporting Services) 추가 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: e3d61228-2aa4-42cc-955e-602dbf3406a7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7bd3261a6669b1677fbfeff23b0017e622600007
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56012744"
---
# <a name="lesson-6-adding-grouping-and-totals-reporting-services"></a>6단원: 그룹화 및 합계 추가(Reporting Services)
  보고서에 그룹화 및 합계를 추가하여 데이터를 구성하고 요약할 수 있습니다.  
  
 보고서에 누계 추가에 대한 자세한 내용은 curah.microsoft.com의 [Reporting Services (SSRS) 보고서에 합계 추가](https://go.microsoft.com/fwlink/p/?LinkId=403698)합니다.  
  
 **항목 내용**  
  
-   [보고서의 데이터를 그룹화](#bkmk_groupdata)  
  
-   [보고서에 합계를 추가 하려면](#bkmk_addtotals)  
  
-   [보고서에 일일 합계를 추가 하려면](#bkmk_adddailytotal)  
  
-   [보고서에 총합계를 추가 하려면](#bkmk_addgrandtotal)  
  
-   [(선택 사항) 보고서 서버로 보고서를 게시 하려면](#bkmk_publishreport)  
  
##  <a name="bkmk_groupdata"></a> 보고서의 데이터를 그룹화  
  
1.  **디자인** 탭을 클릭합니다.  
  
2.  표시 되지 않으면 합니다 **Rowgroups** 창 디자인 화면을 마우스 오른쪽 단추로 클릭 하 고 클릭 **보기** 클릭 하 고 **그룹화**.  
  
3.  **보고서 데이터** 창으로 끕니다 합니다 `Date` 필드를 **행 그룹** 창입니다. **(자세히)** 라는 행 위에 놓습니다.  
  
     행 핸들 안에 대괄호가 표시되어 그룹임을 나타냅니다. 이제 테이블에 세로 점선의 양쪽에 하나씩 두 개의 Date 열이 있습니다.  
  
     ![](../../2014/tutorials/media/rs-basictablegroups1design.gif "rs_BasicTableGroups1Design")  
  
4.  **보고서 데이터** 창으로 끕니다 합니다 `Order` 필드를 **행 그룹** 창입니다. Date 아래, **(자세히)** 위에 놓습니다.  
  
     행 핸들 안에 두 개의 대괄호가 표시되어 두 개의 그룹임을 나타냅니다. 테이블에 두 개의 `Order` 열을 너무 합니다.  
  
5.  원래 Date 및 Order 열을 삭제 합니다 **오른쪽** 이중선입니다. 그러면 이 개인 레코드 값이 제거되고 그룹 값만 표시됩니다. 두 열의 열 핸들을 선택하고 마우스 오른쪽 단추로 클릭한 다음 **열 삭제**를 클릭합니다.  
  
     ![삭제할 열 선택](../../2014/tutorials/media/rs-basictablegroupsdeletecols.gif "삭제할 열 선택")  
  
     열 머리글 및 날짜의 서식을 다시 지정할 수 있습니다.  
  
6.  **미리 보기** 탭으로 전환하여 보고서를 미리 봅니다. 다음 그림과 비슷해야 합니다.  
  
     ![Date 다음 Order 기준으로 그룹화된 테이블](../../2014/tutorials/media/rs-basictablegroupspreview.gif "Date 다음 Order 기준으로 그룹화된 테이블")  
  
##  <a name="bkmk_addtotals"></a> 보고서에 합계를 추가 하려면  
  
1.  디자인 뷰로 전환합니다.  
  
2.  `[LineTotal]`필드가 들어 있는 데이터 영역 셀을 마우스 오른쪽 단추로 클릭하고 **합계 추가**를 클릭합니다.  
  
     그러면 각 주문의 금액 합계가 표시되는 행이 추가됩니다.  
  
3.  `[Qty]`필드가 들어 있는 셀을 마우스 오른쪽 단추로 클릭하고 **합계 추가**를 클릭합니다.  
  
     그러면 각 주문의 수량 합계가 합계 행에 추가됩니다.  
  
4.  `Sum[Qty]`왼쪽의 빈 셀에 "**Order Total"** 이라는 레이블을 입력합니다.  
  
5.  합계 행에 배경색을 추가할 수 있습니다. 두 합계 셀과 레이블 셀을 선택합니다.  
  
6.  **서식** 메뉴에서 **배경색**, **밝은 회색**, **확인**을 차례로 클릭합니다.  
  
     ![디자인 뷰: 주문 합계가 있는 기본 테이블](../../2014/tutorials/media/rs-basictablesumlinetotaldesign.gif "디자인 뷰: 주문 합계가 있는 기본 테이블")  
  
##  <a name="bkmk_adddailytotal"></a> 보고서에 일일 합계를 추가 하려면  
  
1.  Order 셀을 마우스 오른쪽 **합계 추가**, 클릭 **후**합니다.  
  
     매일 및 레이블을 수량 및 금액의 합계를 표시를 포함 하는 새 행이 추가 "**총**" Order 열에 있습니다.  
  
2.  같은 셀에서 **Daily** 라는 단어를 **Total** 이라는 단어 앞에 입력하여 **Daily Total**이라고 표시되도록 합니다.  
  
3.  **Daily Total** 셀, 두 개의 **Sum** 셀 및 이들 사이에 있는 빈 셀을 선택합니다.  
  
4.  **서식** 메뉴에서 **배경색**, **주황색**, **확인**을 차례로 클릭합니다.  
  
     ![](../../2014/tutorials/media/rs-basictablesumdaytotaldesign.gif "rs_BasicTableSumDayTotalDesign")  
  
##  <a name="bkmk_addgrandtotal"></a> 보고서에 총합계를 추가 하려면  
  
1.  Date 셀을 마우스 오른쪽 단추로 클릭하고 **합계 추가**를 가리킨 후 **다음 이후**를 클릭합니다.  
  
     전체 보고서에 대 한 수량 및 금액의 합계를 표시를 포함 하는 새 행이 추가 하며 **총** 레이블을 `Date` 열입니다.  
  
2.  같은 셀에서 **Grand** 라는 단어를 **Total** 이라는 단어 앞에 입력하여 **Grand Total**이라고 표시되도록 합니다.  
  
3.  **Grand Total** 셀, 두 개의 **Sum** 셀 및 이들 사이에 있는 빈 셀을 선택합니다.  
  
4.  **서식** 메뉴에서 **배경색**, **밝은 파란색**, **확인**을 차례로 클릭합니다.  
  
     ![디자인 뷰: 기본 테이블의 총합계](../../2014/tutorials/media/rs-basictablesumgrandtotaldesign.gif "디자인 뷰: 기본 테이블의 총합계")  
  
5.  미리 보기를 클릭합니다.  
  
     마지막 페이지는 다음과 같아야 합니다.  
  
     ![미리 보기: 총합계가 있는 기본 테이블](../../2014/tutorials/media/rs-basictablesumgrandtotalpreview.gif "미리 보기: 총합계가 있는 기본 테이블")  
  
##  <a name="bkmk_publishreport"></a> (선택 사항) 보고서 서버로 보고서를 게시 하려면  
  
1.  선택 단계에서는 보고서 관리자에서 보고서를 볼 수 있도록 기본 모드 보고서 서버에 완료된 보고서를 게시합니다.  
  
2.  도구 모음에서 **프로젝트** 를 클릭한 후 **자습서 속성...** 을 클릭합니다.  
  
3.  에 **TargetServerURL** 보고서 서버의 이름 이름의 예를 들어 입력 **http://\<서버 이름 > / reportserver**  
  
4.   **확인**을 클릭합니다.  
  
5.  도구 모음에서 **빌드** 를 클릭한 후 **자습서 배포**를 클릭합니다.  
  
     출력 창에 다음과 비슷한 메시지가 표시되면 배포가 성공한 것입니다.  
  
    > ------ 빌드 시작: 프로젝트: 자습서, 구성: 디버그 ------'Sales Orders.rdl'을 건너 뛰는 중입니다. 항목이 최신입니다. 빌드 완료 -- 0개 오류, 0개 경고------ 배포 시작: 프로젝트: 자습서, 구성: 디버그--- http:// 배포\<서버 이름 > reportserverDeploying 보고서 ' 자습서/Sales Orders'. 배포 완료--0 개 오류, 0 개 경고 === 빌드: 1개 성공 또는 최신, 0개 실패, 0개 생략 ==================== 배포: 1개 성공, 0개 실패, 0개 생략 ==========  
  
     다음과 비슷한 오류 메시지가 표시되면 보고서 서버에 대한 권한이 있는지 확인하고 관리자 권한으로 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 를 시작했는지 확인합니다.  
  
    > "사용자에 게 부여 된 권한에 ' XXXXXXXX\\< 사용자 이름\>'이 작업을 수행 하는 데 충분 하지 않습니다"  
  
6.  예를 들어 관리자 권한으로 보고서 관리자를 시작, Internet Explorer에 대 한 아이콘을 마우스 오른쪽 단추로 클릭 하 고, 클릭 **관리자 권한으로 실행**합니다.  
  
     보고서 관리자 URL로 이동합니다. 예: `http://<server name>/reports`  
  
7.  보고서가 포함된 폴더로 이동하고 `Sales Orders` 보고서의 이름을 클릭하여 브라우저에서 렌더링된 보고서를 봅니다.  
  
## <a name="next-steps"></a>다음 단계  
 기본 테이블 보고서 만들기 자습서를 성공적으로 완료했습니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 필터링, 그룹화 및 정렬&#40;보고서 작성기 및 SSRS&#41;](report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  
