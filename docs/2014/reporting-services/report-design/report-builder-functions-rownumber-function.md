---
title: RowNumber 함수(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 9d718ba8-d323-49fb-aac8-e7013a117b75
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: bb6025b8cf196d45fe0a6c9ac5cf0c19aa54013e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37276279"
---
# <a name="rownumber-function-report-builder-and-ssrs"></a>RowNumber 함수(보고서 작성기 및 SSRS)
  지정한 범위에서 행 개수의 실행 개수를 반환합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>구문  
  
```  
  
RowNumber(scope)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *범위*  
 (`String`) 데이터 집합, 데이터 영역 또는 그룹 또는 null의 이름 (`Nothing` 에서 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]), 행 개수를 계산할 컨텍스트를 지정 하는 합니다. `Nothing` 보고서 데이터 집합을 일반적으로 하는 가장 바깥쪽 컨텍스트를 지정합니다.  
  
## <a name="remarks"></a>Remarks  
 `RowNumber` 것 처럼 지정한 범위 내 행 개수의 실행 값 반환 [RunningValue](report-builder-functions-runningvalue-function.md) 집계 함수의 실행 값을 반환 합니다. 범위를 지정할 때 행 개수를 1로 다시 설정할 시점을 지정합니다.  
  
 *scope* 는 식이 될 수 없습니다. *scope* 는 포함하는 범위여야 합니다. 가장 바깥쪽에서 가장 안쪽 포함까지의 일반적인 범위는 보고서 데이터 집합, 데이터 영역, 행 그룹 또는 열 그룹입니다.  
  
 열에 걸쳐 값을 증가시키려면 열 그룹의 이름인 범위를 지정합니다. 행에 따라 수를 증가시키려면 행 그룹의 이름인 범위를 지정합니다.  
  
> [!NOTE]  
>  행 그룹과 열 그룹 모두를 지정하는 집계를 하나의 식에 포함하는 것은 지원되지 않습니다.  
  
 자세한 내용은 [집계 함수 참조&#40;보고서 작성기 및 SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) 및 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)를 참조하세요.  
  
## <a name="code-example"></a>코드 예  
 다음은 식에 사용할 수 있는 여 `BackgroundColor` 항상 흰색으로 시작 하는 각 그룹에 대 한 세부 정보 행 색을 대체 하는 테이블 릭 스 데이터 영역 정보 행의 속성입니다.  
  
```  
=IIF(RowNumber("GroupbyCategory") Mod 2, "White", "PaleGreen")  
```  
  
## <a name="see-also"></a>관련 항목  
 [보고서에 사용 되는 식 &#40;보고서 작성기 및 SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [식의 데이터 형식&#40;보고서 작성기 및 SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [합계, 집계 및 기본 제공 컬렉션의 식 범위 &#40;보고서 작성기 및 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
