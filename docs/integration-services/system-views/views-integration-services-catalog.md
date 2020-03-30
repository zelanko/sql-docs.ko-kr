---
title: 뷰(Integration Services 카탈로그) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
helpviewer_keywords:
- views [Integration Services]
ms.assetid: d0294d43-4852-46dc-9afa-d0c19ea9aa03
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6e1f54ee39981785f17c4883ec5dd191ecf7ccbc
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71295152"
---
# <a name="views-integration-services-catalog"></a>뷰 (Integration Services 카탈로그)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  이 섹션에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 인스턴스에 배포된 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 관리하는 데 사용할 수 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 뷰에 대해 설명합니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 뷰를 쿼리하여 **SSISDB** 카탈로그에 저장된 개체, 설정 및 작업 데이터를 검사할 수 있습니다.  
  
 카탈로그의 기본 이름은 SSISDB입니다. 카탈로그에 저장되는 개체에는 프로젝트, 패키지, 매개 변수, 환경 및 작업 기록이 있습니다.  
  
 데이터베이스 뷰 및 저장 프로시저를 직접 사용하거나 관리되는 API를 호출하는 사용자 지정 코드를 작성할 수 있습니다. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 및 관리되는 API는 뷰를 쿼리하고 이 섹션에 설명된 저장 프로시저를 호출하여 많은 태스크를 수행합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [catalog.catalog_properties&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그의 속성을 표시합니다.  
  
 [catalog.effective_object_permissions&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-effective-object-permissions-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 있는 모든 개체의 현재 보안 주체에 대한 유효 사용 권한을 표시합니다.  
  
 [catalog.environment_variables&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-environment-variables-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 있는 모든 환경에 대한 환경 변수 정보를 표시합니다.  
  
 [catalog.environments&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-environments-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 있는 모든 환경에 대한 자세한 정보를 표시합니다. 환경에는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트에서 참조할 수 있는 변수가 포함됩니다.  
  
 [catalog.execution_parameter_values&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md)  
 실행 인스턴스 중에 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지에서 사용한 실제 매개 변수 값을 표시합니다.  
  
 [catalog.executions&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-executions-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그의 패키지 실행 인스턴스를 표시합니다. 패키지 실행 태스크로 실행되는 패키지는 부모 패키지와 같은 실행 인스턴스에서 실행됩니다.  
  
 [catalog.explicit_object_permissions&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-explicit-object-permissions-ssisdb-database.md)  
 사용자에게 명시적으로 할당된 사용 권한만 표시합니다.  
  
 [catalog.extended_operation_info&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-extended-operation-info-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 있는 모든 작업에 대한 확장 정보를 표시합니다.  
  
 [catalog.folders&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-folders-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 있는 폴더를 표시합니다.  
  
 [catalog.object_parameters&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-object-parameters-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 있는 모든 패키지 및 프로젝트의 매개 변수를 표시합니다.  
  
 [catalog.object_versions &#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-object-versions-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 있는 개체의 버전을 표시합니다. 이 릴리스에서는 프로젝트 버전만 이 뷰에서 지원됩니다.  
  
 [catalog.operation_messages&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에서 작업 중에 기록된 메시지를 표시합니다.  
  
 [catalog.operations&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 있는 모든 작업에 대한 자세한 정보를 표시합니다.  
  
 [catalog.packages &#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-packages-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 표시된 모든 패키지에 대한 자세한 정보를 표시합니다.  
  
 [catalog.environment_references&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-environment-references-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 있는 모든 프로젝트의 환경 참조를 표시합니다.  
  
 [catalog.projects &#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-projects-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 표시된 모든 프로젝트에 대한 자세한 정보를 표시합니다.  
  
 [catalog.validations&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-validations-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 있는 모든 프로젝트 및 패키지 유효성 검사에 대한 자세한 정보를 표시합니다.  
  
[catalog.master_properties&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-master-properties-ssisdb-database.md)  
[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out 마스터의 속성을 표시합니다.

[catalog.worker_agents&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-worker-agents-ssisdb-database.md)  
[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out 작업자의 정보를 표시합니다.  
