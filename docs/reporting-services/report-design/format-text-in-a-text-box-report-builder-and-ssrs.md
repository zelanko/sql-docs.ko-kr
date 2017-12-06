---
title: "입력란의 텍스트 서식 지정(보고서 작성기 및 SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: df0794b5-96b0-4034-bd17-1be7f31e29db
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 4752ac55673b7c208a2d051da928fee1404693f9
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="format-text-in-a-text-box-report-builder-and-ssrs"></a>입력란의 텍스트 서식 지정(보고서 작성기 및 SSRS)
  입력란에 있는 텍스트 부분의 서식을 개별적으로 지정하고 한 입력란 내에 자리 표시자 텍스트와 정적 텍스트를 함께 사용할 수 있습니다. 여러 서식을 함께 사용하고 자리 표시자 텍스트를 추가하는 이 기능을 통해 보고서의 텍스트에 대한 편지 병합 또는 템플릿을 만들 수 있습니다. 자리 표시자를 사용하여 모든 식을 개별적으로 정의하고 서식을 지정할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-combine-multiple-formats-in-a-text-box"></a>입력란에서 여러 서식을 함께 사용하려면  
  
1.  **삽입** 탭에서 **입력란**을 클릭합니다. 디자인 화면을 클릭한 다음 끌어 원하는 크기의 상자를 만듭니다.  
  
2.  입력란 내에서 서식을 지정할 텍스트를 선택합니다.  
  
3.  선택한 텍스트를 마우스 오른쪽 단추로 클릭하고 **텍스트 속성**을 클릭합니다.  
  
4.  서식 옵션을 설정합니다. 예를 들어 **일반** 탭에서 다음과 같이 작업합니다.  
  
    -   **도구 설명** 도구 설명을 반환하는 식 또는 텍스트를 입력합니다. 보고서의 항목 위에 포인터를 놓으면 도구 설명이 나타납니다.  
  
    -   **태그 형식** 선택한 텍스트를 렌더링할 방식을 나타내기 위한 옵션을 선택합니다.  
  
         **일반 텍스트** 선택한 텍스트를 단순 텍스트로 표시합니다. HTML은 리터럴 텍스트로 처리됩니다.  
  
         **HTML**  선택한 텍스트를 HTML로 표시합니다. 자리 표시자의 식 값에 유효한 HTML 태그가 포함된 경우 이러한 태그는 HTML로 렌더링됩니다. 자세한 내용은 [보고서로 HTML 가져오기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/importing-html-into-a-report-report-builder-and-ssrs.md)를 참조하세요.  
  
5.  **확인**을 클릭합니다.  
  
6.  서식을 지정할 나머지 텍스트에 대해 2~5단계를 반복합니다.  
  
### <a name="to-format-text-and-placeholders-differently-in-the-same-text-box"></a>같은 입력란에서 텍스트 및 자리 표시자의 서식을 다르게 지정하려면  
  
1.  **삽입** 탭에서 **목록**을 클릭합니다. 디자인 화면을 클릭한 다음 끌어 원하는 크기의 상자를 만듭니다. **데이터 집합 속성** 대화 상자가 열립니다. 보고서에 포함된 데이터 집합이나 공유 데이터 집합을 사용할 수 있습니다. 자세한 내용은 [데이터 집합 속성 대화 상자, 쿼리&#40;보고서 작성기&#41;](../../reporting-services/report-data/dataset-properties-dialog-box-query-report-builder.md) 또는 [데이터 집합 속성 대화 상자, 쿼리](http://msdn.microsoft.com/library/1fa34a4b-7de0-4e92-99fa-bc28a206773f)를 참조하세요.  
  
2.  **삽입** 탭에서 **입력란**을 클릭합니다. 목록을 클릭한 다음 끌어 원하는 크기의 상자를 만듭니다.  
  
3.  입력란에 **My Field**와 같은 레이블을 입력합니다.  
  
4.  데이터 집합의 필드를 입력란으로 끕니다. 해당 필드에 대한 자리 표시자가 만들어집니다.  
  
5.  기본 서식의 경우 자리 표시자 텍스트를 선택한 후 **홈** 탭의 **글꼴** 그룹에서 서식 옵션 중 하나를 클릭합니다. 예를 들어 **굵게** 단추를 클릭합니다.  
  
     다른 서식 옵션을 보려면 자리 표시자 텍스트를 마우스 오른쪽 단추로 클릭한 다음 **자리 표시자 속성**을 클릭합니다.  
  
6.  **확인**을 클릭합니다. 보고서 디자인 뷰의 입력란에 "**My Field**: [*FieldName*]"을 포함해야 합니다. 여기서 *FieldName* 은 필드 이름입니다.  
  
7.  **실행**을 클릭합니다.  
  
 목록은 필드의 각 값에 대해 한 번씩 반복되고 매번 *FieldName* 은 데이터 집합에 있는 해당 필드의 값으로 바뀝니다.  
  
## <a name="see-also"></a>관련 항목:  
 [입력란&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/text-boxes-report-builder-and-ssrs.md)   
 [텍스트 및 자리 표시자 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [보고서에 사용되는 식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [보고서에 HTML 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-html-into-a-report-report-builder-and-ssrs.md)   
 [테이블, 행렬 및 목록&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [숫자 및 날짜 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [자리 표시자 속성 대화 상자, 일반&#40;보고서 작성기 및 SSRS&#41;](http://msdn.microsoft.com/library/7a867736-a3b0-4b5a-b3e5-fe7c8d7618a8)  
  
  
