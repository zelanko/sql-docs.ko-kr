---
title: 재귀 계층 구조 그룹 만들기(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8b830ba5-4d64-4348-a2b1-76b9338a1462
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 00af8f5e46f2423714d396cb462dd81fde7f9dd6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="create-a-recursive-hierarchy-group-report-builder-and-ssrs"></a>재귀 계층 구조 그룹 만들기(보고서 작성기 및 SSRS)
[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 페이지를 매긴 보고서에서 재귀 계층 구조 그룹은 조직 계층의 관리자와 직원 관계에 대한 보고 구조와 같이 여러 계층 수준을 포함하는 단일 보고서 데이터 집합의 데이터를 구성합니다.  
  
 테이블의 데이터를 재귀 계층 구조 그룹으로 구성하기 전에 모든 계층 데이터를 포함하는 단일 데이터 집합이 있어야 합니다. 이 데이터 집합에는 그룹화할 항목과 항목을 그룹화할 기준에 대한 개별 필드가 포함되어 있습니다. 예를 들어 관리자에 속한 직원을 재귀적으로 그룹화할 데이터 집합에 이름, 직원 이름, 직원 ID 및 관리자 ID가 들어 있을 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-create-a-recursive-hierarchy-group"></a>재귀 계층 구조 그룹을 만들려면  
  
1.  디자인 뷰에서 테이블을 추가하고 표시할 데이터 집합 필드를 끕니다. 일반적으로 계층으로 표시할 필드가 첫 번째 열에 있습니다.  
  
2.  테이블에서 임의의 위치를 두 번 클릭하여 선택합니다. 그룹화 창에 선택한 테이블에 대한 그룹 세부 정보가 표시됩니다. 행 그룹 창에서 **세부 정보**를 마우스 오른쪽 단추로 클릭한 다음 **그룹 편집**을 클릭합니다. **그룹 속성** 대화 상자가 열립니다.  
  
3.  **그룹 식**에서 **추가**를 클릭합니다. 새 행이 표에 나타납니다.  
  
4.  **그룹화 대상** 목록에서 그룹화할 필드를 입력하거나 선택합니다.  
  
5.  **고급**을 클릭합니다.  
  
6.  **재귀적 부모** 목록에서 그룹화할 필드를 입력하거나 선택합니다.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     보고서를 실행합니다. 계층을 표시할 들여쓰기가 없는 경우에도 보고서에서 재귀 계층 구조 그룹을 표시합니다.  
  
## <a name="to-format-a-recursive-hierarchy-group-with-indent-levels"></a>들여쓰기 수준을 사용하여 재귀 계층 구조 그룹의 서식을 지정하려면  
  
1.  계층 형식을 표시하는 들여쓰기 수준을 추가할 필드를 포함하는 입력란을 클릭합니다. 입력란에 대한 속성이 속성 창에 표시됩니다.  
  
    > [!NOTE]  
    >  속성 창이 표시되지 않으면 **보기** 탭에서 **속성** 을 클릭합니다.  
  
2.  속성 창에서 **패딩** 노드를 확장하고 **왼쪽**을 클릭한 다음 드롭다운 목록에서 **\<식…>** 을 선택합니다.  
  
3.  식 창에서 다음 식을 입력합니다.  
  
     `=CStr(2 + (Level()*10)) + "pt"`  
  
     Padding 속성은 모두 *nnyy*형식의 문자열을 요구합니다. 여기서 *nn* 은 숫자이고, *yy* 는 측정 단위입니다. 예 식은 **Level** 함수를 사용하여 재귀 수준에 따라 안쪽 여백의 크기를 늘리는 문자열을 만듭니다. 예를 들어 1 수준의 행은 (2 + (1\*10))=12pt의 패딩으로, 3 수준의 행은 (2 + (3\*10))=32pt의 패딩으로 늘어납니다. **Level** 함수에 대한 자세한 내용은 [Level 함수](../../reporting-services/report-design/report-builder-functions-level-function.md)를 참조하십시오.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     보고서를 실행합니다. 보고서에 그룹화된 데이터의 계층 뷰가 표시됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [재귀 계층 구조 그룹 생성&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)   
 [데이터 필터링, 그룹화 및 정렬&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [집계 함수 참조&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)   
 [테이블&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [행렬&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [목록&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [테이블, 행렬 및 목록&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
