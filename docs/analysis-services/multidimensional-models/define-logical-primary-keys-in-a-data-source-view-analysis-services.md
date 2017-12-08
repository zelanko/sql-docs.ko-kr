---
title: "데이터 원본 뷰 (Analysis Services)에서 논리적 기본 키 정의 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- removing logical primary keys
- logical primary keys [SQL Server]
- deleting logical primary keys
- data source views [Analysis Services], logical primary keys
ms.assetid: 172bc267-c637-4caa-bf55-0ba198d30b1e
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c6ba2ab3a2fb37400a47b9d54981d48190f7f0e5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="define-logical-primary-keys-in-a-data-source-view-analysis-services"></a>데이터 원본 뷰에서 논리적 기본 키 정의(Analysis Services)
  데이터 원본 뷰 마법사와 데이터 원본 뷰 디자이너는 기본 데이터베이스 테이블을 기반으로 데이터 원본 뷰에 추가되는 테이블의 기본 키를 자동으로 정의합니다.  
  
 하지만 때로는 데이터 원본 뷰에서 수동으로 기본 키를 정의해야 할 수도 있습니다. 예를 들어 성능 또는 디자인상의 이유로 데이터 원본의 테이블이 기본 키 열을 명시적으로 정의하지 않았을 수 있습니다. 명명된 쿼리 및 뷰에서 테이블의 기본 키 열을 생략할 수도 있습니다. 테이블, 뷰 또는 명명된 쿼리에 물리적 기본 키가 정의되어 있지 않으면 데이터 원본 뷰 디자이너에서 테이블, 뷰 또는 명명된 쿼리에 대해 수동으로 논리적 기본 키를 정의할 수 있습니다.  
  
## <a name="set-a-logical-primary-key"></a>논리적 기본 키 설정  
 기본 키는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 테이블의 레코드를 고유하게 식별하고, 차원 테이블의 키 열을 식별하며, 테이블, 뷰 및 명명된 쿼리 간의 관계를 지원하는 데 필요합니다. 이러한 관계는 기본 데이터 원본에서 데이터 및 메타데이터를 검색할 쿼리를 작성하고 고급 비즈니스 인텔리전스 기능을 이용하는 데 사용됩니다.  
  
 명명된 계산을 포함하여 모든 열을 논리적 기본 키에 사용할 수 있습니다. 논리적 기본 키를 만들면 데이터 원본 뷰에서 UNIQUE 제약 조건이 생성되며 PRIMARY KEY 제약 조건으로 표시됩니다. 선택한 테이블에 지정된 기존의 다른 논리적 기본 키는 모두 삭제됩니다.  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 논리적 기본 키를 설정할 데이터 원본 뷰가 포함된 프로젝트를 열거나 데이터베이스에 연결합니다.  
  
2.  솔루션 탐색기에서 **데이터 원본 뷰** 폴더를 확장한 다음 해당 데이터 원본 뷰를 두 번 클릭합니다.  
  
     테이블이나 뷰를 찾으려면 **데이터 원본 뷰** 메뉴를 클릭하거나 **테이블**  또는 **다이어그램** 창의 열린 영역을 마우스 오른쪽 단추로 클릭하여 **테이블 찾기** 옵션을 사용합니다.  
  
3.  **테이블** 또는 **다이어그램** 창에서 논리적 기본 키를 정의하는 데 사용할 열을 마우스 오른쪽 단추로 클릭한 다음 **논리적 기본 키 설정**을 클릭합니다.  
  
     논리적 기본 키 설정을 위한 옵션은 기본 키가 없는 테이블에만 사용할 수 있습니다.  
  
     키를 설정하면 키 아이콘을 통해 기본 키 열이 식별됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [다차원 모델의 데이터 원본 뷰](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [데이터 원본 뷰에서 명명된 계산 정의&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)  
  
  
