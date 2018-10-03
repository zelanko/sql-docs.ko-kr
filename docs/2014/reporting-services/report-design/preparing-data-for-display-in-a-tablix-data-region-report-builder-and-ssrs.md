---
title: 테이블릭스 데이터 영역에 표시하기 위한 데이터 준비(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: fbb00dc6-7887-480c-b771-cab6fecb8dcc
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: be7dc2e586afc2a7e0ca7b2b1189716f8f5e5c40
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48156053"
---
# <a name="preparing-data-for-display-in-a-tablix-data-region-report-builder-and-ssrs"></a>테이블릭스 데이터 영역에 표시하기 위한 데이터 준비(보고서 작성기 및 SSRS)
  테이블릭스 데이터 영역에는 데이터 집합의 데이터가 표시됩니다. 데이터 집합에 대해 검색된 모든 데이터를 보거나 필터를 만들어 일부 데이터만 볼 수 있습니다. 또한 조건 식을 추가하여 Null 값을 채우거나 데이터 집합에 대한 쿼리를 수정하여 기존 열에 대한 정렬 순서를 정의하는 열을 포함할 수도 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="working-with-nulls-and-blanks-in-field-values"></a>Null 및 비어 있는 필드 값 작업  
 데이터 집합에서 필드 컬렉션에 대한 데이터는 Null과 빈 값을 포함하여 데이터 원본에서 런타임에 검색된 모든 값을 포함합니다. 일반적으로 Null 값과 비어 있는 값은 구분되지 않으며 대부분의 경우 이것이 정상입니다. 예를 들어, 숫자와 같은 집계 함수 [합계](report-builder-functions-sum-function.md) 하 고 [Avg](report-builder-functions-avg-function.md) null 값을 무시 합니다. 자세한 내용은 [집계 함수 참조&#40;보고서 작성기 및 SSRS&#41;](report-builder-functions-aggregate-functions-reference.md)를 참조하세요.  
  
 Null 값을 다르게 처리하려면 조건 식이나 사용자 지정 코드를 사용하여 Null 값에 대한 사용자 지정 값을 대체할 수 있습니다. 예를 들어 다음 식은 `Null` 필드에 Null 값이 나타날 때마다 `[Size]`이라는 텍스트로 대체합니다.  
  
```  
=IIF(Fields!Size.Value IS NOTHING,"Null",Fields!Size.Value)  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)] 데이터 원본에서 데이터를 검색하기 전에 데이터에서 Null 값을 제거하는 방법은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL Server 온라인 설명서 [의](http://go.microsoft.com/fwlink/?linkid=120955)설명서에 있는 "Null 값" 및 "Null 값 및 조인"을 참조하십시오.  
  
## <a name="handling-null-field-names"></a>Null 필드 이름 처리  
 식에서 Null 값을 테스트하는 것은 쿼리 결과 집합에 필드 자체가 있는 한 문제가 되지 않습니다. 사용자 지정 코드에서는 런타임에 데이터 원본으로부터 반환된 컬렉션 필드에 Null 필드가 나타나는지 여부를 테스트할 수 있습니다. 자세한 내용은 [데이터 집합 필드 컬렉션 참조&#40;보고서 작성기 및 SSRS&#41;](built-in-collections-dataset-fields-collection-references-report-builder.md)를 참조하세요.  
  
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
  
 이 정렬 순서에 따라 테이블 데이터 영역을 정렬하려면 세부 정보 그룹의 정렬 식을 `=Fields!ColorSortOrder.Value`로 설정합니다. 자세한 내용은 [데이터 영역의 데이터 정렬&#40;보고서 작성기 및 SSRS&#41;](sort-data-in-a-data-region-report-builder-and-ssrs.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 집합 필드 컬렉션&#40;보고서 작성기 및 SSRS&#41;](../report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [식&#40;보고서 작성기 및 SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [필터링, 그룹화 및 데이터 정렬 &#40;보고서 작성기 및 SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  
