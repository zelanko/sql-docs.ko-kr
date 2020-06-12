---
title: 다차원 모델 솔루션 배포 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services deployments, planning
- deploying [Analysis Services]
- deploying [Analysis Services], planning
ms.assetid: 7259c201-ff54-43e8-bda5-a6d51474e0e6
author: minewiskan
ms.author: owend
ms.openlocfilehash: 21bbf20dfdc15470adc6277149679d2e5b403d9e
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546027"
---
# <a name="multidimensional-model-solution-deployment"></a>다차원 모델 솔루션 배포
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트 개발을 완료했으면 Analysis Services 서버에 데이터베이스를 배포할 수 있습니다. Analysis Services는 데이터베이스를 테스트 서버나 프로덕션 서버로 이동하는 데 사용할 수 있는 6가지의 배포 방법을 제공합니다. 메소드를 이점이 많은 순서에 따라 나열하면 AMO 자동화, XMLA, 배포 마법사, 배포 유틸리티, 동기화 마법사, 백업 및 복원과 같습니다.  
  
 이 항목에는 다음 섹션이 포함되어 있습니다.  
  
 [배포 방법](#bkmk_meth)  
  
 [배포 고려 사항](#bkmk_considerations)  
  
 [관련 작업](#bkmk_rel)  
  
##  <a name="deployment-methods"></a><a name="bkmk_meth"></a>배포 방법  
  
|방법|Description|링크|  
|------------|-----------------|----------|  
|**AMO(Analysis Management Objects) 자동화**|AMO는 솔루션 배포에 사용할 수 있는 명령을 포함하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 전체 명령 집합을 프로그래밍 방식으로 사용할 수 있는 인터페이스를 개발자에게 제공합니다. 솔루션 배포를 위한 방법으로 AMO 자동화는 가장 유연한 방법이지만 프로그래밍이 필요합니다.  AMO를 사용하는 경우의 주요 이점은 SQL Server 에이전트와 AMO 애플리케이션을 함께 사용하여 미리 설정된 일정에 따라 배포를 실행할 수 있다는 것입니다.|[AMO&#40;Analysis Management Objects&#41;를 사용하여 개발](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo)|  
|**XMLA**|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하여 기존 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에 대한 메타데이터의 XMLA 스크립트를 생성하고 다른 서버에서 이 스크립트를 실행하여 초기 데이터베이스를 다시 만듭니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 배포 프로세스를 정의하고 코드화한 다음 XMLA 스크립트로 저장하여 XMLA 스크립트를 쉽게 만들 수 있습니다. XMLA 스크립트를 파일로 저장한 후에는 쉽게 일정에 따라 스크립트를 실행하거나 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스에 직접 연결하는 애플리케이션에 스크립트를 포함할 수 있습니다.<br /><br /> SQL Server 에이전트를 사용하여 미리 설정된 기준에 따라 XMLA 스크립트를 실행할 수도 있지만 XMLA 스크립트에는 AMO만큼의 융통성은 없습니다. AMO는 전체적인 범위의 관리 명령을 호스팅하여 가장 폭넓은 기능을 제공합니다.|[XMLA를 사용하여 모델 솔루션 배포](deploy-model-solutions-using-xmla.md)|  
|**배포 마법사**|배포 마법사를 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에서 생성된 XMLA 출력 파일로 프로젝트의 메타데이터를 대상 서버에 배포합니다. 배포 마법사를 사용하면 프로젝트 빌드의 출력 디렉터리에 생성되는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 파일을 사용하여 직접 배포할 수 있습니다.<br /><br /> [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사의 주요 이점은 편리함입니다. XMLA 스크립트를 나중에 사용하기 위해 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에 저장하는 것처럼 배포 마법사 스크립트를 저장할 수 있습니다. 배포 마법사는 대화형으로 실행하거나 배포 유틸리티를 통해 명령 프롬프트에서 실행할 수 있습니다.|[배포 마법사를 사용하여 모델 솔루션 배포](deploy-model-solutions-using-the-deployment-wizard.md)|  
|**배포 유틸리티**|배포 유틸리티를 사용하여 명령 프롬프트에서 Analysis Services 배포 엔진을 시작할 수 있습니다.|[배포 유틸리티를 사용하여 모델 솔루션 배포](deploy-model-solutions-with-the-deployment-utility.md)|  
|**데이터베이스 동기화 마법사**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스 동기화 마법사를 사용하여 두 데이터베이스 간의 메타데이터와 데이터를 동기화합니다.<br /><br /> 동기화 마법사를 사용하여 원본 서버의 데이터와 메타데이터를 모두 대상 서버로 복사할 수 있습니다. 대상 서버에 배포하려는 데이터베이스 복사본이 없을 경우 새 데이터베이스가 대상 서버로 복사됩니다. 대상 서버에 동일한 데이터베이스의 복사본이 이미 있을 경우에도 대상 서버의 데이터베이스가 업데이트되어 원본 데이터베이스의 메타데이터와 데이터를 사용합니다.|[Analysis Services 데이터베이스 동기화](synchronize-analysis-services-databases.md)|  
|**백업 및 복원**|백업은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 이동하는 가장 단순한 방법입니다. **백업** 대화 상자에서 옵션을 구성한 다음 대화 상자에서 직접 백업을 실행하거나 스크립트를 만들고 저장하여 필요할 때마다 실행할 수 있습니다.<br /><br /> 백업 및 복원은 다른 배포 방법만큼 자주 사용하지는 않지만 최소한의 인프라 요구 사항으로 배포를 빠르게 완료할 수 있습니다.|[Analysis Services 데이터베이스 백업 및 복원](backup-and-restore-of-analysis-services-databases.md)|  
  
##  <a name="deployment-considerations"></a><a name="bkmk_considerations"></a>배포 고려 사항  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 배포하기 전 다음과 같은 질문이 해당 솔루션에 적용되는지 확인하고 문제 해결 방법을 위해 관련 링크를 검토하십시오.  
  
|고려 사항|추가 정보 링크|  
|-------------------|------------------------------|  
|이 솔루션에 어떤 하드웨어 및 소프트웨어 리소스가 필요합니까?|[Analysis Services 배포에 대한 요구 사항 및 고려 사항](requirements-and-considerations-for-analysis-services-deployment.md)|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 패키지, 보고서 또는 관계형 데이터베이스 스키마와 같이 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트 범위 외부에 있는 관련 개체를 어떻게 배포합니까?||  
|배포된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에서 데이터를 어떻게 로드하고 업데이트합니까?<br /><br /> 배포된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에서 메타데이터(예: 계산)를 어떻게 업데이트하나요?|이 항목의[배포 방법](#bkmk_meth) .|  
|인터넷을 통해 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터에 대한 액세스를 사용자에게 제공하기를 원합니까?|[IIS&#40;인터넷 정보 서비스&#41; 8.0에서 Analysis Services에 대한 HTTP 액세스 구성](../instances/configure-http-access-to-analysis-services-on-iis-8-0.md)|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터에 대한 지속적인 쿼리 액세스를 제공하기를 원합니까?|[Analysis Services 배포에 대한 요구 사항 및 고려 사항](requirements-and-considerations-for-analysis-services-deployment.md)|  
|연결된 개체 또는 원격 파티션을 사용하여 분산 환경에 개체를 배포하기를 원합니까?|[로컬 파티션 만들기 및 관리&#40;Analysis Services&#41;](create-and-manage-a-local-partition-analysis-services.md), [원격 파티션 만들기 및 관리&#40;Analysis Services&#41;](create-and-manage-a-remote-partition-analysis-services.md) 및 [연결된 측정값 그룹](linked-measure-groups.md).|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터를 어떻게 보호합니까?|[개체 및 작업에 대한 액세스 승인&#40;Analysis Services&#41;](authorizing-access-to-objects-and-operations-analysis-services.md)|  
  
##  <a name="related-tasks"></a><a name="bkmk_rel"></a> 관련 작업  
 [Analysis Services 배포에 대한 요구 사항 및 고려 사항](requirements-and-considerations-for-analysis-services-deployment.md)  
  
 [XMLA를 사용하여 모델 솔루션 배포](deploy-model-solutions-using-xmla.md)  
  
 [배포 마법사를 사용하여 모델 솔루션 배포](deploy-model-solutions-using-the-deployment-wizard.md)  
  
 [배포 유틸리티를 사용하여 모델 솔루션 배포](deploy-model-solutions-with-the-deployment-utility.md)  
  
  
