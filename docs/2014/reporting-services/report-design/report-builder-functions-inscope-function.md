---
title: InScope 함수(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a8cd209a-e5d3-4dce-ab2d-f271f6c54955
caps.latest.revision: 7
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: e677c9e02f452a486b9168f15c662362640ea86e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36182501"
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
 `InScope` 지정 하는 범위에 멤버 자격에 대 한 보고서 항목의 현재 인스턴스 범위를 테스트 하는 함수는 *범위*매개 변수입니다.  
  
 *Scope* 는 식이 될 수 없습니다.  
  
 일반적인 용도 `InScope` 함수는 동적으로 범위가 되는 데이터 영역에 범위를 지정 합니다. 예를 들어 `InScope` 이름과 다른 매개 변수 집합을 클릭 한 셀에 따라 다양 한 보고서를 제공할 하는 데이터 영역 셀의 드릴스루 링크에 사용할 수 있습니다. 이러한 예는 다음과 같습니다.  
  
-   드릴스루 링크의 보고서 이름으로 사용된 다음 식은 클릭한 셀이 `ProductDetail` 그룹에 있으면 `Month` 보고서를 열고 그렇지 않으면 `ProductSummary` 보고서를 엽니다.  
  
    ```  
    =Iif(InScope("Month"), "ProductDetail", "ProductSummary")  
    ```  
  
-   사용 된 다음 식의 `Omit` 드릴스루 보고서 매개 변수의 속성은 매개 변수를 전달 대상 보고서를 클릭 한 셀에 있을 경우에는 `Product` 그룹입니다.  
  
    ```  
    =Not(InScope("Product"))  
    ```  
  
 자세한 내용은 [집계 함수 참조&#40;보고서 작성기 및 SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) 및 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)를 참조하세요.  
  
## <a name="example"></a>예제  
 다음 코드 예에서는 항목의 현재 인스턴스가 `Product` 데이터 집합, 데이터 영역 또는 그룹 범위 내에 있는지 여부를 나타냅니다.  
  
```  
=InScope("Product")  
```  
  
## <a name="see-also"></a>관련 항목  
 [식은 보고서에서 사용 하 여 &#40;보고서 작성기 및 SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [식의 데이터 형식&#40;보고서 작성기 및 SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [합계, 집계 및 기본 제공 컬렉션의 식 범위 &#40;보고서 작성기 및 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  