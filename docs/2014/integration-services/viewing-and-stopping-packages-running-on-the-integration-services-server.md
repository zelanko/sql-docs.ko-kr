---
title: 보기 및 통합에서 실행 중인 패키지 중지 Services 서버 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- packages [Integration Services], managing
- managing running packages [Integration Services]
- packages [Integration Services], running
- running package [Integration Services], managing
ms.assetid: 11bf44e6-f6b0-475f-b816-40e914dbac80
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9a53cf3dbd11c87177c725cf246fb4b1016d87ed
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66054594"
---
# <a name="viewing-and-stopping-packages-running-on-the-integration-services-server"></a>Integration Services 서버에서 실행 중인 패키지 보기 및 중지
  `SSISDB` 데이터베이스는 사용자에게 표시되지 않는 내부 테이블에 실행 기록을 저장합니다. 그러나 공용 뷰 쿼리를 통해 이 데이터베이스에서 필요한 정보를 얻을 수 있습니다. 또한 이 데이터베이스는 패키지와 관련된 일반적인 태스크를 수행하기 위해 호출할 수 있는 저장 프로시저를 제공합니다.  
  
 일반적으로 서버의 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 개체는 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 관리합니다. 그러나 데이터베이스 뷰를 쿼리하고 저장 프로시저를 직접 호출하거나 관리되는 API를 호출하는 사용자 지정 코드를 작성할 수도 있습니다. [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 및 관리되는 API는 뷰를 쿼리하고 저장 프로시저를 호출하여 많은 태스크를 수행합니다. 예를 들어 서버에서 현재 실행 중인 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지 목록을 보고 필요한 경우 패키지를 중지하도록 요청할 수 있습니다.  
  
## <a name="viewing-the-list-of-running-packages"></a>실행 중인 패키지 목록 보기  
 서버에서 현재 실행 중인 패키지 목록을 **활성 작업** 대화 상자에서 볼 수 있습니다. 자세한 내용은 [Active Operations Dialog Box](../../2014/integration-services/active-operations-dialog-box.md)를 참조하세요.  
  
 실행 중인 패키지 목록을 보는 데 사용할 수 있는 다른 방법은 다음 항목을 참조하십시오.  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] 액세스  
 서버에서 실행 중인 패키지 목록을 보려면 상태가 2인 패키지에 대해 [catalog.executions&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-views/catalog-executions-ssisdb-database) 뷰를 쿼리합니다.  
  
 관리되는 API를 통해 프로그래밍 방식으로 액세스  
 <xref:Microsoft.SqlServer.Management.IntegrationServices> 네임스페이스 및 해당 클래스를 참조하세요.  
  
## <a name="stopping-a-running-package"></a>실행 중인 패키지 중지  
 **활성 작업** 대화 상자에서 실행 중인 패키지를 중지하도록 요청할 수 있습니다. 자세한 내용은 [Active Operations Dialog Box](../../2014/integration-services/active-operations-dialog-box.md)를 참조하세요.  
  
 실행 중인 패키지를 중지하는 데 사용할 수 있는 다른 방법은 다음 항목을 참조하십시오.  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] 액세스  
 서버에서 실행 중인 패키지를 중지하려면 [catalog.stop_operation&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-stop-operation-ssisdb-database) 저장 프로시저를 호출합니다.  
  
 관리되는 API를 통해 프로그래밍 방식으로 액세스  
 <xref:Microsoft.SqlServer.Management.IntegrationServices> 네임스페이스 및 해당 클래스를 참조하세요.  
  
## <a name="viewing-the-history-of-packages-that-have-run"></a>실행된 패키지 기록 보기  
 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]에서 실행된 패키지의 기록을 보려면 **모든 실행** 보고서를 사용합니다. **모든 실행** 보고서 및 다른 표준 보고서에 대한 자세한 내용은 [Integration Services 서버를 위한 보고서](../../2014/integration-services/reports-for-the-integration-services-server.md)를 참조하세요.  
  
 실행 중인 패키지의 기록을 보는 데 사용할 수 있는 다른 방법에 대한 자세한 내용은 다음 항목을 참조하십시오.  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] 액세스  
 실행된 패키지에 대한 정보를 보려면 [catalog.executions&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-views/catalog-executions-ssisdb-database) 뷰를 쿼리합니다.  
  
 관리되는 API를 통해 프로그래밍 방식으로 액세스  
 <xref:Microsoft.SqlServer.Management.IntegrationServices> 네임스페이스 및 해당 클래스를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [프로젝트 및 패키지 실행](packages/run-integration-services-ssis-packages.md)   
 [패키지 실행 보고서 문제 해결](troubleshooting/troubleshooting-reports-for-package-execution.md)  
  
  
