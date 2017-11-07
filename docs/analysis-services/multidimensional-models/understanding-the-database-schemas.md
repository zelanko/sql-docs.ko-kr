---
title: "데이터베이스 스키마 이해 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Schema Generation Wizard, database schema
- database schema [Analysis Services]
- relational schema [Analysis Services], database schema
- subject area schema options [Analysis Services]
- staging area schema options [Analysis Services]
- denormalized schemas
ms.assetid: 51e411f9-ee3f-4b92-9833-c2bce8c6b752
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 12d62289fe08395c91eff39202b60ee0f67ff82a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="understanding-the-database-schemas"></a>데이터베이스 스키마 이해
  스키마 생성 마법사는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 차원 및 측정값 그룹을 기반으로 주제 영역 데이터베이스에 대한 비정규 관계형 스키마를 생성합니다. 마법사는 각 차원에 대해 차원 데이터를 저장할 관계형 테이블(차원 테이블)과 각 측정값 그룹에 대해 팩트 데이터를 저장할 관계형 테이블(팩트 테이블)을 생성합니다. 이러한 관계형 테이블을 생성할 때 연결된 차원, 연결된 측정값 및 서버 시간 차원은 무시합니다.  
  
## <a name="validation"></a>유효성 검사  
 스키마 생성 마법사는 기본 관계형 스키마를 생성하기 전에 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 큐브 및 차원의 유효성을 검사합니다. 오류를 발견하면 작업을 중지하고 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 태스크 목록 창에 오류를 보고합니다. 생성을 막는 오류의 예는 다음과 같습니다.  
  
-   키 특성이 두 개 이상인 차원  
  
-   키 특성과 다른 데이터 형식의 부모 특성  
  
-   측정값이 없는 측정값 그룹  
  
-   중복 제거 차원 또는 잘못 구성된 측정값  
  
-   잘못 구성된 서로게이트 키. **ScdOriginalID** 특성 유형을 사용하는 여러 개의 특성 또는 정수 데이터 형식을 통해 열에 바인딩되지 않은 **ScdOriginalID** 를 사용하는 특성이 여기에 해당됩니다.  
  
## <a name="dimension-tables"></a>차원 테이블  
 스키마 생성 마법사는 각 차원에 대해 주제 영역 데이터베이스에 포함할 차원 테이블을 생성합니다. 차원 테이블의 구조는 차원 테이블의 기반이 되는 차원을 디자인할 때 선택한 사항에 따라 달라집니다.  
  
 열  
 마법사는 차원 테이블의 기반이 되는 차원의 각 특성에 연결되는 바인딩(예: 각 특성의 **KeyColumns**, **NameColumn**, **ValueColumn**, **CustomRollupColumn**, **CustomRollupPropertiesColumn**및 **UnaryOperatorColumn** 속성에 대한 바인딩)에 대해 하나의 열을 생성합니다.  
  
 관계  
 마법사는 각 부모 특성에 대한 열과 차원 테이블의 기본 키 간에 관계를 생성합니다.  
  
 또한 큐브의 참조 차원으로 정의되는 각 추가 차원 테이블의 기본 키에 대한 관계를 생성합니다(해당되는 경우).  
  
 제약 조건  
 마법사는 기본적으로 차원의 키 특성을 기준으로 각 차원 테이블에 대해 기본 키 제약 조건을 생성합니다. 기본 키 제약 조건이 생성되면 기본적으로 별도의 이름 열이 생성됩니다. 데이터베이스에서 기본 키를 생성하지 않더라도 데이터 원본 뷰에는 논리적 기본 키가 생성됩니다.  
  
> [!NOTE]  
>  차원 테이블의 기반이 되는 차원에서 키 특성을 두 개 이상 지정하면 오류가 발생합니다.  
  
 번역  
 마법사는 번역 열이 필요한 특성에 대해 번역된 값을 보관할 별도의 테이블을 생성합니다. 또한 마법사는 필요한 각 언어에 대해 별도의 열을 만듭니다.  
  
## <a name="fact-tables"></a>팩트 테이블  
 스키마 생성 마법사는 큐브의 각 측정값 그룹에 대해 주제 영역 데이터베이스에 포함할 팩트 테이블을 생성합니다. 팩트 테이블의 구조는 팩트 테이블의 기반이 되는 측정값 그룹을 디자인할 때 선택한 사항 및 측정값 그룹과 포함된 차원 간에 설정된 관계에 따라 달라집니다.  
  
 열  
 마법사는 **Count** 집계 함수를 사용하는 측정값을 제외하고 각 측정값에 대해 하나의 열을 생성합니다. 이 함수를 사용하는 측정값에는 팩트 테이블에서 해당되는 열이 필요하지 않습니다.  
  
 또한 마법사는 측정값 그룹에 있는 각 일반 차원 관계의 세분성 특성 열 각각에 대해 열을 생성하고, 테이블의 기반이 되는 측정값 그룹에 대한 팩트 차원 관계가 있는 차원의 각 특성에 연결된 바인딩에 대해 하나 이상의 열을 생성합니다(해당되는 경우).  
  
 관계  
 마법사는 팩트 테이블의 각 일반 차원 관계에 대해 차원 테이블의 세분성 특성에 대한 관계를 생성합니다. 세분성이 차원 테이블의 키 특성을 기반으로 하는 경우에는 데이터베이스와 데이터 원본 뷰에서 관계가 생성됩니다. 세분성이 다른 특성을 기반으로 하는 경우에는 데이터 원본 뷰에서만 관계가 생성됩니다.  
  
 마법사에서 인덱스를 생성하도록 선택한 경우에는 이러한 각 관계 열에 대해 비클러스터형 인덱스가 생성됩니다.  
  
 제약 조건  
 팩트 테이블에서는 기본 키가 생성되지 않습니다.  
  
 참조 무결성을 강제 적용하는 경우에는 차원 테이블과 팩트 테이블 간에 참조 무결성 제약 조건이 생성됩니다(해당되는 경우).  
  
 번역  
 마법사는 측정값 그룹에서 번역 열이 필요한 속성에 대해 번역된 값을 보관할 별도의 테이블을 생성합니다. 또한 마법사는 필요한 각 언어에 대해 별도의 열을 만듭니다.  
  
## <a name="data-type-conversion-and-default-lengths"></a>데이터 형식 변환 및 기본 길이  
 스키마 생성 마법사는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **wchar** 데이터 형식을 사용하는 열을 제외하고 모든 경우에 데이터 형식을 무시합니다. **wchar** 데이터 크기는 **nvarchar** 데이터 형식으로 직접 변환됩니다. 그러나 **wchar** 크기를 사용하는 지정된 열의 길이가 4000바이트를 초과하면 스키마 생성 마법사에서 오류가 발생합니다.  
  
 특성에 대한 바인딩과 같은 데이터 항목에 대해 길이를 지정하지 않으면 해당 열에 다음 표의 기본 길이가 사용됩니다.  
  
|데이터 항목|기본 길이(바이트)|  
|---------------|------------------------------|  
|KeyColumn|50|  
|NameColumn|50|  
|CustomRollupColumn|3000|  
|CustomRollupPropertiesColumn|500|  
|UnaryOperatorColumn|1.|  
  
## <a name="see-also"></a>관련 항목:  
 [증분 생성 이해](../../analysis-services/multidimensional-models/understanding-incremental-generation.md)   
 [데이터 원본 뷰 및 데이터 원본에 대 한 변경 관리](../../analysis-services/multidimensional-models/manage-changes-to-data-source-views-and-data-sources.md)  
  
  

