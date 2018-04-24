---
title: 범주별로 분류한 웹 서비스 작업(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: ''
ms.component: develop
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: e3f346b5-7e26-481d-9821-1846e2e91289
caps.latest.revision: 7
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 1e5fa55ca294fd0ba85a88d0f8834db6b994f542
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="categorized-web-service-operations-master-data-services"></a>범주별로 분류한 웹 서비스 작업(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 웹 서비스에는 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]가 해당 사용자 인터페이스를 통해 사용하는 모든 기능을 제어하기 위한 코드를 작성할 수 있는 완전한 작업 집합이 포함되어 있습니다. 웹 서비스 작업은 <xref:Microsoft.MasterDataServices.IService> 인터페이스를 통해 정의되며 <xref:Microsoft.MasterDataServices.ServiceClient>에서 메서드로 구현됩니다. 이 항목에서는 웹 서비스 API를 사용하는 방법을 이해하는 데 도움이 되도록 웹 서비스 작업을 개념적 범주로 그룹화하였습니다.  
  
## <a name="model-operations"></a>모델 작업  
 이러한 작업은 모델을 만들고, 업데이트하고, 삭제하는 데 사용될 뿐 아니라 모델의 모든 콘텐츠(예: 엔터티, 계층 및 버전)에 대해 작업을 수행하는 데에도 사용됩니다. 자세한 내용은 [모델&#40;Master Data Services&#41;](../../master-data-services/models-master-data-services.md)을 참조하세요.  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.MetadataClone%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.MetadataCreate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.MetadataDelete%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.MetadataGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.MetadataUpdate%2A>|  
  
## <a name="entity-operations"></a>엔터티 작업  
 이러한 작업은 단일 엔터티의 멤버를 만들고, 업데이트하고, 삭제하는 데 사용됩니다. 자세한 내용은 [엔터티&#40;Master Data Services&#41;](../../master-data-services/entities-master-data-services.md) 및 [멤버&#40;Master Data Services&#41;](../../master-data-services/members-master-data-services.md)를 참조하세요.  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityMemberKeyLookup%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityMembersCopy%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityMembersCreate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityMembersDelete%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityMembersGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityMembersMerge%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityMembersUpdate%2A>|  
  
## <a name="member-operations"></a>멤버 작업  
 이러한 작업은 멤버를 가져오고, 업데이트하고, 삭제하는 데 사용됩니다. 작업의 대상이 되는 멤버 집합에는 여러 엔터티의 멤버를 포함할 수 있습니다. 자세한 내용은 [멤버&#40;Master Data Services&#41;](../../master-data-services/members-master-data-services.md)를 참조하세요.  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.ModelMembersBulkDelete%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.ModelMembersBulkMerge%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.ModelMembersBulkUpdate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.ModelMembersGet%2A>|  
  
## <a name="attribute-and-hierarchy-operations"></a>특성 및 계층 작업  
 이러한 작업은 특성 및 계층 정보를 가져오는 데 사용됩니다. 특성 및 계층은 <xref:Microsoft.MasterDataServices.ServiceClient.MetadataUpdate%2A>와 같은 모델 작업을 사용하여 수정할 수도 있습니다. 자세한 내용은 [특성&#40;Master Data Services&#41;](../../master-data-services/attributes-master-data-services.md) 및 [계층&#40;Master Data Services&#41;](../../master-data-services/hierarchies-master-data-services.md)을 참조하세요.  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityMemberAttributesGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.HierarchyMembersGet%2A>|  
  
## <a name="business-rule-operations"></a>비즈니스 규칙 작업  
 이러한 작업은 비즈니스 규칙을 만들고, 업데이트하고, 삭제하고, 게시하는 데 사용됩니다. 자세한 내용은 [비즈니스 규칙&#40;Master Data Services&#41;](../../master-data-services/business-rules-master-data-services.md)을 참조하세요.  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.BusinessRulesClone%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.BusinessRulesCreate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.BusinessRulesDelete%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.BusinessRulesGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.BusinessRulesPaletteGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.BusinessRulesPublish%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.BusinessRulesUpdate%2A>|  
  
## <a name="annotation-operations"></a>주석 작업  
 이러한 작업은 주석을 만들고, 업데이트하고, 삭제하는 데 사용됩니다. 자세한 내용은 [주석&#40;Master Data Services&#41;](../../master-data-services/annotations-master-data-services.md)을 참조하세요.  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.AnnotationsDelete%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.AnnotationsUpdate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityMemberAnnotationsCreate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityMemberAnnotationsGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.TransactionAnnotationsCreate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.TransactionAnnotationsGet%2A>|  
  
## <a name="transaction-operations"></a>트랜잭션 작업  
 이러한 작업은 트랜잭션을 가져오고 되돌리는 데 사용됩니다. 자세한 내용은 [트랜잭션&#40;Master Data Services&#41;](../../master-data-services/transactions-master-data-services.md)을 참조하세요.  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.TransactionsGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.TransactionsReverse%2A>|  
  
## <a name="version-and-validation-operations"></a>버전 및 유효성 검사 작업  
 이러한 작업은 버전을 복사하고 그 유효성을 검사하는 데 사용됩니다. 자세한 내용은 [버전&#40;Master Data Services&#41;](../../master-data-services/versions-master-data-services.md) 및 [유효성 검사&#40;Master Data Services&#41;](../../master-data-services/validation-master-data-services.md)를 참조하세요.  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.VersionCopy%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.ValidationGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.ValidationProcess%2A>|  
  
## <a name="data-quality-operations"></a>데이터 품질 작업  
 이러한 작업은 데이터 품질 태스크를 수행하고 그 결과를 검토하는 데 사용됩니다.  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.DataQualityCleansingOperationCreate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.DataQualityMatchingOperationCreate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.DataQualityInstalledState%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.DataQualityKnowledgeBasesGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.DataQualityOperationStart%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.DataQualityOperationResultsGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.DataQualityOperationStatus%2A>|  
  
## <a name="data-import-operations"></a>데이터 가져오기 작업  
 이러한 작업은 데이터를 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 데이터베이스로 가져오는 데 사용됩니다. 자세한 내용은 [개요: 테이블에서 데이터 가져오기&#40;Master Data Services&#41;](../../master-data-services/overview-importing-data-from-tables-master-data-services.md)를 참조하세요.  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityStagingClear%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityStagingGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityStagingLoad%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityStagingProcess%2A>|  
  
 다음 작업은 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]에 포함된 준비 프로세스를 사용하여 데이터를 가져오는 데 사용됩니다. 이러한 작업은 기존 데이터베이스를 지원하는 데에만 사용해야 합니다. 새로운 개발 작업에서는 앞에 나열된 작업을 사용하십시오.  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.StagingClear%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.StagingGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.StagingNameCheck%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.StagingProcess%2A>|  
  
## <a name="data-export-operations"></a>데이터 내보내기 작업  
 이러한 작업은 구독 뷰를 통해 데이터를 내보내는 데 사용됩니다. 자세한 내용은 [개요: 데이터 내보내기&#40;Master Data Services&#41;](../../master-data-services/overview-exporting-data-master-data-services.md)를 참조하세요.  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.ExportViewCreate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.ExportViewDelete%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.ExportViewListGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.ExportViewUpdate%2A>|  
  
## <a name="security-operations"></a>보안 작업  
 이러한 작업은 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 데이터베이스에 대한 액세스를 제어하는 보안 설정을 수정하는 데 사용됩니다. 자세한 내용은 [보안&#40;Master Data Services&#41;](../../master-data-services/security-master-data-services.md)을 참조하세요.  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SecurityPrincipalsClone%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SecurityPrincipalsCreate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SecurityPrincipalsDelete%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SecurityPrincipalsGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SecurityPrincipalsUpdate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SecurityPrivilegesClone%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SecurityPrivilegesCreate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SecurityPrivilegesDelete%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SecurityPrivilegesGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SecurityPrivilegesUpdate%2A>|  
  
## <a name="system-operations"></a>시스템 작업  
 이러한 작업은 시스템 설정 및 사용자 기본 설정을 가져오고 업데이트하는 데 사용됩니다.  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.ServiceCheck%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.ServiceVersionGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SystemDomainListGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SystemPropertiesGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SystemSettingsGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SystemSettingsUpdate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.UserPreferencesDelete%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.UserPreferencesGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.UserPreferencesUpdate%2A>|  
  
  
