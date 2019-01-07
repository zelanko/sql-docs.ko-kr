---
title: InScope 함수(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: a8cd209a-e5d3-4dce-ab2d-f271f6c54955
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: e37a25432e6e701ffd97bf95799b1a567748e1df
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48183793"
---
# <a name="inscope-function-report-builder-and-ssrs"></a>InScope 함수(보고서 작성기 및 SSRS)
  항목의 현재 인스턴스가 지정한 범위 내에 있는지 여부를 나타냅니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>구문  
  
```  
InScope(scope)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *범위*  
 (`String`) 데이터 집합, 데이터 영역 또는 범위를 지정 하는 그룹의 이름입니다.  
  
## <a name="return-type"></a>반환 형식  
 반환 된 `Boolean`합니다.  
  
## <a name="remarks"></a>Remarks  
 합니다 `InScope` 로 지정 된 범위의 멤버 자격에 대 한 보고서 항목의 현재 인스턴스 범위를 테스트 하는 함수를 *범위*매개 변수입니다.  
  
 *Scope* 는 식이 될 수 없습니다.  
  
 일반적인 용도 `InScope` 함수는 동적 있는 데이터 영역의 범위를 지정 합니다. 예를 들어 `InScope` 는 다양 한 보고서 이름과 다양 한 매개 변수 집합을 클릭 한 셀에 따라 제공할 데이터 영역 셀의 드릴스루 링크에 사용할 수 있습니다. 이러한 예는 다음과 같습니다.  
  
-   드릴스루 링크의 보고서 이름으로 사용된 다음 식은 클릭한 셀이 `ProductDetail` 그룹에 있으면 `Month` 보고서를 열고 그렇지 않으면 `ProductSummary` 보고서를 엽니다.  
  
    ```  
    =Iif(InScope("Month"), "ProductDetail", "ProductSummary")  
    ```  
  
-   다음 식을 사용 합니다 `Omit` 드릴스루 보고서 매개 변수의 속성은 매개 변수를 전달 대상 보고서를 클릭 한 셀이 있는 경우에는 `Product` 그룹.  
  
    ```  
    =Not(InScope("Product"))  
    ```  
  
 자세한 내용은 [집계 함수 참조&#40;보고서 작성기 및 SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) 및 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)를 참조하세요.  
  
## <a name="example"></a>예제  
 다음 코드 예에서는 항목의 현재 인스턴스가 `Product` 데이터 세트, 데이터 영역 또는 그룹 범위 내에 있는지 여부를 나타냅니다.  
  
```  
=InScope("Product")  
```  
  
## <a name="see-also"></a>관련 항목  
 [보고서에 사용 되는 식 &#40;보고서 작성기 및 SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [식의 데이터 형식&#40;보고서 작성기 및 SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [합계, 집계 및 기본 제공 컬렉션의 식 범위 &#40;보고서 작성기 및 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
