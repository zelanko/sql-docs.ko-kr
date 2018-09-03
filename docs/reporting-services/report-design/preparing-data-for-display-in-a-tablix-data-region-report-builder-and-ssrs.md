---
title: 테이블릭스 데이터 영역에 표시하기 위한 데이터 준비(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 08/17/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: fbb00dc6-7887-480c-b771-cab6fecb8dcc
caps.latest.revision: 5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0106cac1213e9037008bc9c89b0ef501457c6446
ms.sourcegitcommit: 9cd01df88a8ceff9f514c112342950e03892b12c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2018
ms.locfileid: "40405600"
---
# <a name="preparing-data-for-display-in-a-tablix-data-region-report-builder-and-ssrs"></a>테이블릭스 데이터 영역에 표시하기 위한 데이터 준비(보고서 작성기 및 SSRS)
  테이블릭스 데이터 영역에는 데이터 집합의 데이터가 표시됩니다. 데이터 집합에 대해 검색된 모든 데이터를 보거나 필터를 만들어 일부 데이터만 볼 수 있습니다. 또한 조건 식을 추가하여 Null 값을 채우거나 데이터 집합에 대한 쿼리를 수정하여 기존 열에 대한 정렬 순서를 정의하는 열을 포함할 수도 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="working-with-nulls-and-blanks-in-field-values"></a>Null 및 비어 있는 필드 값 작업  
 데이터 집합에서 필드 컬렉션에 대한 데이터는 Null과 빈 값을 포함하여 데이터 원본에서 런타임에 검색된 모든 값을 포함합니다. 일반적으로 Null 값과 비어 있는 값은 구분되지 않으며 대부분의 경우 이것이 정상입니다. 예를 들어 [Sum](../../reporting-services/report-design/report-builder-functions-sum-function.md) 및 [Avg](../../reporting-services/report-design/report-builder-functions-avg-function.md) 와 같은 숫자 집계 함수는 Null 값을 무시합니다. 자세한 내용은 [집계 함수 참조&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)를 참조하세요.  
  
 Null 값을 다르게 처리하려면 조건 식이나 사용자 지정 코드를 사용하여 Null 값에 대한 사용자 지정 값을 대체할 수 있습니다. 예를 들어 다음 식은 `Null` 필드에 Null 값이 나타날 때마다 `[Size]`이라는 텍스트로 대체합니다.  
  
```  
=IIF(Fields!Size.Value IS NOTHING,"Null",Fields!Size.Value)  
```  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 원본에서 데이터를 검색하기 전에 null을 제거하는 방법에 대한 자세한 내용은 [NULL 및 UNKNOWN(Transact-SQL)](../../t-sql/language-elements/null-and-unknown-transact-sql.md)을 참조하세요.  
  
## <a name="handling-null-field-names"></a>Null 필드 이름 처리  
 식에서 Null 값을 테스트하는 것은 쿼리 결과 집합에 필드 자체가 있는 한 문제가 되지 않습니다. 사용자 지정 코드에서는 런타임에 데이터 원본으로부터 반환된 컬렉션 필드에 Null 필드가 나타나는지 여부를 테스트할 수 있습니다. 자세한 내용은 [데이터 집합 필드 컬렉션 참조&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/built-in-collections-dataset-fields-collection-references-report-builder.md)를 참조하세요.  
  
## <a name="adding-a-sort-order-column"></a>정렬 순서 열 추가  
 기본적으로 데이터 집합 필드의 값을 사전순으로 정렬할 수 있습니다. 다른 순서로 정렬하려면 데이터 집합에 데이터 영역에서의 정렬 순서를 정의하는 새 열을 추가합니다. 예를 들어 `[Color]` 필드에 대해 정렬을 수행하고 흰색과 검정색 항목을 먼저 정렬하려면 다음 쿼리처럼 `[ColorSortOrder]`열을 추가합니다.  
  
```  
SELECT ProductID, p.Name, Color,  
   CASE  
      WHEN p.Color = 'White' THEN 1  
      WHEN p.Color = 'Black' THEN 2  
      WHEN p.Color = 'Blue' THEN 3  
      WHEN p.Color = 'Yellow' THEN 4  
      ELSE 5  
   END As ColorSortOrder  
FROM Production.Product p  
```  
  
 이 정렬 순서에 따라 테이블 데이터 영역을 정렬하려면 세부 정보 그룹의 정렬 식을 `=Fields!ColorSortOrder.Value`로 설정합니다. 자세한 내용은 [데이터 영역의 데이터 정렬&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/sort-data-in-a-data-region-report-builder-and-ssrs.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 집합 필드 컬렉션&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [데이터 필터링, 그룹화 및 정렬&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  
