---
title: 보고서 매개 변수 추가, 변경 또는 삭제(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d44a8e0a-10cf-4502-9391-09743ffc9bad
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9c6751843d730f01f609b19069bda900a4e9aebe
ms.sourcegitcommit: b70b99c2e412b4d697021f3bf1a92046aafcbe37
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/13/2018
ms.locfileid: "40405325"
---
# <a name="add-change-or-delete-a-report-parameter-report-builder-and-ssrs"></a>보고서 매개 변수 추가, 변경 또는 삭제(보고서 작성기 및 SSRS)
  보고서 매개 변수를 사용하면 보고서 데이터를 선택하고, 관련된 보고서를 서로 연결하고, 다양하게 보고서를 표현할 수 있습니다. 기본값 및 사용 가능한 값 목록을 제공할 수 있으며 사용자는 선택 항목을 변경할 수 있습니다.  
  
 보고서를 게시한 후에는 보고서 서버에서 보고서 매개 변수의 기본값, 사용 가능한 값 및 기타 속성을 변경할 수 있습니다. 링크된 보고서를 만들어 여러 기본 매개 변수 값 집합을 제공할 수 있습니다. 자세한 내용은 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)를 참조하세요.  
  
 이 문서에서는 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]의 페이지를 매긴 보고서 또는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 보고서 디자이너에 보고서 매개 변수를 추가하는 방법에 대해 설명합니다. [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)]에서 모바일 보고서에 보고서 매개 변수를 추가할 수도 있습니다. 자세한 내용은 [Create mobile reports with SQL Server Mobile Report Publisher](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md) 을 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-or-edit-a-report-parameter"></a>보고서 매개 변수를 추가하거나 편집하려면  
  
1.  [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 또는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에 있는 보고서 디자이너의 **보고서 데이터** 창에서 **매개 변수** 노드를 마우스 오른쪽 단추로 클릭하고 **매개 변수 추가**를 클릭합니다. **보고서 매개 변수 속성** 대화 상자가 열립니다.  
  
2.  **이름**에 매개 변수의 이름을 입력하거나 기본 이름을 그대로 사용합니다.  
  
3.  **프롬프트**에 사용자가 보고서를 실행할 때 매개 변수 입력란 옆에 표시되는 텍스트를 입력합니다.  
  
4.  **데이터 형식**에서 매개 변수 값에 대한 데이터 형식을 선택합니다.  
  
5.  매개 변수에 빈 값을 포함할 수 있는 경우 **빈 값 허용**을 선택합니다.  
  
6.  매개 변수에 Null 값을 포함할 수 있는 경우 **Null 값 허용**을 선택합니다.  
  
7.  사용자가 매개 변수 값을 둘 이상 선택할 수 있도록 하려면 **다중 값 허용**을 선택합니다.  
  
8.  표시 여부 옵션을 설정합니다.  
  
    -   보고서 위쪽의 도구 모음에 매개 변수를 표시하려면 **표시**를 선택합니다.  
  
    -   매개 변수를 숨겨서 도구 모음에 표시하지 않으려면 **숨김**을 선택합니다.  
  
    -   매개 변수를 숨겨서 보고서가 게시된 후 보고서 서버에서 수정되지 않도록 하려면 **내부**를 선택합니다. 그러면 보고서 매개 변수는 보고서 정의에서만 볼 수 있습니다. 이 옵션을 사용하려면 기본값을 설정하거나 Null 값을 허용하도록 설정해야 합니다.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-delete-a-report-parameter"></a>보고서 매개 변수를 삭제하려면  
  
1.  **보고서 데이터** 창에서 **매개 변수** 노드를 확장합니다.  
  
2.  보고서 매개 변수를 마우스 오른쪽 단추로 클릭하고 **삭제**를 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 매개 변수의 사용 가능한 값 추가, 변경 또는 삭제&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-available-values-for-a-report-parameter.md)   
 [보고서 매개 변수의 기본값 추가, 변경 또는 삭제&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-default-values-for-a-report-parameter.md)   
 [보고서 매개 변수의 순서 변경&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)   
 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [보고서에 연계 매개 변수 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [자습서: 보고서에 매개 변수 추가&#40;보고서 작성기&#41;](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [데이터 집합 필터, 데이터 영역 필터 및 그룹 필터 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [매개 변수 컬렉션 참조&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)   
 [보고서에 다중 값 매개 변수 추가](../../reporting-services/report-design/add-a-multi-value-parameter-to-a-report.md)  
  
  
