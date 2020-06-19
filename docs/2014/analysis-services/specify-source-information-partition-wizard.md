---
title: 원본 정보 지정 (파티션 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.partitionwizard.specifydsvandfacttables.f1
ms.assetid: b6c13587-c690-45d9-af90-b3d652afc55b
author: minewiskan
ms.author: owend
ms.openlocfilehash: a597d1f8f3b5720f2f7a688fdf2aabc7941a0ce1
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940304"
---
# <a name="specify-source-information-partition-wizard"></a>원본 정보 지정(파티션 마법사)
  **원본 정보 지정** 페이지를 사용하여 파티션이 생성될 측정값 그룹과 파티션에 대한 데이터 원본 뷰를 선택할 수 있을 뿐만 아니라 파티션에 대한 테이블을 필터링할 수 있습니다.  
  
> [!CAUTION]  
>  **사용 가능한 테이블** 에서 다른 파티션에서 사용하는 테이블을 지정하는 경우 **행 제한** 페이지에서 쿼리를 제공하지 않으면 큐브의 데이터가 중복될 수 있습니다.  
  
## <a name="options"></a>옵션  
 **측정값 그룹**  
 이 파티션에 대한 측정값 그룹을 선택합니다.  
  
 **찾는 위치**  
 이 파티션의 원본 테이블이 들어 있는 데이터 원본 또는 데이터 원본 뷰를 선택합니다. 기본적으로 측정값 그룹에서 사용하는 데이터 원본 뷰가 선택됩니다.  
  
 **테이블 필터**  
 **사용 가능한 테이블**에 표시되는 테이블의 이름을 제한하는 데 사용할 문자열을 입력합니다.  
  
 **테이블 찾기**  
 **사용 가능한 테이블**의 테이블 목록을 새로 고치고 **테이블 필터**에 문자열이 지정된 경우 목록을 추가로 제한하려면 선택합니다.  
  
 **사용 가능한 테이블**  
 파티션의 원본 테이블로 사용할 테이블을 선택합니다. **파티션 마법사** 는 **사용 가능한 테이블**에서 선택한 각 테이블에 대해 하나의 파티션을 만듭니다.  
  
 **테이블 필터**에서 필터를 지정하지 않으면 이 옵션은 **찾는 위치** 에서 지정한 것 중 **측정값 그룹**에서 지정한 측정값 그룹이 사용하는 팩트 테이블과 구조가 비슷한 데이터 원본 또는 데이터 원본 뷰의 모든 테이블을 나열합니다.  
  
 **테이블 필터**에서 필터를 지정하면 이전 조건을 만족하는 테이블 이름과 이 필터를 비교하여 목록을 보다 엄격하게 제한합니다. **테이블 필터** 에 지정한 문자열을 포함하고 있는 테이블만 표시됩니다.  
  
> [!NOTE]  
>  테이블을 두 개 이상 선택하면 **행 제한** 페이지가 표시되지 않고 선택한 테이블에서 생성된 파티션에 대해 행을 제한할 수 없습니다. 각 파티션에 대한 행을 제한하려면 파티션이 생성될 각 테이블마다 파티션 마법사를 한 번씩 실행합니다.  
  
## <a name="see-also"></a>참고 항목  
 [파티션&#40;Analysis Services - 다차원 데이터&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)  
  
  
