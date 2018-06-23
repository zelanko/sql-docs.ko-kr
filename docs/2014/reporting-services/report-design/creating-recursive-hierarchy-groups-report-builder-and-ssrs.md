---
title: 재귀 계층 구조 그룹 생성(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 06eccab6-4089-46e8-a84f-5bf3bbe0c23b
caps.latest.revision: 7
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 52410faf7827c6692575aff641070565d0ef6243
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36185347"
---
# <a name="creating-recursive-hierarchy-groups-report-builder-and-ssrs"></a>재귀 계층 구조 그룹 생성(보고서 작성기 및 SSRS)
  부모와 자식 간의 관계가 데이터 집합의 필드는 나타내는 재귀 데이터를 표시 하려면 자식 필드에 따라 데이터 영역 그룹 식을 설정 하 고 부모 필드에 따라 부모 속성을 설정할 수 있습니다.  
  
 계층적 데이터를 표시하는 것은 조직도의 직원과 같은 재귀 계층 구조 그룹에 일반적입니다. 데이터 집합에는 직원 및 관리자 목록이 포함되며 관리자 이름은 직원 목록에도 나타납니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="creating-recursive-hierarchies"></a>재귀 계층 만들기  
 테이블릭스 데이터 영역에서 재귀 계층 구조를 작성하려면 자식 데이터를 지정하는 필드로 그룹 식을 설정하고 부모 데이터를 지정하는 필드로 그룹의 Parent 속성을 설정해야 합니다. 예를 들어 직원 ID 및 관리자 ID에 대한 필드를 포함하는 데이터 집합이 있으며 직원이 관리자에게 보고하는 경우 그룹 식을 직원 ID로 설정하고 Parent 속성을 관리자 ID로 설정합니다.  
  
 재귀 계층 구조로 정의된 그룹, 즉 Parent 속성을 사용하는 그룹에는 그룹 식이 하나만 있을 수 있습니다. 입력란 안쪽 여백에 `Level` 함수를 사용하여 계층에서의 수준을 기준으로 직원 이름을 들여쓸 수 있습니다.  
  
 자세한 내용은 [데이터 영역에서 그룹 추가 또는 삭제&#40;보고서 작성기 및 SSRS&#41;](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md) 및 [재귀 계층 구조 그룹 만들기&#40;보고서 작성기 및 SSRS&#41;](create-a-recursive-hierarchy-group-report-builder-and-ssrs.md)를 참조하세요.  
  
### <a name="aggregate-functions-that-support-recursion"></a>재귀를 지원하는 집계 함수  
 매개 변수 *Recursive* 를 허용하는 Reporting Services 집계 함수를 사용하여 재귀 계층 구조의 요약 데이터를 계산할 수 있습니다. The following functions accept `Recursive` as a parameter: [Sum](report-builder-functions-sum-function.md), [Avg](report-builder-functions-avg-function.md), [Count](report-builder-functions-count-function.md), [CountDistinct](report-builder-functions-countdistinct-function.md), [CountRows](report-builder-functions-countrows-function.md), [Max](report-builder-functions-max-function.md), [Min](report-builder-functions-min-function.md), [StDev](report-builder-functions-stdev-function.md), [StDevP](report-builder-functions-stdevp-function.md), [Sum](report-builder-functions-sum-function.md), [Var](report-builder-functions-var-function.md), and [VarP](report-builder-functions-varp-function.md). 자세한 내용은 [집계 함수 참조&#40;보고서 작성기 및 SSRS&#41;](report-builder-functions-aggregate-functions-reference.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [테이블, 행렬 및 목록&#40;보고서 작성기 및 SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [테이블릭스 데이터 영역&#40;보고서 작성기 및 SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [집계 함수 참조 &#40;보고서 작성기 및 SSRS&#41;](report-builder-functions-aggregate-functions-reference.md)   
 [테이블&#40;보고서 작성기 및 SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [행렬&#40;보고서 작성기 및 SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [목록&#40;보고서 작성기 및 SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [테이블, 행렬 및 목록&#40;보고서 작성기 및 SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  