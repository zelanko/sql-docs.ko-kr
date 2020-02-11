---
title: InScope 함수(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: a8cd209a-e5d3-4dce-ab2d-f271f6c54955
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 84f9b681ee632e922f5ab349bf1a72fbea63f911
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66105246"
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
 (`String`) 범위를 지정하는 데이터 세트, 데이터 영역 또는 그룹의 이름입니다.  
  
## <a name="return-type"></a>반환 형식  
 
  `Boolean`을 반환합니다.  
  
## <a name="remarks"></a>설명  
 함수 `InScope` 는 *범위*매개 변수로 지정 된 범위의 멤버 자격에 대해 보고서 항목의 현재 인스턴스 범위를 테스트 합니다.  
  
 *Scope* 는 식이 될 수 없습니다.  
  
 
  `InScope` 함수는 일반적으로 동적으로 범위가 지정되는 데이터 영역에 사용됩니다. 예를 들어 데이터 영역 셀의 드릴스루 링크에 `InScope`를 사용하여 클릭한 셀에 따라 다양한 보고서 이름과 다양한 매개 변수 집합을 제공할 수 있습니다. 이러한 예는 다음과 같습니다.  
  
-   드릴스루 링크의 보고서 이름으로 사용된 다음 식은 클릭한 셀이 `ProductDetail` 그룹에 있으면 `Month` 보고서를 열고 그렇지 않으면 `ProductSummary` 보고서를 엽니다.  
  
    ```  
    =Iif(InScope("Month"), "ProductDetail", "ProductSummary")  
    ```  
  
-   드릴스루 보고서 매개 변수의 `Omit` 속성에 사용된 다음 식은 클릭한 셀이 `Product` 그룹에 있는 경우에만 대상 보고서에 매개 변수를 전달합니다.  
  
    ```  
    =Not(InScope("Product"))  
    ```  
  
 자세한 내용은 [집계 함수 참조&#40;보고서 작성기 및 SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) 및 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)를 참조하세요.  
  
## <a name="example"></a>예제  
 다음 코드 예에서는 항목의 현재 인스턴스가 `Product` 데이터 세트, 데이터 영역 또는 그룹 범위 내에 있는지 여부를 나타냅니다.  
  
```  
=InScope("Product")  
```  
  
## <a name="see-also"></a>참고 항목  
 [보고서에 사용되는 식&#40;보고서 작성기 및 SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [식의 데이터 형식&#40;보고서 작성기 및 SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
