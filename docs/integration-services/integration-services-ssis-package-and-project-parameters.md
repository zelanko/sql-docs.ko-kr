---
title: "Integration Services (SSIS) 패키지 및 프로젝트 매개 변수 | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.designer.parameter.f1"
  - "sql13.dts.designer.paramterwindow.f1"
ms.assetid: 9ed9ca8e-8b1e-48d9-907d-285516d6562b
caps.latest.revision: 23
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 22
---
# Integration Services (SSIS) 패키지 및 프로젝트 매개 변수
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] (SSIS) 매개 변수를 사용 하 여 패키지 실행 시 패키지 내의 속성에 값을 할당할 수 있습니다. 프로젝트 수준에서 *프로젝트 매개 변수* 를 만들고 패키지 수준에서 *패키지 매개 변수* 를 만들 수 있습니다. 프로젝트 매개 변수는 프로젝트가 수신하는 외부 입력을 프로젝트 내 하나 이상의 패키지에 제공하기 위해 사용됩니다. 패키지 매개 변수를 사용하면 패키지를 편집하여 다시 배포할 필요 없이 패키지 실행을 수정할 수 있습니다.  
  
 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 에서 **Project.params** 창을 사용하여 프로젝트 매개 변수를 만들거나, 수정하거나, 삭제합니다. **** 디자이너의 매개 변수 [!INCLUDE[ssIS](../includes/ssis-md.md)] 탭을 사용하여 패키지 매개 변수를 만들고, 수정하고, 삭제합니다. **매개 변수화** 대화 상자를 사용하여 새 매개 변수나 기존 매개 변수를 태스크 속성과 연결합니다. **Project.params** 창 및 **매개 변수** 탭을 사용하는 방법은 [Create Parameters](../Topic/Create%20Parameters.md)를 참조하십시오. **매개 변수화** 대화 상자에 대한 자세한 내용은 [Parameterize Dialog Box](../Topic/Parameterize%20Dialog%20Box.md)를 참조하십시오.  
  
## 매개 변수 및 패키지 배포 모델  
 일반적으로 패키지 배포 모델을 사용하여 패키지를 배포하려면 매개 변수 대신 구성을 사용해야 합니다.  
  
 패키지 배포 모델을 사용하여 매개 변수가 포함된 패키지를 배포한 다음 패키지를 실행할 경우 실행 중에는 매개 변수가 호출되지 않습니다. 패키지에 패키지 매개 변수가 포함되고 있고 패키지 내의 식에 매개 변수가 사용되는 경우 결과 값은 런타임에 적용됩니다. 패키지에 프로젝트 매개 변수가 포함되어 있는 경우 패키지 실행이 실패할 수 있습니다.  
  
## 매개 변수 및 프로젝트 배포 모델  
 뷰, 저장된 프로시저를 사용 하는 SSIS (Integration Services) 서버에 프로젝트를 배포할 때와 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] UI 프로젝트 및 패키지 매개 변수를 관리 합니다. 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [뷰 & #40; Integration Services 카탈로그 & #41;](../integration-services/system-views/views-integration-services-catalog.md)  
  
-   [저장 프로시저 & #40; Integration Services 카탈로그 & #41;](../integration-services/system-stored-procedures/stored-procedures-integration-services-catalog.md)  
  
-   [구성 대화 상자](../integration-services/service/configure-dialog-box.md)  
  
-   [패키지 실행 대화 상자](../integration-services/packages/execute-package-dialog-box.md)  
  
### 매개 변수 값  
 매개 변수에는 최대 세 가지 서로 다른 유형의 값을 지정할 수 있습니다. 패키지 실행이 시작되면 매개 변수에 대해 단일 값이 사용되고 매개 변수가 해당 최종 리터럴 값으로 확인됩니다.  
  
 다음 표에서는 값 유형을 나열합니다.  
  
|값 이름|설명|값 유형|  
|----------------|-----------------|-------------------|  
|실행 값|특정 패키지 실행 인스턴스에 할당되는 값입니다. 이 할당은 다른 모든 값을 재정의하지만 단일 패키지 실행 인스턴스에만 적용됩니다.|리터럴|  
|서버 값|프로젝트를 Integration Services 서버에 배포한 후 프로젝트 범위 내에서 매개 변수에 지정된 값입니다. 이 값은 디자인 기본값을 재정의합니다.|리터럴 또는 환경 변수 참조|  
|디자인 값|[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 프로젝트가 생성되거나 편집될 때 매개 변수에 지정되는 값입니다. 이 값은 프로젝트와 함께 지속됩니다.|리터럴|  
  
 단일 매개 변수를 사용하여 여러 패키지 속성에 값을 지정할 수 있습니다. 단일 패키지 속성은 단일 매개 변수로부터의 값만 지정할 수 있습니다.  
  
###  <a name="executions"></a> 실행 및 매개 변수 값  
 *실행* 은 단일 패키지 실행 인스턴스를 나타내는 개체입니다. 실행을 만들 때는 실행 매개 변수 값과 같이 패키지를 실행하는 데 필요한 모든 세부 정보를 지정합니다. 기존 실행에 대한 매개 변수 값을 수정할 수도 있습니다.  
  
 실행 매개 변수 값을 명시적으로 설정할 때는 해당 실행 인스턴스에만 값을 적용할 수 있습니다. 실행 값은 서버 값 또는 디자인 값 대신 사용됩니다. 실행 값을 명시적으로 설정하지 않고 서버 값이 지정된 경우 서버 값이 사용됩니다.  
  
 매개 변수가 필수로 표시된 경우 해당 매개 변수에 대해 서버 값 또는 실행 값을 지정해야 합니다. 그렇지 않으면 해당 패키지가 실행되지 않습니다. 디자인 타임에는 매개 변수에 기본값이 있지만 프로젝트를 배포하면 기본값이 사용되지 않습니다.  
  
#### 환경 변수  
 매개 변수가 환경 변수를 참조하는 경우 해당 변수의 리터럴 값이 지정된 환경 참조를 통해 확인되고 매개 변수에 적용됩니다. 패키지 실행에 사용되는 최종 리터럴 매개 변수 값은 실행 매개 변수 값으로 참조됩니다. **실행** 대화 상자를 사용하여 실행에 대한 환경 참조를 지정합니다.  
  
 프로젝트 매개 변수가 환경 변수를 참조하고, 변수의 리터럴 값을 실행 시 확인할 수 없으면 디자인 값이 사용됩니다. 서버 값이 사용되지 않습니다.  
  
 매개 변수 값에 지정된 환경 변수를 보려면 catalog.object_parameters 뷰를 쿼리합니다. 자세한 내용은 참조 [catalog.object_parameters & #40; SSISDB 데이터베이스 & #41;](../integration-services/system-views/catalog-object-parameters-ssisdb-database.md)합니다.  
  
#### 실행 매개 변수 값 확인  
 매개 변수 값을 표시 및 설정하는 데 사용할 수 있는 Transact-SQL 뷰 및 저장 프로시저는 다음과 같습니다.  
  
 [catalog.execution_parameter_values & #40입니다. SSISDB 데이터베이스 & #41;](../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md)(뷰)  
 특정 실행에 사용될 실제 매개 변수 값을 보여 줍니다.  
  
 [catalog.get_parameter_values & #40입니다. SSISDB 데이터베이스 & #41;](../integration-services/system-stored-procedures/catalog-get-parameter-values-ssisdb-database.md) (저장된 프로시저)  
 지정된 패키지와 환경 참조의 실제 값을 확인하고 보여 줍니다.  
  
 [catalog.object_parameters & #40입니다. SSISDB 데이터베이스 & #41;](../integration-services/system-views/catalog-object-parameters-ssisdb-database.md) (뷰)  
 디자인 기본값 및 서버 기본값을 포함하여 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 카탈로그의 모든 패키지 및 속성에 대한 매개 변수와 속성을 표시합니다.  
  
 [catalog.set_execution_parameter_value & #40입니다. SSISDB 데이터베이스 & #41;](../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 카탈로그의 실행 인스턴스에 대한 매개 변수 값을 설정합니다.  
  
 또한 **** 의 패키지 실행 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 대화 상자를 사용하여 매개 변수 값을 수정할 수 있습니다. 자세한 내용은 [Execute Package Dialog Box](../integration-services/packages/execute-package-dialog-box.md)을 참조하세요.  
  
 Dtexec를 사용할 수도 있습니다 **/Parameter** 매개 변수 값을 수정 합니다. 자세한 내용은 [dtexec Utility](../integration-services/packages/dtexec-utility.md)를 참조하세요.  
  
### 매개 변수 유효성 검사  
 매개 변수 값을 확인할 수 없는 경우 해당 패키지 실행이 실패합니다. 오류를 방지하려면 **** 의 유효성 검사 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]대화 상자를 사용하여 프로젝트 및 패키지의 유효성을 검사합니다. 유효성 검사를 통해 모든 매개 변수가 필요한 값을 가지고 있는지 확인하거나 특정 환경 참조에 필요한 값을 확인할 수 있습니다. 유효성 검사는 또한 다른 일반적인 패키지 문제도 확인합니다.  
  
 자세한 내용은 [Validate Dialog Box](../integration-services/service/validate-dialog-box.md)을 참조하세요.  
  
### 매개 변수 예  
 이 예에서는 패키지의 옵션을 지정하는 데 사용되는 **pkgOptions** 라는 매개 변수를 설명합니다.  
  
 디자인 타임에 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 매개 변수가 생성될 때 매개 변수에 기본값 1이 할당되었습니다. 이 기본값을 디자인 기본값이라고 합니다. 프로젝트가 SSISDB 카탈로그에 배포되고 이 매개 변수에 다른 값이 할당되지 않은 경우 패키지 실행 시 **pkgOptions** 매개 변수에 해당하는 패키지 속성에 값 1이 할당됩니다. 디자인 기본값은 프로젝트와 함께 프로젝트 수명 주기 내내 지속됩니다.  
  
 특정 패키지 실행 인스턴스를 준비하는 경우 **pkgOptions** 매개 변수에 값 5가 할당됩니다. 이 값은 특정 실행 인스턴스에 대한 매개 변수에만 적용되므로 실행 값이라고 합니다. 실행이 시작되면 **pkgOptions** 매개 변수에 해당하는 패키지 속성에 값 5가 할당됩니다.  
  
## 관련 태스크  
 [매개 변수 만들기](../Topic/Create%20Parameters.md)  
  
 [프로젝트를 배포한 후 매개 변수 값 설정](../Topic/Set%20Parameter%20Values%20After%20the%20Project%20Is%20Deployed.md)  
  
## 관련 내용  
 mattmasson.com의 블로그 항목, [SSIS 빠른 팁: 필수 매개 변수](http://go.microsoft.com/fwlink/?LinkId=239781).  
  
  