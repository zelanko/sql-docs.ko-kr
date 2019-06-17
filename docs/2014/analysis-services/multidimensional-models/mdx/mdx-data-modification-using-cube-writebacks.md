---
title: 큐브 쓰기 저장 (MDX)를 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- writeback [Analysis Services], cubes
- cubes [Analysis Services], modifying
- modifying cubes
- UPDATE CUBE statement
- cubes [Analysis Services], writeback
ms.assetid: ae2385fc-7fa0-4f8e-98d7-dcb0a5f0eeea
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a79e98375c27c6a3570b2fafcf424965d7a97c8d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66074223"
---
# <a name="using-cube-writebacks-mdx"></a>큐브 쓰기 저장(Writeback) 사용(MDX)
  큐브를 업데이트하는 데는 [UPDATE CUBE](/sql/mdx/mdx-data-manipulation-update-cube) 문을 사용합니다. 이 문은 특정 값을 가진 튜플을 업데이트할 수 있도록 해줍니다. 큐브 업데이트에 UPDATE CUBE 문을 효과적으로 사용하기 위해서는 문의 구문, 발생할 수 있는 오류 조건 및 업데이트로 인한 큐브의 영향을 이해해야 합니다.  
  
## <a name="update-cube-statement-syntax"></a>UPDATE CUBE 문 구문  
 다음은 UPDATE CUBE 문의 구문입니다.  
  
```  
UPDATE [CUBE] <Cube_Name> SET <tuple>.VALUE = <value> [,<tuple>.VALUE = <value>...]  
 [ USE_EQUAL_ALLOCATION | USE_EQUAL_INCREMENT |  
  USE_WEIGHTED_ALLOCATION [BY <weight value_expression>] |  
  USE_WEIGHTED_INCREMENT [BY <weight value_expression>] ]   
```  
  
 튜플의 전체 좌표 집합을 지정하지 않으면 지정되지 않은 좌표에 계층의 기본 멤버가 사용됩니다. 확인된 튜플은 [Sum](/sql/mdx/sum-mdx) 함수를 사용하여 집계한 셀을 참조해야 하며 셀 좌표 중 하나로 계산 멤버를 사용해선 안 됩니다.  
  
 UPDATE CUBE 문은 원자 셀에 일련의 개별 쓰기 저장 작업을 생성하는 서브루틴으로 볼 수 있습니다. 이 쓰기 저장 작업은 모두 지정된 합계로 롤업됩니다.  
  
> [!NOTE]  
>  업데이트된 셀이 겹치지 않을 경우 `Update Isolation Level` 연결 문자열 속성을 사용하여 UPDATE CUBE의 성능을 향상시킬 수 있습니다. 자세한 내용은 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>을 참조하세요.  
  
## <a name="example"></a>예제  
 Adventure Works 큐브에서 Sales Targets 측정값 그룹을 사용하여 UPDATE CUBE를 테스트할 수 있습니다. 이 측정값 그룹은 SUM으로 집계된 측정값으로 구성되며 UPDATE CUBE의 필수 구성 요소입니다.  
  
1.  Adventure Works 데이터베이스에서 Sales Targets 측정값 그룹에 쓰기 저장을 사용합니다. Management Studio에서 측정값 그룹을 마우스 오른쪽 단추로 클릭하고 **쓰기 저장 옵션**을 가리킨 후 **쓰기 저장 사용**을 선택합니다.  
  
     Writeback 폴더에 새로운 쓰기 저장 테이블이 표시되어야 합니다. 테이블 이름은 WriteTable_Fact Sales Quota입니다.  
  
2.  MDX 쿼리 창을 엽니다. 원래 값을 보려면 다음 select 문을 실행합니다.  
  
    ```  
    SELECT [Measures].[Sales Amount Quota] on 0 ,  
    [Employee].[Employee Department].[Title].&[Sales Representative].children on 1  
    FROM [Adventure Works]  
  
    ```  
  
     각 담당자의 판매 할당액이 표시되어야 합니다.  
  
3.  새 값을 쓰기 저장하려면 update cube 문을 실행합니다. 이 예에서는 판매 할당액을 0으로 설정합니다. 새 값이 0이므로 할당 방법을 지정하지 마십시오.  
  
    ```  
    UPDATE CUBE [Adventure Works]   
    SET ([Measures].[Sales Amount Quota], [Employee].[Employee Department].[Department].&[Sales]) = 0  
  
    ```  
  
4.  SELECT 문을 다시 실행합니다. 이제 할당액에 0이 표시되어야 합니다.  
  
 쓰기 저장 값이 현재 세션으로 제한됩니다. 사용자와 세션 간에 값을 유지하려면 쓰기 저장 테이블을 처리하십시오. Management Studio에서 WriteTable_Fact Sales Quota를 마우스 오른쪽 단추로 클릭하고 **처리**를 선택합니다.  
  
 할당 방법을 지정하려면 새 값이 0보다 커야 합니다. 이 예에서 Sales Amount Quota의 새 값은 200만이고 할당 방법을 통해 모든 판매 담당자 간에 할당량이 배포됩니다.  
  
```  
UPDATE CUBE [Adventure Works]   
SET ([Measures].[Sales Amount Quota], [Employee].[Employee Department].[Department].&[Sales]) = 2000000   
USE_EQUAL_ALLOCATION  
```  
  
## <a name="error-conditions"></a>오류 조건  
 다음 표에서는 쓰기 저장 실패를 유발하는 원인과 해당 오류의 결과를 설명합니다.  
  
|오류 조건|결과|  
|---------------------|------------|  
|업데이트가 함께 존재할 수 없는 동일한 차원의 멤버를 포함합니다.|업데이트가 실패합니다. 참조된 셀이 큐브 공간에 포함되지 않습니다.|  
|업데이트가 부호 없는 형식의 측정값을 원본으로 하는 측정값을 포함합니다.|업데이트가 실패합니다. 증가분은 음수 값을 사용할 수 있는 측정값이 필요합니다.|  
|업데이트가 sum 이외의 집계를 수행하는 측정값을 포함합니다.|오류가 발생합니다.|  
|하위 큐브에서 업데이트를 시도했습니다.|오류가 발생합니다.|  
  
## <a name="affect-of-cube-changes"></a>큐브 변경의 영향  
 다음 변경 사항은 쓰기 저장(writeback)에 영향을 주지 않습니다.  
  
-   큐브, 큐브의 측정값 그룹 또는 큐브의 차원에 대한 처리  
  
-   임의의 차원에 속성 추가  
  
-   새 차원 추가  
  
-   쓰기 저장(writeback)을 포함하지 않는 차원 삭제  
  
-   계층 추가, 수정 또는 제거  
  
-   새 측정값 추가  
  
 다음 변경은 쓰기 저장(writeback) 데이터를 제거하기 전에는 수행할 수 없습니다.  
  
-   쓰기 저장(writeback)가 속성을 포함할 때 속성 또는 속성 계층 삭제. 여기에는 속성 또는 속성 계층의 명시적 제거 또는 속성의 부모 차원 제거도 포함됩니다.  
  
-   쓰기 저장(writeback)에 포함된 측정값 삭제  
  
-   쓰기 저장(writeback)에 포함된 차원에 `(All)` 수준 없이 속성 추가  
  
-   쓰기 저장(writeback)에 포함된 차원의 차원 세분성 변경  
  
## <a name="see-also"></a>관련 항목  
 [데이터 수정&#40;MDX&#41;](mdx-data-modification-modifying-data.md)  
  
  
