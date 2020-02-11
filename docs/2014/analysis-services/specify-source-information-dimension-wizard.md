---
title: 원본 정보 지정 (차원 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensionwizard.dimensionmaintable.f1
ms.assetid: 0538b490-5185-49e1-a783-4ce3539a0de5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 30234275a724dddce95cdad66e5e37a382a25e62
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66068175"
---
# <a name="specify-source-information-dimension-wizard"></a>원본 정보 지정(차원 마법사)
  
  **주 차원 테이블 선택** 페이지를 사용하여 생성될 차원의 데이터 원본 뷰, 주 차원 테이블, 키 열 및 멤버 이름 열을 선택할 수 있습니다.  
  
 **차원 마법사를 열려면**  
  
-   
  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]의 **솔루션 탐색기**에서 **프로젝트의** 차원 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 폴더를 마우스 오른쪽 단추로 클릭한 다음 **새 차원**을 클릭합니다.  
  
## <a name="options"></a>옵션  
 **데이터 원본 뷰**  
 데이터 원본 뷰를 선택합니다.  
  
 **주 테이블**  
 선택한 데이터 원본 뷰에서 차원의 주 테이블로 사용할 테이블을 선택합니다.  
  
 **키 열**  
 
  **주 테이블** 에 지정된 테이블에서 차원의 키 특성에 대한 키 열을 선택합니다.  
  
> [!NOTE]  
>  둘 이상의 열을 선택할 수 있습니다. 테이블에 복합 기본 키가 있으면 복합 기본 키에 포함된 열을 모두 선택하십시오. 키 열의 순서는 중요합니다.  
  
 **이름 열**  
 
  **주 테이블** 에 지정된 테이블에서 차원의 멤버 이름을 제공하는 열을 선택합니다. 복합 키를 사용하는 경우 이름 열을 지정해야 합니다. 복합 키에 대한 이름 열을 만들려면 데이터 원본 뷰에 지정된 키 열을 연결하는 명명된 계산을 만드는 것이 좋습니다. 단일 키를 사용하는 경우 이름 열은 선택 사항입니다.  
  
## <a name="see-also"></a>참고 항목  
 [차원 마법사 F1 도움말](dimension-wizard-f1-help.md)   
 [차원 &#40;Analysis Services 다차원 데이터&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [다차원 모델의 차원](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
