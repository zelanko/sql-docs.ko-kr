---
title: 여러 페이지에 행 및 열 머리글 표시(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 2422b1e2-822f-4379-9d7f-9afebb350e3f
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 642be62739a87a0fff4990f574a2c6f57f6e5c91
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48136493"
---
# <a name="display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs"></a>여러 페이지에 행 및 열 머리글 표시(보고서 작성기 및 SSRS)
  여러 페이지에 걸쳐 있는 테이블릭스 데이터 영역에 대해 페이지마다 행 및 열 머리글을 반복할지 여부를 제어할 수 있습니다. 테이블릭스 데이터 영역은 테이블, 행렬 또는 목록일 수 있습니다.  
  
 행과 열을 제어하는 방법은 테이블릭스 데이터 영역에 그룹 머리글이 있는지 여부에 따라 달라집니다. 그룹 머리글이 있는 테이블릭스 데이터 영역을 클릭하면 다음 그림에서처럼 테이블릭스 영역이 점선으로 표시됩니다.  
  
 ![테이블 릭 스 데이터 영역](../media/rs-tablixareas.gif "테이블 릭 스 데이터 영역")  
  
 새 테이블 또는 행렬 마법사나 새 차트 마법사를 사용하거나, 그룹화 창에 필드를 추가하거나, 상황에 맞는 메뉴를 사용하여 그룹을 추가하면 행 및 열 그룹 머리글이 자동으로 만들어집니다. 테이블릭스 데이터 영역에 테이블릭스 본문 영역만 있고 그룹 머리글은 없는 경우 행과 열은 테이블릭스 멤버입니다.  
  
 정적 멤버의 경우에는 상단 인접 행 또는 측면 인접 열을 여러 페이지에 표시할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-display-row-headers-on-multiple-pages"></a>여러 페이지에 행 머리글을 표시하려면  
  
1.  테이블릭스 데이터 영역에서 행, 열 또는 모퉁이 핸들을 마우스 오른쪽 단추로 클릭한 다음 **테이블릭스 속성**을 클릭합니다.  
  
2.  **행 머리글**에서 **각 페이지에서 머리글 행 반복**을 선택합니다.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-display-column-headers-on-multiple-pages"></a>여러 페이지에 열 머리글을 표시하려면  
  
1.  테이블릭스 데이터 영역에서 행, 열 또는 모퉁이 핸들을 마우스 오른쪽 단추로 클릭한 다음 **테이블릭스 속성**을 클릭합니다.  
  
2.  **열 머리글**에서 **각 페이지에서 머리글 열 반복**을 선택합니다.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-display-a-static-tablix-member-row-or-column-on-multiple-pages"></a>정적 테이블릭스 멤버(행 또는 열)를 여러 페이지에 표시하려면  
  
1.  디자인 화면에서 테이블릭스 데이터 영역의 행 또는 열 핸들을 클릭하여 선택합니다. 그룹화 창에 행 및 열 그룹이 표시됩니다.  
  
2.  그룹화 창의 오른쪽에서 아래쪽 화살표를 클릭한 다음 **고급 모드**를 클릭합니다. 행 그룹 창에 행 그룹 계층 구조의 정적 및 동적 멤버 계층이 표시되고 열 그룹 창에 열 그룹 계층 구조의 비슷한 정적 및 동적 멤버 계층이 표시됩니다.  
  
3.  스크롤할 때 계속 표시할 정적 멤버(행 또는 열)에 해당하는 정적 멤버를 클릭합니다. 속성 창에 **테이블릭스 멤버** 속성이 표시됩니다.  
  
     속성 창이 표시되지 않는 경우 보고서 작성기 창의 맨 위에서 **보기** 탭을 클릭한 다음 **속성**을 클릭합니다.  
  
4.  속성 창에서 **RepeatOnNewPage** 를 True로 설정합니다.  
  
5.  **KeepWithGroup** 을 이후로 설정합니다.  
  
6.  반복할 인접 멤버의 수만큼 이 과정을 반복합니다.  
  
7.  보고서를 미리 봅니다.  
  
 테이블릭스 데이터 영역이 걸쳐 있는 보고서의 각 페이지를 볼 때 정적 테이블릭스 멤버가 각 페이지에서 반복됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서 찾기, 보기 및 관리&#40;보고서 작성기 및 SSRS&#41;](../report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [보고서를 내보내는 &#40;보고서 작성기 및 SSRS&#41;](../report-builder/export-reports-report-builder-and-ssrs.md)   
 [나누기, 머리글, 열 및 행 제어 페이지 &#40;보고서 작성기 및 SSRS&#41;](controlling-page-breaks-headings-columns-and-rows-report-builder-and-ssrs.md)   
 [그룹과 함께 머리글 및 바닥글 표시&#40;보고서 작성기 및 SSRS&#41;](display-headers-and-footers-with-a-group-report-builder-and-ssrs.md)   
 [보고서를 스크롤할 때 머리글 계속 표시 &#40;보고서 작성기 및 SSRS&#41;](keep-headers-visible-when-scrolling-through-a-report-report-builder-and-ssrs.md)  
  
  
