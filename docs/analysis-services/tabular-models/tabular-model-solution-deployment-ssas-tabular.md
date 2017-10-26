---
title: "테이블 형식 모델 솔루션 배포 (SSAS 테이블 형식) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: aff96558-e5e5-4b95-8ddf-ee0709c842fb
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ad8d85e820ae8940a1b80dd130c57d5d06f140e6
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="tabular-model-solution-deployment-ssas-tabular"></a>테이블 형식 모델 솔루션 배포(SSAS 테이블 형식)
  테이블 형식 모델 프로젝트를 제작한 후에는 사용자가 보고 클라이언트 응용 프로그램을 사용하여 모델을 찾아볼 수 있도록 프로젝트를 배포해야 합니다. 이 항목에서는 사용자 환경에서 테이블 형식 모델 솔루션을 배포할 때 사용할 수 있는 다양한 속성과 메서드에 대해 설명합니다.  
  
 이 항목의 섹션:  
  
-   [이점](#bkmk_benefits)  
  
-   [SSDT(SQL Server Data Tools)에서 테이블 형식 모델 배포](#bkmk_deploying_bism)  
  
-   [배포 속성](#bkmk_deploy_props)  
  
-   [배포 방법](#bkmk_meth)  
  
-   [배포 서버 구성 및 배포된 모델에 연결](#bkmk_connecting)  
  
-   [관련 작업](#bkmk_rt)  
  
##  <a name="bkmk_benefits"></a> 이점  
 테이블 형식 모델을 배포하면 테스트, 준비 또는 프로덕션 환경에 model 데이터베이스가 만들어집니다. 그러면 사용자는 Sharepoint에서 .bism 연결 파일을 통해 또는 Microsoft Excel, [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]또는 사용자 지정 응용 프로그램과 같은 보고 클라이언트 응용 프로그램에서 직접 데이터 연결을 사용하여 배포된 모델에 연결할 수 있습니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 새 테이블 형식 모델 프로젝트와 함께 만들어지며 모델을 제작하는 데 사용되는 모델 작업 영역 데이터베이스는 작업 영역 서버 인스턴스에 남아 있으므로 필요한 경우 모델 프로젝트를 변경한 다음 테스트, 준비 또는 프로덕션 환경에 다시 배포할 수 있습니다.  
  
##  <a name="bkmk_deploying_bism"></a> SSDT(SQL Server Data Tools)에서 테이블 형식 모델 배포  
 솔루션을 배포하는 작업은 간단하지만 모델이 올바른 구성 옵션을 사용하여 올바른 Analysis Services 인스턴스로 배포되도록 몇 가지 단계를 수행해야 합니다.  
  
 테이블 형식 모델은 몇 가지 배포 특정 속성을 사용하여 정의됩니다. 배포할 때 **서버** 속성에서 지정한 Analysis Services 인스턴스에 대해 연결이 설정됩니다. 그런 다음 **데이터베이스** 속성에서 지정한 이름의 새 model 데이터베이스가 해당 인스턴스에 만들어집니다(아직 없는 경우). 모델 프로젝트의 Model.bim 파일에 있는 메타데이터를 사용하여 배포 서버의 model 데이터베이스에 있는 개체가 구성됩니다. **처리 옵션**을 사용하면 모델 메타데이터만 배포하여 model 데이터베이스를 만들지 여부를 지정할 수 있으며 **기본값** 또는 **전체** 를 지정한 경우 데이터 원본에 연결하는 데 사용된 가장 자격 증명이 모델 작업 영역 데이터베이스에서 배포된 model 데이터베이스로 메모리 내에 전달됩니다. 그런 다음 Analysis Services는 배포된 모델에 데이터를 채우는 작업을 실행합니다. 배포 프로세스가 완료되면 클라이언트 응용 프로그램에서 데이터 연결 또는 SharePoint의 .bism 연결 파일을 사용하여 모델에 연결할 수 있습니다.  
  
##  <a name="bkmk_deploy_props"></a> 배포 속성  
 프로젝트 배포 옵션 및 배포 서버 속성은 모델을 준비 또는 프로덕션 Analysis Services 환경에 배포하는 방법 및 위치를 지정합니다. 모든 모델 프로젝트에 대해 기본 속성 설정이 정의되지만 특정 배포 요구 사항에 따라 프로젝트별로 이러한 속성 설정을 변경할 수 있습니다. 기본 배포 속성 설정에 대한 자세한 내용은 [기본 데이터 모델링 및 배포 속성 구성&#40;SSAS 테이블 형식&#41;](../../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)을 참조하세요.  
  
### <a name="deployment-options-properties"></a>배포 옵션 속성  
 다음과 같은 배포 옵션 속성이 있습니다.  
  
|속성|기본 설정|Description|  
|--------------|---------------------|-----------------|  
|**처리 옵션**|**기본값**|이 속성은 개체에 대한 변경 내용을 배포할 때 필요한 처리 유형을 지정합니다. 이 속성에는 다음과 같은 옵션이 있습니다.<br /><br /> **기본값** – 이 설정은 Analysis Services에서 필요한 처리 유형을 결정하도록 지정합니다. 처리되지 않은 개체가 처리되며 필요한 경우 특성 관계, 특성 계층, 사용자 계층 및 계산 열을 다시 계산합니다. 이 설정을 사용하면 전체 처리 옵션을 사용할 때보다 일반적으로 배포 시간이 빨라집니다.<br /><br /> **처리 안 함** – 이 설정은 메타데이터만 배포되도록 지정합니다. 배포 후 배포된 모델에서 처리 작업을 실행하여 데이터를 업데이트하고 다시 계산해야 할 수 있습니다.<br /><br /> **전체** – 이 설정은 메타데이터가 배포되고 전체 처리 작업이 수행되도록 지정합니다. 이렇게 하면 배포된 모델의 메타데이터와 데이터가 최신 상태로 업데이트됩니다.|  
|**트랜잭션 배포**|**False**|이 속성은 배포가 트랜잭션인지 여부를 지정합니다. 기본적으로 모든 개체 또는 변경된 개체의 배포는 배포되는 개체의 처리에 있어서 트랜잭션이 아닙니다. 처리가 실패해도 배포는 성공하고 유지될 수 있습니다. 이를 변경하여 배포와 처리를 단일 트랜잭션에 통합할 수 있습니다.|  
|**쿼리 모드**|**메모리 내**|이 속성은 메모리 내(캐시됨) 모드 또는 DirectQuery 모드 중에서 쿼리 결과가 반환되는 원본이 실행되는 모드를 지정합니다. 이 속성에는 다음과 같은 옵션이 있습니다.<br /><br /> **DirectQuery** – 이 설정은 모델에 대한 모든 쿼리에서 관계형 데이터 원본만 사용하도록 지정합니다.<br /><br /> **DirectQuery with In-Memory** - 이 설정은 클라이언트의 연결 문자열에 다르게 지정되어 있지 않으면 기본적으로 관계형 원본을 사용하여 쿼리에 응답하도록 지정합니다.<br /><br /> **In-Memory** - 이 설정은 캐시만 사용하여 쿼리에 응답하도록 지정합니다.<br /><br /> **In-Memory with DirectQuery** - 이 설정은 기본적으로 클라이언트에서 연결 문자열에 다르게 지정되어 있지 않으면 캐시를 사용하여 쿼리에 응답하도록 지정합니다.<br /><br /> <br /><br /> 자세한 내용은 [DirectQuery 모드&#40;SSAS 테이블 형식&#41;](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)를 참조하세요.|  
  
### <a name="deployment-server-properties"></a>배포 서버 속성  
 다음과 같은 배포 서버 속성이 있습니다.  
  
|속성|기본 설정|Description|  
|--------------|---------------------|-----------------|  
|**서버**<br /><br /> 프로젝트가 생성될 때 설정됩니다.|**localhost**|프로젝트가 생성될 때 설정되는 이 속성은 모델이 배포될 이름별 Analysis Services 인스턴스를 지정합니다. 기본적으로 모델은 로컬 컴퓨터에 있는 기본 Analysis Services 인스턴스로 배포됩니다. 하지만 이 설정을 변경하여 로컬 컴퓨터의 명명된 인스턴스 또는 Analysis Services 개체를 만들 권한이 있는 원격 컴퓨터의 인스턴스를 지정할 수 있습니다.|  
|**버전**|작업 영역 서버가 위치한 인스턴스와 동일한 버전입니다.|이 속성은 모델이 배포될 Analysis Services 서버의 버전을 지정합니다. 서버 버전은 프로젝트에 통합할 수 있는 다양한 기능을 정의합니다. 기본적으로 로컬 Analysis Services 서버의 버전이 사용됩니다. 프로덕션 Analysis Services 서버 등의 다른 Analysis Services 서버를 지정하는 경우 해당 Analysis Services 서버의 버전을 지정해야 합니다.|  
|**데이터베이스**|**\<프로젝트 이름 >**|이 속성은 배포 시 모델 개체가 인스턴스화될 Analysis Services 데이터베이스의 이름을 지정합니다. 이 이름은 보고 클라이언트 데이터 연결 또는 .bism 데이터 연결 파일에도 지정됩니다.<br /><br /> 모델을 제작할 때 언제든지 이 이름을 변경할 수 있습니다. 모델을 배포한 후 이름을 변경하면 배포 후의 변경 내용은 이전에 배포한 모델에 영향을 주지 않습니다. 예를 들어 **TestDB** 이라는 솔루션을 열고 기본 model 데이터베이스 이름인 Model로 솔루션을 배포한 다음, 솔루션을 수정하고 model 데이터베이스 **Sales**의 이름을 바꾸면 솔루션이 배포된 Analysis Services 인스턴스에는 Model이라는 이름의 데이터베이스와 Sales라는 이름의 데이터베이스가 별도로 표시됩니다.|  
|**큐브 이름**|**Model**|이 속성은 클라이언트 도구(예: Excel)와 AMO(Analysis Management Objects)에 표시된 큐브 이름을 지정합니다.|  
  
### <a name="directquery-options-properties"></a>DirectQuery 옵션 속성  
 다음과 같은 배포 옵션 속성이 있습니다.  
  
|속성|기본 설정|Description|  
|--------------|---------------------|-----------------|  
|**가장 설정**|**기본값**|이 속성은 DirectQuery 모드로 실행되는 모델이 데이터 원본에 연결할 때 사용되는 가장 설정을 지정합니다. 메모리 내 캐시를 쿼리할 때는 가장 자격 증명이 사용되지 않습니다. 이 속성 설정에는 다음과 같은 옵션이 있습니다.<br /><br /> **기본값** – 이 설정은 테이블 가져오기 마법사를 사용하여 데이터 원본 연결이 만들어진 경우 Analysis Services가 가장 정보 페이지에서 지정한 옵션을 사용하도록 지정합니다.<br /><br /> **ImpersonateCurrentUser** – 이 설정은 모든 데이터 원본에 연결할 때 현재 로그온한 사용자의 사용자 계정이 사용되도록 지정합니다.|  
  
##  <a name="bkmk_meth"></a> 배포 방법  
 여러 가지 방법을 사용하여 테이블 형식 모델 프로젝트를 배포할 수 있습니다. 다차원 등의 다른 Analysis Services에 사용할 수 있는 대부분의 배포 방법은 테이블 형식 모델 프로젝트를 배포하는 데도 사용할 수 있습니다.  
  
|메서드|Description|링크|  
|------------|-----------------|----------|  
|**SQL Server Data Tools의 배포 명령**|배포 명령은 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 제작 환경에서 테이블 형식 모델 프로젝트를 배포하는 간단하고 직관적인 방법을 제공합니다.<br /><br /> **\*\* 주의 \*\*** 이 방법은 프로덕션 서버에 배포하는 데 사용하면 안 됩니다. 이 방법을 사용하면 기존 모델에서 특정 속성을 덮어쓸 수 있습니다.|[SQL Server Data Tools에서 배포&#40;SSAS 테이블 형식&#41;](../../analysis-services/tabular-models/deploy-from-sql-server-data-tools-ssas-tabular.md)|  
|**AMO(Analysis Management Objects) 자동화**|AMO는 솔루션 배포에 사용할 수 있는 명령을 포함하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 전체 명령 집합을 프로그래밍 방식으로 사용할 수 있는 인터페이스를 개발자에게 제공합니다. 솔루션 배포를 위한 방법으로 AMO 자동화는 가장 유연한 방법이지만 프로그래밍이 필요합니다.  AMO를 사용하는 경우의 주요 이점은 SQL Server 에이전트와 AMO 응용 프로그램을 함께 사용하여 미리 설정된 일정에 따라 배포를 실행할 수 있다는 것입니다.|[AMO&#40;Analysis Management Objects&#41;를 사용하여 개발](../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)|  
|**XMLA**|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하여 기존 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에 대한 메타데이터의 XMLA 스크립트를 생성하고 다른 서버에서 이 스크립트를 실행하여 초기 데이터베이스를 다시 만듭니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 배포 프로세스를 정의하고 코드화한 다음 XMLA 스크립트로 저장하여 XMLA 스크립트를 쉽게 만들 수 있습니다. XMLA 스크립트를 파일로 저장한 후에는 쉽게 일정에 따라 스크립트를 실행하거나 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스에 직접 연결하는 응용 프로그램에 스크립트를 포함할 수 있습니다.<br /><br /> SQL Server 에이전트를 사용하여 미리 설정된 기준에 따라 XMLA 스크립트를 실행할 수도 있지만 XMLA 스크립트에는 AMO만큼의 융통성은 없습니다. AMO는 전체적인 범위의 관리 명령을 호스팅하여 가장 폭넓은 기능을 제공합니다.|[XMLA를 사용하여 모델 솔루션 배포](../../analysis-services/multidimensional-models/deploy-model-solutions-using-xmla.md)|  
|**배포 마법사**|배포 마법사를 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에서 생성된 XMLA 출력 파일로 프로젝트의 메타데이터를 대상 서버에 배포합니다. 배포 마법사를 사용하면 프로젝트 빌드의 출력 디렉터리에 생성되는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 파일을 사용하여 직접 배포할 수 있습니다.<br /><br /> [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사의 주요 이점은 편리함입니다. XMLA 스크립트를 나중에 사용하기 위해 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에 저장하는 것처럼 배포 마법사 스크립트를 저장할 수 있습니다. 배포 마법사는 대화형으로 실행하거나 배포 유틸리티를 통해 명령 프롬프트에서 실행할 수 있습니다.|[배포 마법사를 사용하여 모델 솔루션 배포](../../analysis-services/multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)|  
|**배포 유틸리티**|배포 유틸리티를 사용하여 명령 프롬프트에서 Analysis Services 배포 엔진을 시작할 수 있습니다.|[배포 유틸리티를 사용하여 모델 솔루션 배포](../../analysis-services/multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md)|  
|**데이터베이스 동기화 마법사**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스 동기화 마법사를 사용하여 두 데이터베이스 간의 메타데이터와 데이터를 동기화합니다.<br /><br /> 동기화 마법사를 사용하여 원본 서버의 데이터와 메타데이터를 모두 대상 서버로 복사할 수 있습니다. 대상 서버에 배포하려는 데이터베이스 복사본이 없을 경우 새 데이터베이스가 대상 서버로 복사됩니다. 대상 서버에 동일한 데이터베이스의 복사본이 이미 있을 경우에도 대상 서버의 데이터베이스가 업데이트되어 원본 데이터베이스의 메타데이터와 데이터를 사용합니다.|[Analysis Services 데이터베이스 동기화](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)|  
|**Backup 및 Restore 메서드**|백업은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 이동하는 가장 단순한 방법입니다. **백업** 대화 상자에서 옵션을 구성한 다음 대화 상자에서 직접 백업을 실행하거나 스크립트를 만들고 저장하여 필요할 때마다 실행할 수 있습니다.<br /><br /> 백업 및 복원은 다른 배포 방법만큼 자주 사용하지는 않지만 최소한의 인프라 요구 사항으로 배포를 빠르게 완료할 수 있습니다.|[Analysis Services 데이터베이스 백업 및 복원](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)|  
  
##  <a name="bkmk_connecting"></a> 배포 서버 구성 및 배포된 모델에 연결  
 모델을 배포한 후에는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 Analysis Services 서버에서 구성할 수 있는 모델 데이터 액세스 보안, 백업 및 처리 작업에 대한 추가 고려 사항 사항이 있습니다. 이러한 속성 및 구성 설정은 이 항목에서 다루지 않지만 배포된 모델 데이터가 안전하고, 최신 상태로 유지되며, 조직의 사용자에게 가치 있는 데이터 분석 리소스를 제공하는 데 매우 중요합니다.  
  
 모델을 배포하고 선택적 서버 설정을 구성한 후에는 보고 클라이언트 응용 프로그램을 통해 모델을 연결할 수 있으며 모델을 사용하여 모델 메타데이터를 찾아보고 분석할 수 있습니다. 클라이언트 응용 프로그램에서 배포된 model 데이터베이스에 연결하는 방법은 이 항목에서 다루지 않습니다. 클라이언트 응용 프로그램에서 model 데이터베이스에 연결하는 방법을 자세히 알아보려면 [Tabular Model Data Access](../../analysis-services/tabular-models/tabular-model-data-access.md)을 참조하십시오.  
  
##  <a name="bkmk_rt"></a> 관련 작업  
  
|태스크|Description|  
|----------|-----------------|  
|[SQL Server Data Tools에서 배포&#40;SSAS 테이블 형식&#41;](../../analysis-services/tabular-models/deploy-from-sql-server-data-tools-ssas-tabular.md)|[!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 배포 명령을 사용하여 배포 속성을 구성하고 테이블 형식 모델 프로젝트를 배포하는 방법에 대해 설명합니다.|  
|[배포 마법사를 사용하여 모델 솔루션 배포](../../analysis-services/multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)|이 섹션의 항목에서는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사를 사용하여 테이블 형식 및 다차원 모델 솔루션 모두를 배포하는 방법에 대해 설명합니다.|  
|[배포 유틸리티를 사용하여 모델 솔루션 배포](../../analysis-services/multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 유틸리티를 사용하여 테이블 형식 및 다차원 모델 솔루션을 배포하는 방법에 대해 설명합니다.|  
|[XMLA를 사용하여 모델 솔루션 배포](../../analysis-services/multidimensional-models/deploy-model-solutions-using-xmla.md)|XMLA를 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 테이블 형식 솔루션 및 다차원 솔루션을 배포하는 방법에 대해 설명합니다.|  
|[Analysis Services 데이터베이스 동기화](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)|데이터베이스 동기화 마법사를 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 테이블 형식 또는 다차원 데이터베이스 간에 메타데이터와 데이터를 동기화하는 방법에 대해 설명합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [테이블 형식 model 데이터베이스에 연결&#40;SSAS&#41;](../../analysis-services/tabular-models/connect-to-a-tabular-model-database-ssas.md)  
  
  

