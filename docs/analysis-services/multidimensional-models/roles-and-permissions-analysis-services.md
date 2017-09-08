---
title: "역할 및 사용 권한 (Analysis Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
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
- security [Analysis Services], about security
- security [Analysis Services - multidimensional data], about security
ms.assetid: bb885447-868b-4686-853c-8241f63d4370
caps.latest.revision: 21
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2981ab6e8c529fa24fc2256c93dc903dc58857d7
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="roles-and-permissions-analysis-services"></a>역할 및 권한(Analysis Services)
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 작업, 개체 및 데이터에 대한 액세스 권한을 부여하는 역할 기준 권한 부여 모델을 제공합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스 또는 데이터베이스에 액세스하는 모든 사용자는 역할 컨텍스트 내에서 이를 수행해야 합니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 시스템 관리자는 **서버 관리자 역할** 에 서버의 작업에 무제한 액세스할 수 있는 멤버 자격을 부여해야 합니다. 이 역할은 사용 권한이 고정되며 사용자 지정할 수 없습니다. 기본적으로 로컬 관리자 그룹의 멤버는 자동으로 Analysis Services 시스템 관리자가 됩니다.  
  
 데이터를 쿼리하거나 처리하는 관리 권한이 없는 사용자에게는 **데이터베이스 역할**을 통한 액세스 권한을 부여합니다. 시스템 관리자 및 데이터베이스 관리자는 특정 데이터베이스 내에 서로 다른 수준의 액세스를 나타내는 역할을 만든 다음 액세스가 필요한 모든 사용자에게 멤버 자격을 할당할 수 있습니다. 각 역할에는 특정 데이터베이스 내의 개체 및 작업에 액세스할 수 있는 사용자 지정된 권한 집합을 부여합니다. 데이터베이스, 큐브 및 차원(큐브 뷰 제외)과 같은 내부 개체, 행 수준에서 사용 권한을 지정할 수 있습니다.  
  
 역할을 만들고 별도 작업으로 멤버 자격을 지정하는 것이 일반적입니다. 대부분의 경우 모델 디자이너는 디자인 단계에서 역할을 추가합니다. 이렇게 하면 모든 역할 정의가 모델을 정의하는 프로젝트 파일에 반영됩니다. 일반적으로 데이터베이스는, 독립적인 작업으로 개발, 테스트, 실행할 수 있는 스크립트를 만드는 데이터베이스 관리자가 프로덕션 환경으로 전환하기 때문에 역할 멤버 자격은 나중에 전달됩니다.  
  
 모든 권한 부여는 유효한 Windows 사용자 ID를 기반으로 합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 Windows 인증만을 사용하여 사용자 ID를 인증합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 독점적인 인증 방법을 제공하지 않습니다. [Analysis Services에서 지원하는 인증 방법](../../analysis-services/instances/authentication-methodologies-supported-by-analysis-services.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  데이터베이스의 모든 역할에서 각 Windows 사용자 및 그룹에 대해 권한은 부가적입니다. 한 역할은 사용자나 그룹에게 특정 태스크를 수행하거나 데이터를 볼 수 있는 사용 권한을 부여하지 않지만 다른 역할이 이 사용자나 그룹에게 이러한 사용 권한을 부여하는 경우 해당 사용자나 그룹은 작업을 수행하거나 데이터를 볼 수 있게 됩니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [개체 및 작업에 대한 액세스 승인&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)  
  
-   [데이터베이스 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md)  
  
-   [큐브 또는 모델 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)  
  
-   [처리 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md)  
  
-   [개체 메타데이터에 대한 정의 읽기 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-read-definition-permissions-on-object-metadata-analysis-services.md)  
  
-   [데이터 원본 개체에 대한 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-permissions-on-a-data-source-object-analysis-services.md)  
  
-   [데이터 마이닝 구조 및 모델에 대한 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)  
  
-   [차원에 대한 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-permissions-on-a-dimension-analysis-services.md)  
  
-   [차원 데이터에 대한 사용자 지정 액세스 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md)  
  
-   [셀 데이터에 대한 사용자 지정 액세스 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md)  
  
## <a name="see-also"></a>관련 항목:  
 [역할 만들기 및 관리&#40;SSAS 테이블 형식&#41;](../../analysis-services/tabular-models/create-and-manage-roles-ssas-tabular.md)  
  
  
