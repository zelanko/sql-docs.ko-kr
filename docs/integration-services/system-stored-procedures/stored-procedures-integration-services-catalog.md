---
title: 저장 프로시저(Integration Services 카탈로그) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
helpviewer_keywords:
- stored procedures [Integration Services]
ms.assetid: a6ccd884-108f-4fb6-95ad-00b9cb65d5d6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9b9169d79a724d5d4a9d79f32d611e5b6faa4f0a
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86912719"
---
# <a name="stored-procedures-integration-services-catalog"></a>저장 프로시저(Integration Services 카탈로그)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  이 섹션에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 인스턴스에 배포된 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 관리하는 데 사용할 수 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 저장 프로시저에 대해 설명합니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 저장 프로시저를 호출하여 **SSISDB** 카탈로그에 저장된 개체를 추가, 제거, 수정 또는 실행할 수 있습니다.  
  
 카탈로그의 기본 이름은 SSISDB입니다. 카탈로그에 저장되는 개체에는 프로젝트, 패키지, 매개 변수, 환경 및 작업 기록이 있습니다.  
  
 데이터베이스 뷰 및 저장 프로시저를 직접 사용하거나 관리되는 API를 호출하는 사용자 지정 코드를 작성할 수 있습니다. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 및 관리되는 API는 뷰를 쿼리하고 이 섹션에 설명된 저장 프로시저를 호출하여 많은 태스크를 수행합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [catalog.add_data_tap](../../integration-services/system-stored-procedures/catalog-add-data-tap.md)  
 패키지 데이터 흐름에서 구성 요소 출력에 데이터 탭을 추가합니다.  
  
 [catalog.add_data_tap_by_guid](../../integration-services/system-stored-procedures/catalog-add-data-tap-by-guid.md)  
 패키지 데이터 흐름에서 특정 데이터 흐름 경로에 데이터 탭을 추가합니다.  
  
 [catalog.check_schema_version](../../integration-services/system-stored-procedures/catalog-check-schema-version.md)  
 SSISDB 카탈로그 스키마와 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 이진 파일(ISServerExec 및 SQLCLR 어셈블리)이 호환되는지 여부를 결정합니다.  
  
 [catalog.clear_object_parameter_value&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-clear-object-parameter-value-ssisdb-database.md)  
 서버에 저장된 기존 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트 또는 패키지에 대한 매개 변수 값을 지웁니다.  
  
 [catalog.configure_catalog(SSISDB 데이터베이스)](../../integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database.md)  
 카탈로그 속성을 지정된 값으로 설정하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그를 구성합니다.  
  
 [catalog.create_environment&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-create-environment-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 환경을 만듭니다.  
  
 [catalog.create_environment_reference&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-create-environment-reference-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그의 프로젝트에 대한 환경 참조를 만듭니다.  
  
 [catalog.create_environment_variable&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-create-environment-variable-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 환경 변수를 만듭니다.  
  
 [catalog.create_execution&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 실행 인스턴스를 만듭니다.  
  
 [catalog.create_execution_dump](../../integration-services/system-stored-procedures/catalog-create-execution-dump.md)  
 실행 중인 패키지가 일시 중지하고 덤프 파일을 만들도록 합니다.  
  
 [catalog.create_folder&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-create-folder-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 폴더를 만듭니다.  
  
 [catalog.delete_environment&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-delete-environment-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 있는 폴더에서 환경을 삭제합니다.  
  
 [catalog.delete_environment_reference&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-delete-environment-reference-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그의 프로젝트에서 환경 참조를 삭제합니다.  
  
 [catalog.delete_environment_variable&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-delete-environment-variable-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 있는 환경에서 환경 변수를 삭제합니다.  
  
 [catalog.delete_folder&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-delete-folder-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에서 폴더를 삭제합니다.  
  
 [catalog.delete_project &#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-delete-project-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 있는 폴더에서 기존 프로젝트를 삭제합니다.  
  
 [catalog.deny_permission(SSISDB 데이터베이스)](../../integration-services/system-stored-procedures/catalog-deny-permission-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그의 보안 개체에 대한 사용 권한을 거부합니다.  
  
 [catalog.deploy_project &#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그의 폴더에 프로젝트를 배포하거나 이전에 배포된 기존 프로젝트를 업데이트합니다.  
  
 [catalog.get_parameter_values&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-get-parameter-values-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 있는 프로젝트 및 해당 패키지에서 기본 매개 변수 값을 검색 및 확인합니다.  
  
 [catalog.get_project &#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-get-project-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 있는 기존 프로젝트의 속성을 검색합니다.  
  
 [catalog.grant_permission &#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-grant-permission-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그의 보안 개체에 대한 사용 권한을 허용합니다.  
  
 [catalog.move_environment&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-move-environment-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그 내에서 폴더 간에 환경을 이동합니다.  
  
 [catalog.move_project &#40;&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-move-project-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그 내에서 폴더 간에 프로젝트를 이동합니다.  
  
 [catalog.remove_data_tap](../../integration-services/system-stored-procedures/catalog-remove-data-tap.md)  
 실행 중인 구성 요소 출력에서 데이터 탭을 제거합니다.  
  
 [catalog.rename_environment&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-rename-environment-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 있는 환경의 이름을 변경합니다.  
  
 [catalog.rename_folder&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-rename-folder-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 있는 폴더의 이름을 변경합니다.  
  
 [catalog.restore_project &#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-restore-project-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그의 프로젝트를 이전 버전으로 복원합니다.  
  
 [catalog.revoke_permission(SSISDB 데이터베이스)](../../integration-services/system-stored-procedures/catalog-revoke-permission-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그의 보안 개체에 대한 사용 권한을 취소합니다.  
  
 [catalog.set_environment_property&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-property-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 있는 환경의 속성을 설정합니다.  
  
 [catalog.set_environment_reference_type&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-reference-type-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 있는 프로젝트에 대해 기존 환경 참조와 연결된 참조 유형 및 환경 이름을 설정합니다.  
  
 [catalog.set_environment_variable_property&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-variable-property-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 있는 환경 변수의 속성을 설정합니다.  
  
 [catalog.set_environment_variable_protection(SSISDB 데이터베이스)](../../integration-services/system-stored-procedures/catalog-set-environment-variable-protection-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그의 환경 변수에 대한 민감도 비트를 설정합니다.  
  
 [catalog.set_environment_variable_value&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-variable-value-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그의 환경 변수 값을 설정합니다.  
  
 [catalog.set_execution_parameter_value&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그의 실행 인스턴스에 대한 매개 변수 값을 설정합니다.  
  
 [catalog.set_execution_property_override_value](../../integration-services/system-stored-procedures/catalog-set-execution-property-override-value.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그의 실행 인스턴스에 대한 속성 값을 설정합니다.  
  
 [catalog.set_folder_description&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-set-folder-description-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그의 폴더에 대한 설명을 설정합니다.  
  
 [catalog.set_object_parameter_value&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-set-object-parameter-value-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그의 매개 변수 값을 설정합니다. 이 값을 환경 변수에 연결하거나, 할당된 다른 값이 없는 경우 기본적으로 사용할 리터럴 값을 할당합니다.  
  
 [catalog.start_execution&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그의 실행 인스턴스를 시작합니다.  
  
 [catalog.startup](../../integration-services/system-stored-procedures/catalog-startup.md)  
 SSISDB 카탈로그에 대한 작업의 상태를 유지 관리합니다.  
  
 [catalog.stop_operation&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-stop-operation-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그의 실행 인스턴스 또는 유효성 검사를 중지합니다.  
  
 [catalog.validate_package&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-validate-package-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 있는 패키지의 유효성을 비동기적으로 검사합니다.  
  
 [catalog.validate_project&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-validate-project-ssisdb-database.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 있는 프로젝트의 유효성을 비동기적으로 검사합니다.  
  
[catalog.add_execution_worker&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-add-execution-worker-ssisdb-database.md)   
Scale Out의 실행 인스턴스에 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out 작업자를 추가합니다.

[catalog.enable_worker_agent&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-enable-worker-agent-ssisdb-database.md)   
이 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그를 사용하여 Scale Out 마스터에 대한 Scale Out 작업자를 사용하도록 설정합니다.

[catalog.disable_worker_agent&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-disable-worker-agent-ssisdb-database.md)   
이 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그를 사용하여 Scale Out 마스터에 대한 Scale Out 작업자를 사용하지 않도록 설정합니다.


