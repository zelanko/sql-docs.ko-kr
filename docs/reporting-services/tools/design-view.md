---
title: "디자인 보기 | Microsoft Docs"
ms.custom: 
ms.date: 05/31/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rtp.rptdesigner.layoutview.f1
helpviewer_keywords:
- Layout View dialog box
ms.assetid: 6fa378aa-442f-4d2f-beab-02a0fb5cd3ce
caps.latest.revision: 38
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7a3129645fd110b2bddedae0022592a74fb97a9e
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="design-view"></a>디자인 뷰
[!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 보고서 디자이너에서 디자인 뷰를 사용하여 보고서에 보고서 항목을 배치할 수 있습니다. 디자인 뷰는 디자인 화면 또는 레이아웃 뷰라고도 합니다.  
  ![ssrs_ssdt_preview](../../reporting-services/media/ssrs-ssdt-preview.png)
## <a name="report-design-surface"></a>보고서 디자인 화면  
디자인 화면은 보고서 본문, 페이지 머리글 및 페이지 바닥글로 
+ 보고서 본문
+ 페이지 머리글
+ 페이지 바닥글 

도구 상자를 사용하여 이 3가지 섹션에 항목을 선택하여 배치할 수 있습니다. 보고서 데이터 창을 사용하여 데이터 집합 쿼리와 필드 목록을 포함한 데이터 집합, 이미지, 매개 변수 및 데이터 원본을 볼 수 있습니다. 디자인 화면에 보고서 항목을 추가한 후 **보고서 데이터** 창의 데이터 집합 필드를 테이블, 행렬 또는 목록과 같은 데이터 영역에 끌어서 놓습니다. 보고서 디자인 화면의 각 항목에는 속성 대화 상자 또는 속성 창을 사용하여 관리할 수 있는 속성이 포함되어 있습니다.  
  
## <a name="toolbox"></a>도구 상자  
 도구 상자에는 보고서에서 사용할 수 있는 데이터 영역과 기타 보고서 항목이 나열되어 있습니다. 도구 상자의 보고서 항목을 추가하려면 항목을 두 번 클릭하거나 디자인 화면에 끌어 놓습니다. 그런 다음 개체 핸들을 사용하여 모양과 크기를 변경할 수 있습니다.  
  
## <a name="report-data-pane"></a>보고서 데이터 창  
 보고서 데이터 창을 보려면 **보기** 메뉴에서 **보고서 데이터**를 클릭합니다. 이 창을 사용하여 매개 변수, 이미지, 데이터 원본 및 데이터 집합을 정의하고 ReportName과 같은 기본 제공 필드를 참조할 수 있습니다. 새 항목을 추가하려면 **새로 만들기** 메뉴를 클릭하고 항목을 선택합니다. 계산된 필드를 기존 데이터 집합에 추가하려면 **데이터 집합**을 클릭하고 **데이터 집합 속성** 대화 상자에서 **필드**를 선택합니다. 그런 다음 항목을 선택하고 **편집** 을 클릭하여 **속성** 대화 상자를 엽니다. 보고서 데이터 창의 항목을 마우스 오른쪽 단추로 클릭하여 항목을 추가하거나 속성을 업데이트할 수도 있습니다.  
  
 보고서에 데이터 및 이미지를 추가하려면 보고서 데이터 창의 항목을 디자인 화면의 데이터 영역 및 입력란에 끌어 놓습니다.  
  
 자세한 내용은 [Report Data Pane](../../reporting-services/report-data/report-data-pane.md)을 참조하세요.  
  
## <a name="grouping-pane"></a>그룹화 창  
 그룹은 보고서 데이터를 시각적 계층으로 구성하고 합계를 계산하는 데 사용됩니다. 그룹화 창을 사용하여 테이블, 행렬 또는 목록 데이터 영역에 정의된 그룹을 볼 수 있습니다. 기본적으로 그룹화 창에는 선택한 데이터 영역의 모든 그룹이 평면화된 목록으로 표시됩니다. 차트 및 계기 데이터 영역은 그룹화 창에 표시되지 않습니다.  
  
 그룹 간의 관계를 보려면 그룹화 창을 고급 모드로 전환합니다. 이 모드에서는 데이터 영역에서 각 그룹에 해당하는 셀이 시각적으로 표시되어 그룹 멤버의 계층 구조가 나타납니다.  
  
 자세한 내용은 [Grouping Pane](../../reporting-services/tools/grouping-pane.md)을 참조하세요.  
  
## <a name="page-header-and-page-footer"></a>페이지 머리글 및 페이지 바닥글  
 페이지 머리글 및 페이지 바닥글은 각각 페이지의 위쪽과 아래쪽에 표시됩니다. 머리글과 바닥글은 정적 텍스트, 이미지, 선, 사각형, 테두리, 배경색 및 배경 이미지를 포함할 수 있습니다. 머리글이나 바닥글에 보고서 항목을 추가하려면 디자인 화면을 마우스 오른쪽 단추로 클릭하고 머리글 또는 바닥글을 선택합니다. 이렇게 하면 디자인 화면에 머리글 및 바닥글 섹션이 표시됩니다.  
  
## <a name="properties-pane"></a>속성 창  
 속성 창을 사용하여 디자인 화면의 현재 선택된 보고서 항목 또는 그룹화 창의 선택된 그룹에 대한 속성을 볼 수 있습니다. 또는 선택한 보고서 항목 또는 그룹을 마우스 오른쪽 단추로 클릭한 후 **속성** 을 클릭하여 보고서 항목 또는 그룹에 대한 해당 **속성** 대화 상자를 열 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [페이지 머리글 및 바닥글 &#40; 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md)   
 [보고서 디자인 팁 &#40; 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-design/report-design-tips-report-builder-and-ssrs.md)  
  
  

