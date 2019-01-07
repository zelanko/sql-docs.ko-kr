---
title: 보고서 계획(보고서 작성기) | Microsoft Docs
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
helpviewer_keywords:
- getting started
- report design
ms.assetid: 79113505-1ce8-4f8c-9260-d861838f7813
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 385d8cfa69e7407aec2f31ee99962b2a1200e4aa
ms.sourcegitcommit: c7febcaff4a51a899bc775a86e764ac60aab22eb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/30/2018
ms.locfileid: "52710854"
---
# <a name="planning-a-report-report-builder"></a>보고서 계획(보고서 작성기)
  보고서 작성기를 사용하여 다양한 종류의 페이지가 매겨진 보고서를 만들 수 있습니다. 예를 들어 판매 데이터, 마케팅 및 판매 추세를 요약하거나 자세히 보여 주는 보고서를 만들거나 운영 보고서 또는 대시보드를 만들 수 있습니다. 판매 주문, 제품 카탈로그 또는 양식 편지와 같은 서식 있는 텍스트를 사용한 보고서를 만들 수도 있습니다. 이러한 보고서는 모두 보고서 작성기에 있는 동일한 기본 빌딩 블록을 다르게 조합하여 만듭니다. 보고서를 만들기 전에 먼저 계획을 세우면 보다 유용하고 이해하기 쉬운 보고서를 만들 수 있습니다. 보고서 생성 작업을 시작하기 전에 고려해야 할 사항은 다음과 같습니다.  
  
-   **보고서를 렌더링할 형식**  
  
     [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 같은 브라우저에서 온라인으로 보고서를 렌더링하거나 Excel, Word 또는 PDF와 같은 다른 형식으로 보고서를 내보낼 수 있습니다. 내보내는 모든 형식에서 모든 기능을 사용할 수 있는 것은 아니므로 보고서의 최종 형식을 결정할 때는 신중을 기해야 합니다. 자세한 내용은 [보고서 내보내기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)에서 페이지 매김을 제어하는 데 사용되는 규칙을 이해해야 합니다.  
  
-   **보고서에 데이터를 표시하는 데 사용할 구조**  
  
     테이블 형식, 행렬(크로스탭 또는 피벗 테이블 보고서와 유사), 차트 또는 자유 형식 구조 중에서 선택하거나 이들을 조합하여 데이터를 나타낼 수 있습니다. 자세한 내용은 [테이블, 행렬 및 목록&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md) 및 [차트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)를 참조하세요.  
  
-   **원하는 보고서의 모양**  
  
     보고서 작성기는 보고서의 가독성을 높이고, 핵심 정보를 강조하고, 보고서를 읽는 사람이 보고서를 보다 쉽게 탐색할 수 있도록 하기 위해 보고서에 추가할 수 있는 다양한 보고서 항목을 제공합니다. 원하는 보고서 형태를 알면 입력란, 사각형, 이미지, 선 등의 보고서 항목이 필요한지 여부를 결정할 수 있습니다. 항목을 표시하거나 숨기고, 문서 구조를 추가하고, 드릴스루 보고서나 하위 보고서를 포함하고, 보고서에서 다른 보고서에 연결할 수도 있습니다. 자세한 내용은 [이미지, 입력란, 사각형 및 선&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/images-text-boxes-rectangles-and-lines-report-builder-and-ssrs.md) 및 [대화형 정렬, 문서 구조 및 링크&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)를 참조하세요.  
  
-   **보고서를 읽는 사람에게 표시할 데이터(보고서를 읽는 사용자에 맞게 데이터나 서식을 필터링해야 하는지 여부 검토)**  
  
     특정 사용자나 위치, 또는 특정 시간대로 보고서 범위를 좁힐 수 있습니다. 보고서 데이터를 필터링하려면 매개 변수를 사용하여 원하는 데이터만 검색하고 표시합니다. 자세한 내용은 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)에 대해 자세히 알아봅니다.  
  
-   **고유의 계산 필드를 만들어야 하는지 여부**  
  
     보고서에 꼭 맞는 필드가 데이터 원본과 데이터 세트에 없을 수도 있습니다. 이 경우 고유의 계산 필드를 만들어야 할 수도 있습니다. 예를 들어 단가에 수량을 곱해서 품목의 판매액을 구할 수 있습니다. 조건부 서식 및 기타 고급 기능을 제공하려는 경우에도 식을 사용합니다. 자세한 내용은 [식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)을 참조하세요.  
  
-   **보고서 항목을 처음에 숨길지 여부**  
  
     보고서를 처음 실행할 때 데이터 영역, 그룹 및 열과 같은 보고서 항목을 숨길지 여부를 검토합니다. 예를 들어 처음에는 요약 테이블만 제공하고 그 후에 세부 데이터로 드릴다운할 수 있습니다. 자세한 내용은 [드릴다운 동작&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/drilldown-action-report-builder-and-ssrs.md)을 참조하세요.  
  
-   **보고서 배달 방법**  
  
     사용자 본인에게만 필요한 정보가 포함된 보고서의 경우 보고서를 로컬 컴퓨터에 저장하고 보고서에 대한 작업을 계속하거나 보고서를 로컬에서 실행할 수 있습니다. 그러나 보고서를 다른 사용자와 공유하려면 보고서를 기본 모드에서 구성한 보고서 서버나 SharePoint 통합 모드에 있는 보고서 서버에 저장해야 합니다. 보고서를 서버에 저장하면 다른 사용자가 필요할 때마다 보고서를 실행할 수 있습니다. 또는 보고서 서버 관리자가 보고서에 대해 구독을 설정하거나 다른 개인 사용자에 대해 전자 메일 보고서 배달을 설정할 수 있습니다. 원하는 경우 특정 내보내기 형식으로 보고서가 배달되도록 할 수도 있습니다. 자세한 내용은 [보고서 찾기, 보기 및 관리&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server의 보고서 작성기](../../reporting-services/report-builder/report-builder-in-sql-server-2016.md)   
 [보고서 제작 개념&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/report-authoring-concepts-report-builder-and-ssrs.md)   
 [보고서 작성기 자습서](../../reporting-services/report-builder-tutorials.md)  
  
  
