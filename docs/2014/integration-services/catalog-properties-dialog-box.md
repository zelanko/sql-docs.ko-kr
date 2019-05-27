---
title: 카탈로그 속성 대화 상자 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.iscatalogprop.general.f1
- sql12.ssis.ssms.iscreatecatalog.f1
ms.assetid: 3e2fcf11-e010-41c6-bc26-e4b281c0bfbc
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8d3492cce19906322ef9b420718aae0ae9e0e62d
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66061108"
---
# <a name="catalog-properties-dialog-box"></a>카탈로그 속성 대화 상자
  카탈로그 속성 대화 상자를 사용하여 SSISDB 카탈로그를 구성할 수 있습니다. 카탈로그 속성은 중요한 데이터가 암호화되는 방법, 작업 및 프로젝트 버전 관리 데이터가 보존되는 방법 및 유효성 검사 작업의 제한 시간을 정의합니다. SSISDB 카탈로그는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트, 패키지, 매개 변수 및 환경에 대한 중앙 스토리지 및 관리 지점 역할을 합니다.  
  
 또한 catalog.catalog_property 뷰에서 카탈로그 속성을 보고 catalog.configure_catalog 저장 프로시저를 사용하여 속성을 설정할 수 있습니다. 자세한 내용은 [catalog.catalog_properties&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-views/catalog-catalog-properties-ssisdb-database) 및 [catalog.configure_catalog&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database)를 참조하세요.  
  
 SSISDB 카탈로그를 만드는 방법에 대한 자세한 내용은 [SSIS 카탈로그 만들기](catalog/ssis-catalog.md)를 참조하세요.  
  
 **수행 작업**  
  
-   [카탈로그 속성 대화 상자 열기](#open_dialog)  
  
-   [옵션 구성](#options)  
  
##  <a name="open_dialog"></a> 카탈로그 속성 대화 상자 열기  
  
1.  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]를 엽니다.  
  
2.  Microsoft SQL Server 데이터베이스 엔진에 연결합니다.  
  
3.  개체 탐색기에서 **Integration Services** 노드를 확장하고 **SSISDB**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
##  <a name="options"></a> 옵션 구성  
  
### <a name="options"></a>변수  
 다음 표에서는 대화 상자의 특정 속성과 catalog.catalog_property 뷰의 해당 속성에 대해 설명합니다.  
  
|속성 이름(카탈로그 속성 대화 상자)|속성 이름(catalog.catalog_property 뷰)|Description|  
|-----------------------------------------------------|------------------------------------------------------|-----------------|  
|암호화 알고리즘 이름|ENCRYPTION_CLEANUP_ENABLED|카탈로그의 중요한 매개 변수 값을 암호화하는 데 사용되는 암호화 유형을 지정합니다. 가능한 값은 다음과 같습니다.<br /><br /> **DES**<br /><br /> **TRIPLE_DES**<br /><br /> **TRIPLE_DES_3KEY**<br /><br /> **DESPX**<br /><br /> **AES_128**<br /><br /> **AES_192**<br /><br /> **AES_256** (기본값)|  
|유효성 검사 제한 시간(초)|VALIDATION_TIMEOUT|프로젝트 유효성 검사 또는 패키지 유효성 검사가 중지되기 전에 실행될 수 있는 최대 기간(초)을 지정합니다. 기본값은 300초입니다.<br /><br /> 유효성 검사 수행은 비동기 작업입니다. 프로젝트나 패키지가 클수록 유효성 검사에 걸리는 시간이 길어집니다.<br /><br /> 프로젝트와 패키지의 유효성을 검사하는 방법은 [Integration Services Data Types in Expressions](expressions/integration-services-data-types-in-expressions.md)를 참조하십시오.|  
|주기적으로 로그 정리|OPERATION_CLEANUP_ENABLED|SQL Server 에이전트 작업인 작업 정리가 실행되도록 지정하려면 이 속성을 True로 설정하고, 그렇지 않으면 이 속성을 False로 설정합니다.|  
|보존 기간(일)|RETENTION_WINDOW|허용 가능한 작업 데이터의 최대 수명(일)을 지정합니다. 지정된 일수보다 오래된 데이터는 SQL 에이전트 작업인 작업 정리를 통해 제거됩니다.|  
|프로젝트당 최대 버전 수|MAX_PROJECT_VERSIONS|카탈로그에 저장될 프로젝트 버전 수를 지정합니다. 최대값을 초과하는 오래된 버전의 프로젝트는 프로젝트 버전 정리 작업이 실행될 때 제거됩니다.|  
  
  
