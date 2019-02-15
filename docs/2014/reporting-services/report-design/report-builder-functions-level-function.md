---
title: Level 함수(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 41235402-bb9e-4cb7-b91e-431e77db19cf
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: a0eab4c54be4f849a735b7da4de54a9b85cb78f3
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56285311"
---
# <a name="level-function-report-builder-and-ssrs"></a>Level 함수(보고서 작성기 및 SSRS)
  재귀 계층의 현재 수준을 반환합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>구문  
  
```  
  
Level(scope)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *범위*  
 (`String`) 선택 사항입니다. 집계 함수를 적용할 보고서 항목을 포함하는 데이터 세트, 그룹 또는 데이터 영역의 이름입니다. *scope* 를 지정하지 않은 경우 현재 범위가 사용됩니다.  
  
## <a name="return-type"></a>반환 형식  
 `Integer`를 반환합니다. 하는 경우 *범위* 데이터 집합 또는 데이터 영역을 지정 하거나 비재귀 그룹화 (없는 그룹화, 즉 `Parent` 요소), `Level` 0을 반환 합니다. *scope* 를 생략하면 현재 범위의 수준이 반환됩니다.  
  
## <a name="remarks"></a>Remarks  
 `Level` 함수에서 반환되는 값은 0에서 시작합니다. 즉, 계층의 첫 수준은 0입니다.  
  
 `Level` 함수는 직원 목록과 같은 재귀 계층에서 들여쓰기를 제공하는 데 사용할 수 있습니다.  
  
 재귀 계층 구조에 대한 자세한 내용은 [재귀 계층 구조 그룹 만들기&#40;보고서 작성기 및 SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="example"></a>예제  
 다음 코드 예에서는 Employees 그룹에서 행 수준을 제공합니다.  
  
```  
=Level("Employees")  
```  
  
## <a name="see-also"></a>관련 항목  
 [보고서에 사용되는 식&#40;보고서 작성기 및 SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [식의 데이터 형식&#40;보고서 작성기 및 SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
