---
title: SQL Server Data Tools에서 배포 (SSAS 테이블 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.deploystatus.f1
ms.assetid: 67dde3fe-ba43-41f3-b56c-c656029ee93f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6429fb7f30c748c7ac0a8ab69bc16c3d63b4d3ae
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66067297"
---
# <a name="deploy-from-sql-server-data-tools-ssas-tabular"></a>SQL Server Data Tools에서 배포(SSAS 테이블 형식)
  
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 배포 명령을 사용하여 테이블 형식 모델 솔루션을 배포하려면 이 항목의 태스크를 사용합니다.  
  
 이 항목의 섹션:  
  
-   [배포 옵션 및 배포 서버 속성 구성](#bkmk_deploy)  
  
-   [테이블 형식 모델 솔루션 배포](#bkmk_deploy_proc)  
  
-   [배포 상태](#bkmk_deploy_status)  
  
##  <a name="bkmk_deploy"></a>배포 옵션 및 배포 서버 속성 구성  
 테이블 형식 모델 솔루션을 배포하기 전에 먼저 배포 옵션 및 배포 서버 속성을 지정해야 합니다. 배포 속성 및 설정에 대한 자세한 내용은 [테이블 형식 모델 솔루션 배포&#40;SSAS 테이블 형식&#41;](tabular-model-solution-deployment-ssas-tabular.md)에서 배포 명령을 사용하여 테이블 형식 모델 솔루션을 배포하려면 이 항목의 태스크를 사용합니다.  
  
#### <a name="to-configure-deployment-options-and-deployment-server-properties"></a>배포 옵션 및 배포 서버 속성을 구성하려면  
  
1.  
  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]의 **솔루션 탐색기**에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
2.  프로젝트 이름> 속성 대화 상자의 **배포 옵션**에서 기본 설정과 다른 경우 속성 설정을 지정 합니다. ** \<**  
  
    > [!NOTE]  
    >  캐시된 모드의 모델의 경우 **쿼리 모드**는 항상 **메모리 내**입니다.  
  
    > [!NOTE]  
    >  DirectQuery 모드에서는 모델에 **가장 설정** 을 지정할 수 없습니다.  
  
3.  
  **배포 서버**에서 기본 설정과 다른 경우 **서버** (이름), **버전**, **데이터베이스** (이름) 및 **큐브 이름** 속성 설정을 지정한 다음 **확인**을 클릭합니다.  
  
> [!NOTE]  
>  새 프로젝트를 만들 때마다 자동으로 지정된 서버로 배포되도록 기본 배포 서버 속성 설정을 지정할 수도 있습니다. 자세한 내용은 [기본 데이터 모델링 및 배포 속성 구성&#40;SSAS 테이블 형식&#41;](properties-ssas-tabular.md)을 참조하세요.  
  
##  <a name="bkmk_deploy_proc"></a>테이블 형식 모델 솔루션 배포  
  
#### <a name="to-deploy-a-tabular-model-solution"></a>테이블 형식 모델 솔루션을 배포하려면  
  
-   의 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] **빌드** 메뉴에서 **프로젝트 이름 배포 \<>** 를 클릭 합니다.  
  
     처리 옵션 속성이 처리 안 함으로 설정되지 않았으면 **배포** 대화 상자에 메타데이터 배포 및 모델에 포함된 각 테이블의 처리 상태가 표시됩니다. 배포 프로세스가 완료된 후 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하여 Analysis Services 인스턴스에 연결하고 새 model 데이터베이스 개체가 만들어졌는지 확인하거나, 클라이언트 보고 애플리케이션을 사용하여 배포 모델에 연결합니다.  
  
##  <a name="bkmk_deploy_status"></a>배포 상태  
 
  **배포** 대화 상자에서는 배포 작업의 진행 상황을 모니터링할 수 있습니다. 배포 작업을 중지할 수도 있습니다.  
  
 **상태**  
 배포 작업의 성공 여부를 나타냅니다.  
  
 **세부 정보**  
 배포된 메타데이터 항목 및 각 메타데이터 항목의 상태를 나열하고 각 문제에 대한 메시지를 제공합니다.  
  
 **배포 중지**  
 배포 작업을 중지하려면 클릭합니다. 이 옵션은 배포 작업에 시간이 너무 많이 걸리거나 오류가 너무 많은 경우에 유용합니다.  
  
## <a name="see-also"></a>참고 항목  
 [테이블 형식 모델 솔루션 배포 &#40;SSAS 테이블 형식&#41;](tabular-model-solution-deployment-ssas-tabular.md)   
 [SSAS 테이블 형식&#41;&#40;기본 데이터 모델링 및 배포 속성 구성](properties-ssas-tabular.md)  
  
  
