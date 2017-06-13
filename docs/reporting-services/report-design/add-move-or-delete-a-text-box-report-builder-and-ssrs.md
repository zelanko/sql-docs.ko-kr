---
title: "추가, 이동 또는 삭제 (보고서 작성기 및 SSRS)는 텍스트 상자가 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f042cf81-d933-4ac7-9287-c074a46bde98
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 75444343968c9901a24c1a4d431d4d8cfacb1567
ms.contentlocale: ko-kr
ms.lasthandoff: 06/13/2017

---
# <a name="add-move-or-delete-a-text-box-report-builder-and-ssrs"></a>입력란 추가, 이동 또는 삭제(보고서 작성기 및 SSRS)
  입력란은 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 페이지를 매긴 보고서에서 가장 일반적으로 사용되는 보고서 항목입니다. 입력란을 보고서 본문에 추가하여 제목, 매개 변수 선택 항목, 기본 제공 필드 및 날짜와 같은 정보를 표시할 수 있습니다.  
  
 테이블이나 행렬의 각 셀은 실제로 입력란입니다. 테이블 및 행렬이 있는 보고서에 표시되는 거의 모든 보고서 데이터는 보고서의 각 입력란 내용을 평가하는 보고서 처리기의 결과입니다. 따라서 데이터 영역 외부의 다른 입력란과 같은 방식으로 셀의 서식을 지정할 수 있습니다.  
  
 목록 데이터 영역에 입력란을 추가하려면 먼저 입력란을 추가한 다음 목록으로 끌어 와야 합니다.  
  
> [!NOTE]  
>  입력란을 클릭하기만 하면 입력란의 텍스트를 편집할 수 있습니다. 입력란의 텍스트가 아니라 입력란 자체를 선택하려면 편집 상태에서 Esc 키를 누릅니다.  
  
## <a name="to-add-a-text-box"></a>입력란을 추가하려면  
  
1.  디자인 뷰의 **삽입** 탭에서 **입력란**을 클릭합니다.  
  
2.  디자인 화면에서 상자를 클릭한 다음 끌어 원하는 크기의 입력란을 만듭니다.  
  
## <a name="to-add-a-text-box-in-a-list"></a>목록에 입력란을 추가하려면  
  
1.  보고서 디자인 뷰의 **삽입** 탭에서 **목록**을 클릭합니다.  
  
2.  디자인 화면에서 상자를 클릭한 다음 끌어 원하는 크기의 목록을 만듭니다.  
  
3.  **삽입** 탭에서 **입력란**을 클릭합니다.  
  
4.  디자인 화면에서 1단계에서 추가한 목록 안쪽에 있는 상자를 클릭한 다음 끌어 원하는 크기의 입력란을 만듭니다.   
  
5.  입력란이 목록 안쪽에 올바르게 중첩되어 있는지 확인하려면 입력란을 선택합니다.  
  
    > [!NOTE]  
    >  입력란을 클릭하여 편집 모드에 있는 경우에는 Esc 키를 눌러 입력란을 선택합니다.  
  
6.  속성 창에서 **부모** 속성이 목록 데이터 영역에 자동으로 추가된 사각형인지 확인합니다.  
  
    > [!NOTE]  
    >  속성 창이 표시되지 않으면 **보기** 탭에서 **속성** 을 선택합니다.  
  
## <a name="to-move-a-text-box"></a>입력란을 이동하려면  
  
1.  보고서 디자인 뷰에서 입력란 내의 빈 공간을 클릭하여 입력란을 선택합니다.  
  
    > [!NOTE]  
    >  입력란을 클릭하여 편집 모드에 있는 경우에는 Esc 키를 눌러 입력란을 선택합니다.  
  
2.  입력란 핸들을 클릭하고 입력란을 새 위치로 끕니다.   
    또는 화살표 키를 사용하여 선택한 입력란을 가로 또는 세로로 이동합니다. 디자인 화면에서 더 작은 증가값으로 입력란을 이동하려면 Ctrl 키를 누른 채 화살표를 클릭합니다.  
  
## <a name="to-delete-a-text-box"></a>입력란을 삭제하려면  
  
1.  보고서 디자인 뷰에서 입력란 내의 빈 공간을 마우스 오른쪽 단추로 클릭하여 입력란을 선택한 다음 **삭제**를 클릭합니다. 또는 입력란 안의 빈 공간을 클릭한 다음 Delete 키를 누릅니다.  
  
    > [!NOTE]  
    >  입력란을 클릭하여 편집 모드에 있는 경우에는 Esc 키를 눌러 입력란을 선택합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [입력란&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/text-boxes-report-builder-and-ssrs.md)   
 [식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [바로 가기 키&#40;보고서 작성기&#41;](../../reporting-services/report-builder/keyboard-shortcuts-report-builder.md)  
  
  
