---
title: 제한 행 (파티션 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.partitionwizard.typefilterexpression.f1
ms.assetid: eec8da8f-eab4-4ac4-a81d-995c814f88ca
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2b86cfeedd76af51b5f9d8cc4633c73ed9cc17ea
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62748235"
---
# <a name="restrict-rows-partition-wizard"></a>행 제한(파티션 마법사)
  **행 제한** 페이지를 사용하여 지정한 테이블에서 검색한 다음 집계하여 파티션에 포함시킬 행을 제한할 수 있습니다.  
  
> [!NOTE]  
>  이 페이지는 **원본 정보 지정** 페이지에서 단일 테이블을 선택한 경우에만 나타납니다.  
  
> [!CAUTION]  
>  **원본 정보 지정** 페이지의 **사용 가능한 테이블** 에서 다른 파티션이 사용하는 테이블을 지정한 경우 **행 제한** 페이지에서 쿼리를 제공하지 않으면 큐브에서 데이터가 중복될 수 있습니다.  
  
## <a name="options"></a>변수  
 **행을 제한 하는 쿼리를 지정 합니다.**  
 행을 제한하는 쿼리를 **쿼리** 입력란에 입력하려면 선택합니다.  
  
 이 옵션을 선택할 때 **WHERE 절 제공** 이 비어 있으면 이전에 선택한 테이블에서 모든 열과 모든 행을 검색하는 SQL 문으로 해당 옵션이 채워집니다.  
  
 **데이터 집합 속성**  
 파티션 처리 시 테이블에서 행을 검색할 때 사용되는 SQL 문을 입력하거나 수정합니다.  
  
> [!IMPORTANT]  
>  WHERE 절을 지정하여 레코드 하위 집합을 이 파티션에 사용할 수 있습니다. 이것은 여러 개의 파티션이 단일 팩트 테이블을 기반으로 하는 경우 데이터 복제를 방지하기 위해 반드시 필요합니다.  
  
 **확인**  
 **쿼리** 의 문이 유효한 SQL 문인지 확인합니다.  
  
## <a name="see-also"></a>관련 항목  
 [파티션 & #40; Analysis Services-다차원 데이터 & #41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)  
  
  
