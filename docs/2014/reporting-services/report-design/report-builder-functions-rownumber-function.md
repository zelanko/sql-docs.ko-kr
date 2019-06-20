---
title: RowNumber 함수(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 9d718ba8-d323-49fb-aac8-e7013a117b75
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d4a06a24525b3d9d0c4e4a5f3f0b749a7db70261
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66105164"
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
 (`String`) 행 개수를 계산할 컨텍스트를 지정하는 데이터 집합, 데이터 영역, 그룹의 이름 또는 Null([!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]의 `Nothing`)입니다. `Nothing`은 가장 바깥쪽 컨텍스트를 지정하며 이는 일반적으로 보고서 데이터 집합입니다.  
  
## <a name="remarks"></a>Remarks  
 `RowNumber` 것 처럼 지정한 범위 내 행 개수의 실행 값 반환 [RunningValue](report-builder-functions-runningvalue-function.md) 집계 함수의 실행 값을 반환 합니다. 범위를 지정할 때 행 개수를 1로 다시 설정할 시점을 지정합니다.  
  
 *scope* 는 식이 될 수 없습니다. *scope* 는 포함하는 범위여야 합니다. 가장 바깥쪽에서 가장 안쪽 포함까지의 일반적인 범위는 보고서 데이터 세트, 데이터 영역, 행 그룹 또는 열 그룹입니다.  
  
 열에 걸쳐 값을 증가시키려면 열 그룹의 이름인 범위를 지정합니다. 행에 따라 수를 증가시키려면 행 그룹의 이름인 범위를 지정합니다.  
  
> [!NOTE]  
>  행 그룹과 열 그룹 모두를 지정하는 집계를 하나의 식에 포함하는 것은 지원되지 않습니다.  
  
 자세한 내용은 [집계 함수 참조&#40;보고서 작성기 및 SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) 및 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)를 참조하세요.  
  
## <a name="code-example"></a>코드 예  
 다음은 항상 흰색으로 시작되는 각 그룹의 정보 행 색을 대체하기 위해 테이블릭스 데이터 영역 정보 행의 `BackgroundColor` 속성에 사용할 수 있는 식입니다.  
  
```  
=IIF(RowNumber("GroupbyCategory") Mod 2, "White", "PaleGreen")  
```  
  
## <a name="see-also"></a>관련 항목  
 [보고서에 사용되는 식&#40;보고서 작성기 및 SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [식의 데이터 형식&#40;보고서 작성기 및 SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
