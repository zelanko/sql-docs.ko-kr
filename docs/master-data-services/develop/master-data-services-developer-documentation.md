---
title: "Master Data Services 개발자 설명서 | Microsoft"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: develop
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 067b1f69-84eb-4a13-b220-120cd63704b4
caps.latest.revision: 
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 21898c90044ec62c1a7d55fbcfa0cf03d46ba7ce
ms.sourcegitcommit: 6ac1956307d8255dc544e1063922493b30907b80
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/05/2018
---
# <a name="master-data-services-developer-documentation"></a>Master Data Services 개발자 설명서
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]와 상호 작용하는 방식을 사용자 지정하기 위해 코드를 작성하는 방법에 대한 정보를 찾아볼 수 있습니다. 다음 작업을 수행하는 방법을 배워 보십시오.  
  
-   [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 서비스에 액세스하는 프로그램 작성. [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 서비스는 코드를 통해 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 기능을 제어하기 위해 개발자가 사용하는 WCF(Windows Communication Foundation) 서비스입니다.  
  
-   기존 응용 프로그램에 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 기능 통합  
  
-   [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] UI를 사용하여 수행하기 힘들거나 수행이 불가능한 반복 동작 또는 복잡한 동작을 수행하기 위한 코드 작성  
  
-   사용자가 지정하는 비즈니스 규칙에 대한 응답으로 실행되는 사용자 지정 워크플로 만들기. 사용자 지정 워크플로는 사용자가 작성하는 코드를 호출하며, 이 코드에는 워크플로를 처리하는 데 필요한 동작이 사용될 수 있습니다.  
  
## <a name="master-data-manager-web-service"></a>마스터 데이터 관리자 웹 서비스  
 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 서비스를 사용하면 사용자의 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 웹 사이트에 액세스할 수 있는 모든 컴퓨터에서 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]의 기능을 프로그래밍 방식으로 사용할 수 있습니다. 웹 서비스에 액세스하기 위한 코드를 작성하려면 먼저 지정하는 네임스페이스에 포함된 프록시 클래스를 생성해야 합니다. 이 설명서에서는 <xref:Microsoft.MasterDataServices>를 프록시 네임스페이스로 사용합니다. 웹 서비스 작업을 수행하는 데 사용되는 주요 프록시 클래스는 <xref:Microsoft.MasterDataServices.ServiceClient> 인터페이스를 구현하는 <xref:Microsoft.MasterDataServices.IService> 클래스입니다. 코드에서 <xref:Microsoft.MasterDataServices.ServiceClient> 클래스의 메서드를 호출하여 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 서비스에 액세스할 수 있습니다. 네임스페이스의 나머지 클래스는 웹 서비스 작업에서 사용합니다.  
  
### <a name="web-service-content"></a>웹 서비스 콘텐츠  
 [마스터 데이터 관리자 웹 서비스에 대한 프록시 클래스 만들기](../../master-data-services/develop/create-master-data-manager-web-service-proxy-classes.md)  
 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 사이트에서 메타데이터 게시를 활성화하고 웹 서비스 작업에 프로그래밍 방식으로 액세스하는 데 사용할 수 있는 프록시 클래스를 만드는 방법에 대해 설명합니다.  
  
 [범주별로 분류한 웹 서비스 작업&#40;Master Data Services&#41;](../../master-data-services/develop/categorized-web-service-operations-master-data-services.md)  
 <xref:Microsoft.MasterDataServices.ServiceClient> 클래스의 웹 서비스 작업을 범주별로 분류한 목록입니다.  
  
## <a name="custom-workflows"></a>사용자 지정 워크플로  
 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 는 비즈니스 규칙을 사용하여 기본적인 워크플로 솔루션을 만듭니다. 지정 조건에 따라 자동으로 데이터에 대해 업데이트 및 유효성 검사 작업을 수행하고 전자 메일 알림이 전송되게 할 수 있습니다. [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]의 비즈니스 규칙은 가장 일반적인 워크플로 시나리오를 관리하기 위한 것입니다. 워크플로에 다중 계층 승인 또는 복잡한 의사 결정 트리와 같은 보다 CEP(복합 이벤트 처리)가 필요한 경우 사용자가 만드는 사용자 지정 어셈블리로 데이터를 보내도록 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]를 구성할 수 있습니다. 사용자 지정 워크플로를 처리하려면 웹 응용 프로그램 컴퓨터에서 SQL Server MDS Workflow Integration Service를 구성 및 시작하고 <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender> 인터페이스를 구현하는 어셈블리를 만들어야 합니다.  
  
### <a name="custom-workflow-content"></a>사용자 지정 워크플로 콘텐츠  
 [사용자 지정 워크플로 만들기&#40;Master Data Services&#41;](../../master-data-services/develop/create-a-custom-workflow-master-data-services.md)  
 워크플로 처리기 어셈블리를 만드는 방법, SQL Server MDS Workflow Integration Service를 구성 및 시작하는 방법, [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]에서 사용자 지정 워크플로를 시작하는 비즈니스 규칙을 만드는 방법에 대한 지침입니다.  
  
## <a name="web-server-namespaces"></a>웹 서버 네임스페이스  
 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 가 웹 서버 컴퓨터에 어셈블리 집합을 설치합니다. 이러한 어셈블리에는 웹 서버 컴퓨터의 동작을 사용자 지정하는 고급 시나리오에 사용할 수 있는 네임스페이스가 포함됩니다. 다음 표에서는 이러한 네임스페이스에 대해 설명합니다.  
  
|Namespace|Description|  
|---------------|-----------------|  
|<xref:Microsoft.MasterDataServices.Deployment>|모델에서 배포 패키지를 만들고 패키지를 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 데이터베이스에 배포하는 데 사용할 수 있는 클래스를 포함합니다.|  
|<xref:Microsoft.MasterDataServices.Services>|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 응용 프로그램을 통해 웹 서버 컴퓨터에 대해 실행되는 웹 서비스 작업을 수신하고 처리하는 클래스를 포함합니다.|  
|<xref:Microsoft.MasterDataServices.Services.DataContracts>|데이터가 클라이언트 컴퓨터에서 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 응용 프로그램을 통해 웹 서버 컴퓨터로 전달되는 방법을 정의하는 클래스를 포함합니다.|  
|<xref:Microsoft.MasterDataServices.Services.MessageContracts>|요청 및 응답이 클라이언트 컴퓨터에서 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 응용 프로그램을 통해 웹 서버 컴퓨터로 전달되는 방법을 정의하는 클래스를 포함합니다.|  
|<xref:Microsoft.MasterDataServices.Services.ServiceContracts>|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 서비스를 통해 호출할 수 있는 작업을 정의하는 인터페이스를 포함합니다.|  
  
  
