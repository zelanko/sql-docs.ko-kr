---
title: 주제 영역 데이터베이스 스키마 옵션 (스키마 생성 마법사) (Analysis Services-다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.schemagenwizard.subjectareaschemaopts.f1
ms.assetid: 4c109bb8-e19d-412b-908f-bfdd7f872439
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2173255654b9ef02c269ec34bd21f93f8bf629a3
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66067981"
---
# <a name="subject-area-database-schema-options-schema-generation-wizard-analysis-services---multidimensional-data"></a>주제 영역 데이터베이스 스키마 옵션(스키마 생성 마법사)(Analysis Services - 다차원 데이터)
  **주제 영역 데이터베이스 스키마 옵션** 페이지를 사용하여 스키마 생성 방법을 제어하고 데이터 유지 방법을 정의할 수 있습니다.  
  
## <a name="options"></a>변수  
 **소유 스키마**  
 새 주제 영역 데이터베이스 내 스키마의 이름을 지정합니다.  
  
 **차원 테이블에 기본 키 만들기**  
 생성된 스키마의 차원 테이블에 기본 키를 만듭니다. 이 옵션을 선택하지 않으면 인덱스가 생성되지 않습니다.  
  
> [!NOTE]  
>  이 옵션을 선택하지 않으면 참조 무결성이 적용됩니다.  
  
 **인덱스 만들기**  
 생성된 스키마의 외래 키 열에 인덱스를 만듭니다.  
  
 **참조 무결성 적용**  
 생성된 스키마 내에 참조 무결성을 적용합니다. 이 옵션을 선택하지 않으면 관계가 생성되지만 적용되지는 않습니다.  
  
 **다시 생성 시 데이터 유지**  
 마법사가 완료될 때 주제 영역 데이터베이스에 데이터를 유지합니다. 이 옵션을 선택하지 않으면 주제 영역 데이터베이스의 모든 데이터가 경고 없이 지워질 수 있습니다.  
  
 **시간 테이블 채우기**  
 마법사에서 시간 테이블을 채우는 방법을 지정합니다. 다음 표에서는 이 옵션에 사용할 수 있는 값에 대해 설명합니다.  
  
> [!NOTE]  
>  이 옵션은 프로젝트 모드에서 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 를 사용하여 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 프로젝트에서 스키마 생성 마법사를 호출한 경우에만 사용할 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|채우기|주제 영역 시간 테이블을 채웁니다.|  
|채우지 않음|주제 영역 시간 테이블을 채우지 않습니다.|  
|비어 있는 경우에만 채우기|비어 있는 경우에만 주제 영역 시간 테이블을 채웁니다.|  
  
## <a name="see-also"></a>관련 항목  
 [스키마 생성 마법사 F1 도움말 &#40;Analysis Services-다차원 데이터&#41;](schema-generation-wizard-f1-help-analysis-services-multidimensional-data.md)  
  
  
