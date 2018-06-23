---
title: 재귀 계층 구조 그룹 만들기(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8b830ba5-4d64-4348-a2b1-76b9338a1462
caps.latest.revision: 7
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 0a82a52b230564b81261cece8f61ea56cdb21da8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36186472"
---
# <a name="create-a-recursive-hierarchy-group-report-builder-and-ssrs"></a>재귀 계층 구조 그룹 만들기(보고서 작성기 및 SSRS)
  재귀 계층 구조 그룹은 조직 계층의 관리자와 직원 관계에 대한 보고 구조와 같이 여러 계층 수준을 포함하는 단일 보고서 데이터 집합의 데이터를 구성합니다.  
  
 테이블의 데이터를 재귀 계층 구조 그룹으로 구성하기 전에 모든 계층 데이터를 포함하는 단일 데이터 집합이 있어야 합니다. 이 데이터 집합에는 그룹화할 항목과 항목을 그룹화할 기준에 대한 개별 필드가 포함되어 있습니다. 예를 들어 관리자에 속한 직원을 재귀적으로 그룹화할 데이터 집합에 이름, 직원 이름, 직원 ID 및 관리자 ID가 들어 있을 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-create-a-recursive-hierarchy-group"></a>재귀 계층 구조 그룹을 만들려면  
  
1.  디자인 뷰에서 테이블을 추가하고 표시할 데이터 집합 필드를 끕니다. 일반적으로 계층으로 표시할 필드가 첫 번째 열에 있습니다.  
  
2.  테이블에서 임의의 위치를 두 번 클릭하여 선택합니다. 그룹화 창에 선택한 테이블에 대한 그룹 세부 정보가 표시됩니다. 행 그룹 창에서 **세부 정보**를 마우스 오른쪽 단추로 클릭한 다음 **그룹 편집**을 클릭합니다. **그룹 속성** 대화 상자가 열립니다.  
  
3.  **그룹 식**에서 **추가**를 클릭합니다. 새 행이 표에 나타납니다.  
  
4.  **그룹화 대상** 목록에서 그룹화할 필드를 입력하거나 선택합니다.  
  
5.  **고급**을 클릭합니다.  
  
6.  **재귀적 부모** 목록에서 그룹화할 필드를 입력하거나 선택합니다.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     보고서를 실행합니다. 계층을 표시할 들여쓰기가 없는 경우에도 보고서에서 재귀 계층 구조 그룹을 표시합니다.  
  
### <a name="to-format-a-recursive-hierarchy-group-with-indent-levels"></a>들여쓰기 수준을 사용하여 재귀 계층 구조 그룹의 서식을 지정하려면  
  
1.  계층 형식을 표시하는 들여쓰기 수준을 추가할 필드를 포함하는 입력란을 클릭합니다. 입력란에 대한 속성이 속성 창에 표시됩니다.  
  
    > [!NOTE]  
    >  속성 창이 표시되지 않으면 **보기** 탭에서 **속성** 을 클릭합니다.  
  
2.  속성 창에서 확장의 `Padding` 노드를 클릭 하 여 **왼쪽**, 드롭 다운 목록에서 선택  **\<식... >** 합니다.  
  
3.  식 창에서 다음 식을 입력합니다.  
  
     `=CStr(2 + (Level()*10)) + "pt"`  
  
     Padding 속성은 모두 *nnyy*형식의 문자열을 요구합니다. 여기서 *nn* 은 숫자이고, *yy* 는 측정 단위입니다. 사용 하는 문자열을 작성 하는 예제 식은 `Level` 재귀 수준에 따라 안쪽 여백의 크기를 늘리려면 함수입니다. 예를 들어 1 수준의 행은 (2 + (1\*10))=12pt의 패딩으로, 3 수준의 행은 (2 + (3\*10))=32pt의 패딩으로 늘어납니다. 에 대 한 내용은 `Level` 함수, 참조 [수준](report-builder-functions-level-function.md)합니다.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     보고서를 실행합니다. 보고서에 그룹화된 데이터의 계층 뷰가 표시됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [재귀 계층 구조 그룹 생성 &#40;보고서 작성기 및 SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)   
 [데이터 필터링, 그룹화 및 정렬&#40;보고서 작성기 및 SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [집계 함수 참조 &#40;보고서 작성기 및 SSRS&#41;](report-builder-functions-aggregate-functions-reference.md)   
 [테이블&#40;보고서 작성기 및 SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [행렬&#40;보고서 작성기 및 SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [목록&#40;보고서 작성기 및 SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [테이블, 행렬 및 목록&#40;보고서 작성기 및 SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  