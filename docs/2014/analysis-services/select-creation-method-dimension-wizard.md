---
title: 생성 방법 선택 (차원 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.dimensionwizard.dimensiondefinition.f1
ms.assetid: 291b0b2d-a03a-4df6-82f7-90ad92d4d1cf
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 10d52966956d39f7a495e353bdf6acd595cc51ab
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36092760"
---
# <a name="select-creation-method-dimension-wizard"></a>생성 방법 선택(차원 마법사)
  **생성 방법 선택** 페이지를 사용하여 차원 생성 방법을 선택할 수 있습니다.  
  
 **차원 마법사를 열려면**  
  
-   [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]의 **솔루션 탐색기**에서 **프로젝트의** 차원 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 폴더를 마우스 오른쪽 단추로 클릭한 다음 **새 차원**을 클릭합니다.  
  
## <a name="options"></a>변수  
 **기존 테이블 사용**  
 데이터 원본에 여러 테이블의 차원을 생성합니다. 차원에 사용할 수 있는 특성은 테이블의 데이터 구조에 따라 달라집니다.  
  
 자세한 내용은 [기존 테이블을 사용하여 차원 만들기](multidimensional-models/create-a-dimension-by-using-an-existing-table.md)를 참조하세요.  
  
 **데이터 원본에 시간 테이블 생성**  
 기본 데이터 원본에 시간 테이블을 만든 다음 이 테이블을 사용하여 시간 차원을 만듭니다. 이 옵션은 시간 테이블이 없는데 스크립트를 사용하여 시간 테이블을 만들고 싶지 않은 경우에 사용합니다. 새 시간 테이블은 마법사에서 지정한 데이터 범위, 특성 및 달력에 대한 데이터를 포함합니다.  
  
> [!NOTE]  
>  이 옵션을 사용하려면 기본 데이터 원본에 개체를 만들 수 있는 권한이 있어야 합니다. 데이터 원본에 개체를 만들 수 있는 권한이 없는 경우 **서버에 시간 테이블 생성** 옵션을 대신 사용합니다.  
  
 자세한 내용은 [시간 테이블을 생성하여 시간 차원 만들기](multidimensional-models/create-a-time-dimension-by-generating-a-time-table.md)를 참조하세요.  
  
 **서버에 시간 테이블 생성**  
 서버에 직접 시간 테이블을 만든 다음 이 테이블을 사용하여 시간 차원을 만듭니다. 이 옵션은 기본 데이터 원본에 개체를 만들 수 있는 권한이 없는 경우에 사용합니다. 새 시간 차원은 마법사에서 지정한 데이터 범위, 특성 및 달력에 대한 데이터를 포함합니다.  
  
 자세한 내용은 [시간 테이블을 생성하여 시간 차원 만들기](multidimensional-models/create-a-time-dimension-by-generating-a-time-table.md)를 참조하세요.  
  
 **데이터 원본에 시간이 아닌 테이블 생성**  
 기본 관계형 데이터 원본을 사용하지 않고 차원을 디자인한 다음 데이터 원본에 필요한 스키마를 생성합니다. 이 방법을 하향식 모델링이라고 합니다.  
  
> [!NOTE]  
>  이 옵션을 사용하려면 기본 데이터 원본에 개체를 만들 수 있는 권한이 있어야 합니다.  
  
 차원을 작성할 때 템플릿을 사용하거나 사용하지 않을 수 있습니다. 템플릿을 사용하여 차원을 작성하려면 **템플릿** 목록에서 템플릿을 선택합니다.  
  
 자세한 내용은 [데이터 원본에 시간이 아닌 테이블을 생성하여 차원 만들기](multidimensional-models/create-a-dimension-by-generating-a-non-time-table-in-the-data-source.md)를 참조하세요.  
  
 **템플릿**  
 차원을 생성하는 데 사용할 템플릿을 선택합니다. 템플릿은 특정 비즈니스 용도를 위한 전체 특성 집합과 계층 정의를 제공합니다.  
  
> [!NOTE]  
>  이 옵션은 **데이터 원본에 시간이 아닌 테이블 생성** 옵션을 선택한 경우에만 사용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [차원 마법사 F1 도움말](dimension-wizard-f1-help.md)   
 [차원 &#40;Analysis Services-다차원 데이터&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [다차원 모델의 차원](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  