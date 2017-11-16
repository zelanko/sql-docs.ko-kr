---
title: "다차원 모델 데이터베이스 (SSAS) | Microsoft Docs"
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
- SQL Server Management Studio [Analysis Services], databases
- SQL Server Analysis Services, databases
- SSAS, databases
- Analysis Services, databases
- databases [Analysis Services], designing
- Business Intelligence Development Studio, databases [Analysis Services]
- databases [Analysis Services]
ms.assetid: 78b2f22a-b7bd-4a2b-b6fc-0bff4d2b3168
caps.latest.revision: 55
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2b9b4fa79c4ef7a37158c1fbeea32a80c56effa2
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="multidimensional-model-databases-ssas"></a>다차원 model 데이터베이스(SSAS)
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스는 데이터 원본, 데이터 원본 뷰, 큐브, 차원 및 역할의 모음입니다. 필요에 따라 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에는 데이터 마이닝 구조 및 데이터베이스에 사용자 정의 기능을 추가하기 위한 방법을 제공하는 사용자 지정 어셈블리가 포함될 수 있습니다.  
  
 큐브는 Analysis Services의 기본 쿼리 개체입니다. 클라이언트 응용 프로그램을 통해 Analysis Services 데이터베이스에 연결하면 해당 데이터베이스 내의 큐브에 연결됩니다. 차원, 어셈블리, 역할 또는 마이닝 구조를 여러 컨텍스트에서 다시 사용할 경우 데이터베이스에 여러 개의 큐브가 있을 수 있습니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 프로그래밍 방식으로 또는 다음 대화형 방법 중 하나를 사용하여 만들고 수정할 수 있습니다.  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 의 지정된 인스턴스로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]프로젝트를 배포합니다. 이 프로세스에서는 해당 이름을 가진 데이터베이스가 해당 인스턴스 내에 없을 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 만들고 새로 만든 데이터베이스 내의 디자인된 개체를 인스턴스화합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]데이터베이스 작업을 수행하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 프로젝트를 배포한 경우에만 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트의 개체 변경 내용이 적용됩니다.  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 또는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]를 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 인스턴스 내에 빈 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]데이터베이스를 만든 다음 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 를 사용하여 해당 데이터베이스에 직접 연결하고 프로젝트가 아닌 데이터베이스 내에 개체를 만듭니다. 이런 방식으로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스 작업을 수행하면 변경된 개체를 저장할 때 연결되어 있는 데이터베이스에 개체 변경 내용이 적용됩니다.  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 는 원본 제어 소프트웨어와 통합하여 여러 개발자가 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트 내의 여러 개체 작업을 동시에 수행하는 것을 지원합니다. 개발자는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 통하지 않고 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스와 직접 상호 작용할 수도 있지만 이 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스의 개체가 데이터베이스 배포에 사용된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트와 동기화되지 않을 위험이 있습니다. 배포 후에는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 를 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]데이터베이스를 관리합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 를 사용하여 파티션 및 역할과 같은 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]데이터베이스에 특정 변경이 수행될 수 있고 이로 인해 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스의 개체가 데이터베이스 배포에 사용된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트와 동기화되지 않을 수도 있습니다.  
  
## <a name="related-tasks"></a>관련 작업  
 [Analysis Services 데이터베이스 연결 및 분리](../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)  
  
 [Analysis Services 데이터베이스 백업 및 복원](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
 [Analysis Services 데이터베이스 문서화 및 스크립트](../../analysis-services/multidimensional-models/document-and-script-an-analysis-services-database.md)  
  
 [Analysis Services 데이터베이스 수정 또는 삭제](../../analysis-services/multidimensional-models/modify-or-delete-an-analysis-services-database.md)  
  
 [Analysis Services 데이터베이스 이동](../../analysis-services/multidimensional-models/move-an-analysis-services-database.md)  
  
 [다차원 데이터베이스 이름 바꾸기&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/rename-a-multidimensional-database-analysis-services.md)  
  
 [다차원 데이터베이스의 호환성 수준&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)  
  
 [다차원 데이터베이스 속성 설정&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/set-multidimensional-database-properties-analysis-services.md)  
  
 [Analysis Services 데이터베이스 동기화](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)  
  
 [ReadOnly 모드와 ReadWrite 모드 간 Analysis Services 데이터베이스 전환](../../analysis-services/multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)  
  
## <a name="see-also"></a>관련 항목:  
 [온라인 모드로 Analysis Services 데이터베이스에 연결](../../analysis-services/multidimensional-models/connect-in-online-mode-to-an-analysis-services-database.md)   
 [Analysis Services 프로젝트 만들기&#40;SSDT&#41;](../../analysis-services/multidimensional-models/create-an-analysis-services-project-ssdt.md)   
 [MDX 사용 하 여 다차원 데이터 쿼리](../../analysis-services/multidimensional-models/mdx/querying-multidimensional-data-with-mdx.md)  
  
  

