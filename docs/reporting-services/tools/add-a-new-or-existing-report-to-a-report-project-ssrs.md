---
title: "보고서 프로젝트에 새 보고서 또는 기존 보고서 추가(SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: reports [Reporting Services], creating
ms.assetid: 8bc0bb53-ad8a-464d-bb6a-7fea5fa62c5c
caps.latest.revision: "20"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 6edee3df21691e6f9e53a167bb1bd1bce502e76a
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="add-a-new-or-existing-report-to-a-report-project-ssrs"></a>보고서 프로젝트에 새 보고서 또는 기존 보고서 추가(SSRS)
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 보고서 마법사를 사용하거나 프로젝트에 새 보고서를 추가하여 새 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 페이지를 매긴 보고서를 추가할 수 있습니다. 기본 보고서를 추가할 수도 있습니다. 보고서를 추가한 후 프로젝트의 **보고서** 폴더 아래에 나열된 보고서 이름을 볼 수 있습니다.  
  
> [!NOTE]  
>  기존 데이터 원본의 보고서를 미리 보려면 보고서 제작 클라이언트의 데이터 원본에 대한 사용 권한이 있어야 합니다. 자세한 내용은 [데이터 연결, 데이터 원본 및 연결 문자열](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)을 참조하세요.  
  
 보고서를 추가한 후 데이터 원본 및 데이터 집합을 정의하고 보고서 레이아웃을 디자인할 수 있습니다. 시작하려면 [기본 테이블 보고서 만들기&#40;SSRS 자습서&#41;](../../reporting-services/create-a-basic-table-report-ssrs-tutorial.md) 또는 [테이블&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)을 참조하세요.  
  
## <a name="to-add-a-new-report-using-the-report-wizard"></a>보고서 마법사를 사용하여 새 보고서를 추가하려면  
  
1.  솔루션 탐색기에서 보고서 폴더를 마우스 오른쪽 단추로 클릭한 다음 **새 보고서 추가**를 클릭합니다. **보고서 마법사** 대화 상자가 열립니다.  
  
     마법사는 데이터 원본을 만들고, 쿼리를 사용하여 데이터 집합을 만들고, 그룹을 정의하고, 레이아웃을 지정하고, 보고서를 만드는 단계를 안내합니다. 이 단계는 다음과 같습니다.  
  
    -   **데이터 원본 선택.** 보고서를 만드는 첫 번째 단계로 데이터 원본을 정의합니다. 보고서 마법사는 보고서 프로젝트의 전체 공유 데이터 원본 목록뿐만 아니라 새 데이터 원본을 만드는 옵션도 제공합니다.  
  
    -   **쿼리 디자인.** 두 번째 단계로 쿼리를 디자인합니다. 쿼리 문자열을 직접 입력하거나 쿼리 디자이너를 사용하여 작성하거나 다른 보고서에서 쿼리를 가져올 수 있습니다. 쿼리 디자이너에 대한 자세한 내용은 [Reporting Services Query Designers](http://msdn.microsoft.com/library/07efd3f1-804f-45f7-b62a-3e727a3d9835)를 참조하십시오.  
  
    -   **보고서 유형 선택.** 세 번째 단계로 원하는 보고서 유형을 선택합니다. 테이블 형식 보고서나 행렬 보고서를 선택할 수 있습니다. 테이블 형식 보고서의 열 수는 고정되어 있지만 행렬, 즉 크로스탭 보고서는 쿼리 결과에 따라 열 수가 달라집니다. 지도 보고서에는 지리적 배경과 함께 분석 데이터가 표시됩니다.  
  
    -   **보고서 이름을 지정합니다.**  마지막 단계로 보고서의 이름을 지정하고 보고서에 포함할 필드를 확인합니다. 모든 단계가 완료되면 보고서 디자이너는 보고서를 만들어 보고서 서버 프로젝트에 추가합니다.  
  
## <a name="to-add-a-new-blank-report"></a>새 보고서를 추가하려면  
  
1.  **프로젝트** 메뉴에서 **새 항목 추가**를 클릭합니다.  
  
2.  **템플릿**에서 **보고서**를 클릭합니다.  
  
3.  **추가**를 클릭합니다.  
  
     새 보고서가 프로젝트에 추가되어 디자인 화면에 표시됩니다.  
  
## <a name="to-add-an-existing-report"></a>기존 보고서를 추가하려면  
  
1.  **프로젝트** 메뉴에서 **추가**를 클릭한 다음 **기존 항목**을 클릭합니다.  
  
2.  .rdl 파일의 위치를 찾아서 파일을 선택한 다음 **추가**를 클릭합니다.  
  
     보고서가 **보고서** 폴더 아래의 프로젝트에 추가됩니다. 프로젝트를 닫고 다시 열면 보고서가 사전순으로 정렬됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Reporting Services&#40;SSRS&#41; 자습서](../../reporting-services/reporting-services-tutorials-ssrs.md)  
 추가 질문이 있으신가요? [Reporting Services 포럼을 이용해 보세요.](http://go.microsoft.com/fwlink/?LinkId=620231)
  
  
