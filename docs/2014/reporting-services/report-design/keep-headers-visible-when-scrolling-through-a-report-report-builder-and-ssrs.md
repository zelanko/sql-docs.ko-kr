---
title: 보고서를 스크롤할 때 머리글 계속 표시(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 6d9192a4-fd5c-41ad-b9ef-f88f9496afed
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 37c3dc20ab537e7cb8bf69099dbd6d24ff384731
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66105597"
---
# <a name="keep-headers-visible-when-scrolling-through-a-report-report-builder-and-ssrs"></a>보고서를 스크롤할 때 머리글 계속 표시(보고서 작성기 및 SSRS)
  보고서를 렌더링한 다음 스크롤할 때 행 및 열 레이블이 화면에서 사라지지 않도록 하려면 행 또는 열 머리글을 고정할 수 있습니다.  
  
 행과 열을 제어하는 방법은 테이블 또는 행렬이 있는지 여부에 따라 다릅니다. 테이블이 있는 경우 정적 멤버(행 및 열 머리글)가 계속 표시되도록 구성합니다. 행렬이 있는 경우 행 및 열 그룹 머리글이 계속 표시되도록 구성합니다.  
  
 Excel로 보고서를 내보내는 경우 머리글이 자동으로 고정되지 않습니다. Excel에서 창을 고정할 수 있습니다. 자세한 내용은 [Microsoft Excel로 내보내기&#40;보고서 작성기 및 SSRS&#41;](../report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md)의 **페이지 머리글 및 바닥글** 섹션을 참조하세요.  
  
> [!NOTE]  
>  테이블에 행 및 열 그룹이 있는 경우에도 스크롤하는 동안 이러한 그룹 머리글이 계속 표시되도록 할 수 없습니다.  
  
 다음 이미지에서는 표를 보여 줍니다.  
  
 ![테이블](../media/table.png "테이블")  
  
 다음 이미지에서는 행렬을 보여 줍니다.  
  
 ![행렬](../media/matrix.png "행렬")  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-keep-matrix-group-headers-visible-while-scrolling"></a>스크롤하는 동안 행렬 그룹 머리글을 계속 표시하려면  
  
1.  테이블릭스 데이터 영역에서 행, 열 또는 모퉁이 핸들을 마우스 오른쪽 단추로 클릭한 다음 **테이블릭스 속성**을 클릭합니다.  
  
2.  **일반** 탭의 **행 머리글** 또는 **열 머리글**아래에서 **스크롤하는 동안 머리글 계속 표시**를 선택합니다.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-keep-a-static-tablix-member-row-or-column-visible-while-scrolling"></a>스크롤하는 동안 정적 테이블릭스 멤버(행 또는 열)를 계속 표시하려면  
  
1.  디자인 화면에서 테이블의 아무 곳이나 클릭하여 그룹 창에 그룹과 함께 정적 멤버를 표시합니다.  
  
     ![그룹화 창](../media/grouppane-updated.png "그룹화 창")  
  
     행 그룹 창에 행 그룹 계층 구조의 정적 및 동적 멤버 계층이 표시되고 열 그룹 창에 열 그룹 계층 구조의 비슷한 정적 및 동적 멤버 계층이 표시됩니다.  
  
2.  그룹화 창의 오른쪽에서 아래쪽 화살표를 클릭한 다음 **고급 모드**를 클릭합니다.  
  
3.  스크롤하는 동안 계속 표시할 정적 멤버(행 또는 열)를 클릭합니다. 속성 창에 **테이블릭스 멤버** 속성이 표시됩니다.  
  
     ![테이블릭스 구성원 속성](../media/grouppane-tablixmember-updated.png "테이블릭스 구성원 속성")  
  
4.  속성 창에서 설정할 **FixedData** 에 `True`입니다.  
  
5.  스크롤하는 동안 계속 표시할 인접 멤버의 수만큼 이 과정을 반복합니다.  
  
6.  보고서를 미리 봅니다.  
  
 보고서 페이지를 아래로 또는 옆으로 이동할 때 정적 테이블릭스 멤버가 계속 표시됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [테이블릭스 데이터 영역&#40;보고서 작성기 및 SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [보고서 찾기, 보기 및 관리&#40;보고서 작성기 및 SSRS&#41;](../report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [보고서를 내보내는 &#40;보고서 작성기 및 SSRS&#41;](../report-builder/export-reports-report-builder-and-ssrs.md)   
 [그룹과 함께 머리글 및 바닥글 표시&#40;보고서 작성기 및 SSRS&#41;](display-headers-and-footers-with-a-group-report-builder-and-ssrs.md)   
 [여러 페이지에 행 및 열 머리글 표시&#40;보고서 작성기 및 SSRS&#41;](display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs.md)   
 [그룹화 창&#40;보고서 작성기&#41;](grouping-pane-report-builder.md)  
  
  
