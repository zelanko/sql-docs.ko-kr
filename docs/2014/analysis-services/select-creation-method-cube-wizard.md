---
title: 생성 방법 선택 (큐브 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubewizard.cubedefinition.f1
ms.assetid: 985d3b5b-7891-465b-862d-f7e75431b342
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 793c83dba01be84fb468b0be54bb7d0405e39467
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66069627"
---
# <a name="select-creation-method-cube-wizard"></a>생성 방법 선택(큐브 마법사)
  **생성 방법 선택** 페이지를 사용하여 큐브를 만드는 방법을 지정할 수 있습니다.  
  
## <a name="options"></a>변수  
 **기존 테이블 사용**  
 데이터 원본에 있는 기존 테이블을 사용하여 큐브를 만들려면 선택합니다. 마법사가 새 큐브를 만들기 위해 기존 테이블을 기반으로 측정값 그룹과 차원을 선택하고 정의하는 과정을 안내합니다.  
  
 **빈 큐브 만들기**  
 빈 큐브를 만들려면 선택합니다. 이 옵션은 모든 항목을 직접 만들려고 하거나 큐브에 있는 모든 측정값 그룹이 연결된 측정값 그룹인 경우에 유용합니다.  
  
> [!NOTE]  
>  이 옵션은 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 프로젝트를 사용하여 작업하는 경우에만 사용할 수 있고 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스에 직접 연결하는 경우에는 사용할 수 없습니다.  
  
 **데이터 원본에 테이블 생성**  
 큐브를 먼저 만든 다음 큐브 정의를 기반으로 데이터 원본에서 새 테이블을 생성하려면 선택합니다.  
  
> [!NOTE]  
>  이 옵션을 사용하려면 기본 데이터 원본에 개체를 만들 수 있는 권한이 있어야 합니다.  
  
 이 옵션을 선택하면 **템플릿** 옵션을 사용할 수 있습니다.  
  
 **템플릿**  
 큐브를 만드는 데 사용할 템플릿을 선택합니다. 템플릿은 특정 비즈니스 용도를 위한 정의 집합을 제공합니다.  
  
> [!NOTE]  
>  이 옵션은 **데이터 원본에 테이블 생성** 옵션을 선택한 경우에만 사용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [큐브 개체 &#40;Analysis Services-다차원 데이터&#41;](multidimensional-models-olap-logical-cube-objects/cube-objects-analysis-services-multidimensional-data.md)   
 [다차원 모델의 큐브](multidimensional-models/cubes-in-multidimensional-models.md)   
 [다차원 모델의 차원](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
