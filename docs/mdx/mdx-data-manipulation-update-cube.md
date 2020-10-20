---
description: MDX 데이터 조작 - UPDATE CUBE
title: UPDATE CUBE 문 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e4ee6d69057745486ed72f00721f9ab38833ca2e
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196978"
---
# <a name="mdx-data-manipulation---update-cube"></a>MDX 데이터 조작 - UPDATE CUBE


  UPDATE CUBE 문은 SUM 집계를 사용하여 부모에 집계하는 큐브의 셀에 데이터를 쓰기 저장하는 데 사용됩니다. 자세한 설명 및 예제를 보려면이 블로그 게시물: [Analysis Services 사용 하 여 쓰기 저장 응용 프로그램 빌드 (블로그)](/archive/blogs/data_otaku/building-a-writeback-application-with-analysis-services)의 "할당 이해"를 참조 하세요.  
  
## <a name="syntax"></a>구문  
  
```  
  
UPDATE [ CUBE ] Cube_Name   
   SET   
            <update clause>   
           [, <update clause> ...n ]  
  
<update clause> ::=   
      Tuple_Expression[.VALUE]= New_Value  
      [   
        USE_EQUAL_ALLOCATION   
        | USE_EQUAL_INCREMENT   
        | USE_WEIGHTED_ALLOCATION [ BY Weight_Expression]   
        | USE_WEIGHTED_INCREMENT [ BY Weight_Expression]  
      ]  
```  
  
## <a name="arguments"></a>인수  
 *Cube_Name*  
 큐브의 이름을 지정하는 유효한 문자열입니다.  
  
 *Tuple_Expression*  
 튜플을 반환하는 유효한 MDX 식입니다.  
  
 *New_Value*  
 유효한 숫자 식입니다.  
  
 *Weight_Expression*  
 0에서 1 사이의 10진수 값을 반환하는 유효한 MDX 숫자 식입니다.  
  
## <a name="remarks"></a>설명  
 큐브의 지정된 리프 또는 리프가 아닌 셀의 값을 업데이트할 수 있습니다. 지정된 리프가 아닌 셀 값을 종속되는 여러 리프 셀에 할당할 수도 있습니다. 튜플 식으로 지정되는 셀은 다차원 공간의 유효한 셀일 수 있으며, 리프 셀일 필요가 없습니다. 그러나 셀은 [Sum](../mdx/sum-mdx.md) 집계 함수를 사용 하 여 집계 되어야 하며 셀을 식별 하는 데 사용 되는 튜플에 계산 멤버를 포함 해서는 안 됩니다.  
  
 **UPDATE CUBE** 문은 지정 된 합계로 롤업되는 리프 및 리프가 아닌 셀에 일련의 개별 셀 쓰기 저장 (writeback) 작업을 자동으로 생성 하는 서브루틴으로 생각 하면 도움이 될 수 있습니다.  
  
 다음은 할당 방법에 대 한 설명입니다.  
  
 **USE_EQUAL_ALLOCATION:** 업데이트 된 셀에 영향을 주는 모든 리프 셀에는 다음 식에 따라 동일한 값이 할당 됩니다.  
  
```  
<leaf cell value> =   
<New Value> / Count(leaf cells that are contained in <tuple>)  
```  
  
 **USE_EQUAL_INCREMENT:** 업데이트 된 셀에 영향을 주는 모든 리프 셀은 다음 식에 따라 변경 됩니다.  
  
```  
<leaf cell value> = <leaf cell value> +   
(<New Value > - <existing value>) /  
Count(leaf cells contained in <tuple>)  
```  
  
 **USE_WEIGHTED_ALLOCATION:** 업데이트 된 셀에 영향을 주는 모든 리프 셀에는 다음 식을 기반으로 하는 동일한 값이 할당 됩니다.  
  
```  
<leaf cell value> = < New Value> * Weight_Expression  
```  
  
 **USE_WEIGHTED_INCREMENT:** 업데이트 된 셀에 영향을 주는 모든 리프 셀은 다음 식에 따라 변경 됩니다.  
  
```  
<leaf cell value> = <leaf cell value> +   
(<New Value> - <existing value>)  * Weight_Expression  
```  
  
 가중치 식이 지정 되지 않은 경우 **UPDATE CUBE** 문은 암시적으로 다음 식을 사용 합니다.  
  
```  
Weight_Expression = <leaf cell value> / <existing value>  
```  
  
 가중치 식은 영(0)과 1 사이의 10진수 값으로 표현해야 합니다. 이 값은 할당의 영향을 받는 리프 셀에 할당하려는 할당 값의 비율을 지정합니다. 클라이언트 애플리케이션 프로그래머는 해당 롤업 집계 값이 식의 할당된 값과 동일하도록 식을 만들어야 합니다.  
  
> [!CAUTION]  
>  클라이언트 애플리케이션에서는 잘못된 롤업 값이나 일관적이지 않은 데이터 등의 발생 가능한 예기치 않은 결과를 방지하기 위해 모든 차원에 대한 할당을 동시에 고려해야 합니다.  
  
 각 **업데이트 큐브** 할당은 트랜잭션 용도로 원자성으로 간주 되어야 합니다. 즉, 식이나 보안 위배 오류 등의 어떤 이유로 인해 할당 작업 중 하나라도 실패하면 전체 UPDATE CUBE 작업이 실패합니다. 개별 할당 작업의 계산을 처리하기 전에 데이터의 스냅샷을 사용하여 결과 계산이 올바른지 확인해야 합니다.  
  
> [!CAUTION]  
>  정수가 포함된 측정값에서 사용되는 경우 USE_WEIGHTED_ALLOCATION 메서드는 증분적인 반올림 변화로 인한 부정확한 결과를 반환할 수 있습니다.  
  
> [!IMPORTANT]  
>  업데이트된 셀이 겹치지 않을 경우 **Update Isolation Level** 연결 문자열 속성을 사용하여 UPDATE CUBE의 성능을 향상시킬 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>   
 [Mdx 데이터 조작 문은 MDX를 &#40;&#41;](../mdx/mdx-data-manipulation-statements-mdx.md)  
  
