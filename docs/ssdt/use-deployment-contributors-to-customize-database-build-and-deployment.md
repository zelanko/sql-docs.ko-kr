---
title: 배포 기여자를 사용하여 데이터베이스 배포 사용자 지정
description: 데이터베이스 프로젝트의 동작을 수정하는 방법을 알아봅니다. 빌드 및 배포 참가자에 대한 리소스를 보고 이 리소스를 사용하는 시나리오의 예를 확인합니다.
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: fe2064bb-e01e-4a12-9f12-a99aa9a5203f
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 4ca036a22497f05141a7777ddb00ac6ca53dab84
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987779"
---
# <a name="customize-database-build-and-deployment-by-using-build-and-deployment-contributors"></a>빌드 및 배포 참가자를 사용하여 데이터베이스 빌드 및 배포 사용자 지정

Visual Studio는 데이터베이스 프로젝트에 대한 빌드 및 배포 작업의 동작을 수정하기 위해 사용할 수 있는 확장성 지점을 제공합니다.  
  
## <a name="available-extensibility-points"></a>사용 가능한 확장성 지점  
다음 표에 표시된 것처럼 확장성 지점에 대한 확장을 만들 수 있습니다.  
  
|**동작**|**참가자 유형**|**참고 사항**|  
|--------------|------------------------|-------------|  
|빌드|BuildContributor|이 유형의 확장은 프로젝트 모델이 완전히 유효성 검사된 후 SQL 프로젝트를 빌드할 때 실행됩니다. 빌드 참가자는 빌드 작업의 모든 속성 및 모든 사용자 지정 인수뿐만 아니라 완료된 모델에 액세스할 수 있습니다.|  
|배포|DeploymentPlanModifier|이 유형의 확장은 배포 계획이 생성된 후 실행되기 전에 배포 파이프라인의 일부로 SQL 프로젝트가 배포될 때 실행됩니다. DeploymentPlanModifier를 사용하면 단계를 추가하거나 제거하여 배포 계획을 수정할 수 있습니다. 배포 참가자는 배포 계획, 비교 결과 및 원본 및 대상 모델에 액세스할 수 있습니다.|  
|배포|DeploymentPlanExecutor|이 유형의 확장은 배포 계획이 실행될 때 실행되며, 배포 계획에 대한 읽기 전용 액세스를 제공합니다. DeploymentPlanExectutor는 배포 계획을 기반으로 작업을 수행합니다.|  
  
### <a name="supported-extensibility-scenarios"></a>지원되는 확장성 시나리오  
다음 예제 시나리오를 지원하도록 빌드 또는 배포 참가자를 구현할 수 있습니다.  
  
-   **프로젝트 빌드 중 스키마 설명서 생성** - 이 시나리오를 지원하기 위해서는 [BuildContributor](/dotnet/api/microsoft.sqlserver.dac.deployment.buildcontributor)를 구현하고 스키마 설명서를 생성하도록 OnExecute 메서드를 재정의합니다. 확장을 실행할지 여부를 제어하고 출력 파일의 이름을 지정하는 기본 인수를 정의하는 대상 파일을 만들 수 있습니다.  
  
-   **SQL 프로젝트가 배포될 때 다른 보고서 생성** - 이 시나리오를 지원하기 위해서는 SQL 프로젝트를 배포할 때 XML 파일을 생성하는 [DeploymentPlanExecutor](/dotnet/api/microsoft.sqlserver.dac.deployment.deploymentplanexecutor)를 구현합니다.  
  
-   **데이터 동작 발생 시점을 변경하기 위한 배포 계획 수정** - 이 시나리오를 지원하기 위해서는 [DeploymentPlanModifier](/dotnet/api/microsoft.sqlserver.dac.deployment.deploymentplanmodifier)를 구현하고 배포 계획을 반복합니다. 해당 계획의 각 SqlTableMigrationStep에 대해 비교 결과를 조사해서 해당 단계를 수행하거나 건너 뛸지를 결정합니다.  
  
-   **SQL 프로젝트가 배포될 때 생성된 dacpac에 파일 복사** - 이 시나리오를 지원하기 위해서는 배포 참가자를 구현하고, 프로젝트 시스템에서 DeploymentExtensionConfiguration으로 표시된 파일을 지정하도록 OnEstablishDeploymentConfiguration 메서드를 재정의합니다. 이러한 파일은 출력 폴더에 복사되고 생성된 dacpac 내에 추가되어야 합니다. 또한 여러 파일을 출력 폴더에 복사되고 배포 매니페스트에 추가되는 하나의 새 파일로 병합하도록 참가자를 수정할 수도 있습니다. 배포 중에는 OnApplyDeploymentConfiguration 메서드를 구현해서 dacpac에서 해당 파일을 추출하고 OnExecute 메서드에서 사용하도록 준비할 수 있습니다.  
  
또한 참가자에서 데이터베이스 프로젝트 파일에 기록된 사용자 지정된 이름/값 인수 쌍을 노출할 수 있습니다. 이러한 인수를 사용해서는 참가자가 MSBuild에서 정보를 추출하거나 참가자의 최종 사용자가 동작을 사용자 지정할 수 있도록 설정할 수 있습니다. 예를 들어 사용자가 입력 또는 출력 파일의 이름을 지정하도록 허용할 수 있습니다.  
  
## <a name="common-tasks"></a>일반 태스크  
  
|**일반 태스크**|**지원 콘텐츠**|  
|--------------------|--------------------------|  
|**확장성 지점에 대해 자세히 알아보기:** 빌드 및 배포 기여자 구현을 위해 사용할 수 있는 기본 클래스에 대해 자세히 알아볼 수 있습니다.|[BuildContributor](/dotnet/api/microsoft.sqlserver.dac.deployment.buildcontributor)<br /><br />[DeploymentContributor](/dotnet/api/microsoft.sqlserver.dac.deployment.deploymentcontributor)|  
|**샘플 기여자 만들기:** 빌드 또는 배포 기여자를 만드는 데 필요한 단계에 대해 알아봅니다. 이 연습에서는 다음을 수행할 수 있습니다.<br /><br />-   모델의 모든 요소를 나열하는 보고서를 생성하는 빌드 참가자를 만듭니다.<br />-   실행 전 배포 계획을 변경하는 배포 참가자를 만듭니다.<br />-   SQL 프로젝트를 배포할 때 배포 보고서를 생성하는 배포 참가자를 만듭니다.<br /><br />팀에 참가자를 분배하려는 방법에 따라 모든 참가자를 단일 어셈블리에 또는 여러 어셈블리 사이에 만들 수 있습니다.|[연습: 데이터베이스 프로젝트 빌드를 확장하여 모델 통계 생성](../ssdt/walkthrough-extend-database-project-build-to-generate-model-statistics.md)<br /><br />[연습: 데이터베이스 프로젝트 배포를 확장하여 배포 계획 수정](../ssdt/walkthrough-extend-database-project-deployment-to-modify-the-deployment-plan.md)<br /><br />[연습: 데이터베이스 프로젝트 배포를 확장하여 배포 계획 분석](../ssdt/walkthrough-extend-database-project-deployment-to-analyze-the-deployment-plan.md)|  
  
## <a name="see-also"></a>참고 항목  
[SQL 단위 테스트에 대한 사용자 지정 조건 정의](/previous-versions/sql/sql-server-data-tools/jj860449(v=vs.103))  
