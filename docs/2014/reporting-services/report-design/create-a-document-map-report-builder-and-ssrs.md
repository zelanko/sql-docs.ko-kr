---
title: 문서 구조 만들기(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: c200a97b-67f2-499f-8374-3ed1ebe3f33c
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: fc01da68aeaa393631aca6146a41e6eb88ecb14e
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53376635"
---
# <a name="create-a-document-map-report-builder-and-ssrs"></a>문서 구조 만들기(보고서 작성기 및 SSRS)
  문서 구조는 렌더링된 보고서의 보고서 항목에 대한 탐색 링크 집합을 제공합니다. 문서 구조가 포함된 보고서를 열면 보고서 옆에 별도의 창이 나타납니다. 사용자는 문서 구조의 링크를 클릭하여 해당 항목을 표시하는 보고서 페이지로 이동할 수 있습니다. 보고서 섹션 및 그룹은 링크 계층에 정렬되어 있습니다. 이 문서 구조에서 항목을 클릭하면 보고서가 새로 고쳐진 다음 항목에 해당하는 보고서 영역을 표시합니다.  
  
 문서 구조에 링크를 추가하려면 보고서 항목의 `DocumentMapLabel` 속성을 만들 텍스트로 설정하거나 문서 구조에 표시할 텍스트로 계산되는 식으로 설정합니다. 또한 테이블 또는 행렬 그룹에 대한 고유한 값을 문서 구조에 추가할 수 있습니다. 예를 들어 색을 기반으로 하는 그룹의 경우 각 고유 색은 해당 색에 대한 그룹 인스턴스를 표시하는 보고서 페이지에 대한 링크입니다.  
  
 또한 문서 구조를 표시하지 않고 보고서를 실행할 수 있도록 문서 구조 표시를 재정의하는 보고서에 대한 URL을 만든 다음 보고서 뷰어 도구 모음의 **문서 구조 표시/숨기기** 단추를 클릭하여 표시를 설정/해제할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="DocMapRenderExtensions"></a> 문서 구조 및 렌더링 확장 프로그램  
 문서 구조는 미리 보기 및 보고서 뷰어와 같은 HTML 렌더링 확장 프로그램용입니다. 다른 렌더링 확장 프로그램에서는 다음과 같은 방법으로 문서 구조를 표시합니다.  
  
-   PDF는 문서 구조를 책갈피 창으로 렌더링합니다.  
  
-   Excel은 문서 구조를 링크 계층이 포함된 명명된 워크시트로 렌더링합니다. 보고서 섹션은 문서 구조와 함께 동일한 통합 문서에 포함되는 별도의 워크시트로 렌더링됩니다.  
  
-   Word에는 목차 형식의 문서 구조가 포함되어 있습니다.  
  
-   Atom, TIFF, XML 및 CSV는 문서 구조를 무시합니다.  
  
 자세한 내용은 [여러 보고서 렌더링 확장 프로그램의 대화형 기능&#40;보고서 작성기 및 SSRS&#41;](../report-builder/interactive-functionality-different-report-rendering-extensions.md)을 참조하세요.  
  
##  <a name="AddRptItemToMap"></a>   
#### <a name="to-add-a-report-item-to-a-document-map"></a>문서 구조에 보고서 항목을 추가하려면  
  
1.  디자인 뷰에서 문서 구조에 추가할 테이블, 행렬 또는 계기와 같은 보고서 항목을 선택합니다. 보고서 항목 속성이 속성 창에 나타납니다.  
  
    > [!NOTE]  
    >  테이블릭스 데이터 영역을 선택하려면 아무 셀이나 클릭하여 행 및 열 핸들을 표시한 다음 모퉁이 핸들을 클릭합니다.  
  
2.  속성 창에서 문서 구조에 표시 하려는 텍스트를 입력 합니다 `DocumentMapLabel` 속성을 입력 하거나 레이블로 계산 되는 식을 입력 합니다. 예를 들어 **Sales Chart**를 입력합니다.  
  
    > [!NOTE]  
    >  속성 창이 표시되지 않는 경우 **보기** 탭의 **표시/숨기기** 그룹에서 **속성**을 선택합니다.  
  
3.  문서 구조에 표시할 각 보고서 항목에 대해 1단계와 2단계를 반복합니다.  
  
4.  **실행**을 클릭합니다. 보고서가 실행되고 문서 구조에 사용자가 만든 레이블이 표시됩니다. 해당 항목이 있는 보고서 페이지로 이동하는 링크를 클릭합니다.  
  
 
  
##  <a name="AddUniqueValuesToMap"></a>   
#### <a name="to-add-unique-group-values-to-a-document-map"></a>문서 구조에 고유한 그룹 값을 추가하려면  
  
1.  디자인 뷰에서 문서 구조에 표시할 그룹을 포함하는 테이블, 행렬 또는 목록을 선택합니다. 그룹화 창에 행 및 열 그룹이 표시됩니다.  
  
2.  행 그룹 창에서 그룹을 마우스 오른쪽 단추로 클릭한 다음 **그룹 편집**을 클릭합니다. **테이블릭스 그룹 속성** 대화 상자의 **일반** 페이지가 열립니다.  
  
3.  **고급**을 클릭합니다.  
  
4.  **문서 구조** 목록 상자에서 그룹 식과 일치하는 식을 입력하거나 선택합니다.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  문서 구조에 표시할 각 그룹에 대해 1-4단계를 반복합니다.  
  
7.  **실행**을 클릭합니다. 보고서가 실행되고 문서 구조에 그룹 값이 표시됩니다. 해당 항목이 있는 보고서 페이지로 이동하는 링크를 클릭합니다.  
  
 
  
##  <a name="HideMapWhenViewRpt"></a>   
#### <a name="to-hide-the-document-map-when-you-view-a-report"></a>보고서를 볼 때 문서 구조를 숨기려면  
  
1.  보고서 관리자에서 문서 구조를 포함하는 보고서를 찾습니다.  
  
     예를 들어 [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 예제 보고서의 경우 다음 URL에서 Product Catalog라는 보고서를 지정합니다.  
  
    ```  
    http://localhost/Reports/Pages/Report.aspx?ItemPath=%2fAdventureWorks2012+Sample+Reports%2fProduct+Catalog  
    ```  
  
2.  서버의 보고서 경로를 복사합니다. 예에서 보고서 경로는 `%2fAdventureWorks2012+Sample+Reports%2fProduct+Catalog`입니다.  
  
3.  다음 3개의 구성 요소를 사용하여 새 URL을 만듭니다.  
  
    -   보고서 서버의 보고서 뷰어: `http://localhost/ReportServer/Pages/ReportViewer.aspx?`  
  
    -   1단계에서 복사한 보고서 이름. 예를 들면 다음과 같습니다. `%2fAdventureWorks2012+Sample+Reports%2fProduct+Catalog`  
  
    -   문서 구조를 숨기도록 지정하는 디바이스 정보 매개 변수: `&rs%3aCommand=Render&rc%3aFormat=HTML4.0&rc%3aDocMap=False`  
  
     다음 URL에서는 이러한 3개의 구성 요소가 나열되는 순서대로 추가하여 포함되어 있습니다.  
  
    ```  
    http://localhost/ReportServer/Pages/ReportViewer.aspx?  
    %2fAdventureWorks2012+Sample+Reports%2fProduct+Catalog  
    &rs%3aCommand=Render&rc%3aFormat=HTML4.0&rc%3aDocMap=False  
    ```  
  
     이 URL을 사용하려면 해당 URL을 복사하고 모든 줄 바꿈을 제거합니다.  
  
4.  보고서 관리자에 URL을 붙여넣은 다음 Enter 키를 누릅니다. 보고서가 실행되고 문서 구조가 숨겨집니다.  
  
> [!NOTE]  
>  샘플 보고서를 다운로드하는 방법은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][보고서 작성기 및 보고서 디자이너 샘플 보고서](https://go.microsoft.com/fwlink/?LinkId=198283)를 참조하세요.  
>   
>  자세한 내용은 SQL Server 온라인 설명서의 [Reporting Services 설명서](https://go.microsoft.com/fwlink/?linkid=121312) 에 있는 "URL 액세스"를 참조하십시오.  
  
 
  
## <a name="see-also"></a>관련 항목  
 [찾기 및 보고서 관리자에서 보고서 보기 &#40;보고서 작성기 및 SSRS&#41;](../report-builder/finding-and-viewing-reports-in-the-web-portal-report-builder-and-ssrs.md)  
  
  
