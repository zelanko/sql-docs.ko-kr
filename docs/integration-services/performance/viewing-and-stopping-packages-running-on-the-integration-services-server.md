---
title: "Integration Services 서버에서 실행 중인 패키지 보기 및 중지 | Microsoft Docs"
ms.custom: ""
ms.date: "08/26/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "패키지 [Integration Services], 관리"
  - "실행 중인 패키지 관리 [Integration Services]"
  - "패키지 [Integration Services], 실행"
  - "실행 중인 패키지 [Integration Services], 관리"
ms.assetid: 11bf44e6-f6b0-475f-b816-40e914dbac80
caps.latest.revision: 18
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 18
---
# Integration Services 서버에서 실행 중인 패키지 보기 및 중지
  **SSISDB** 데이터베이스는 사용자에게 표시되지 않는 내부 테이블에 실행 기록을 저장합니다. 그러나 공용 뷰 쿼리를 통해 이 데이터베이스에서 필요한 정보를 얻을 수 있습니다. 또한 이 데이터베이스는 패키지와 관련된 일반적인 태스크를 수행하기 위해 호출할 수 있는 저장 프로시저를 제공합니다.  
  
 일반적으로 서버의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 개체는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 관리합니다. 그러나 데이터베이스 뷰를 쿼리하고 저장 프로시저를 직접 호출하거나 관리되는 API를 호출하는 사용자 지정 코드를 작성할 수도 있습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 및 관리되는 API는 뷰를 쿼리하고 저장 프로시저를 호출하여 많은 태스크를 수행합니다. 예를 들어 서버에서 현재 실행 중인 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지 목록을 보고 필요한 경우 패키지를 중지하도록 요청할 수 있습니다.  
  
## 실행 중인 패키지 목록 보기  
 서버에서 현재 실행 중인 패키지 목록을 **활성 작업** 대화 상자에서 볼 수 있습니다. 자세한 내용은 [Active Operations Dialog Box](../../integration-services/performance/active-operations-dialog-box.md)를 참조하세요.  
  
 실행 중인 패키지 목록을 보는 데 사용할 수 있는 다른 방법은 다음 항목을 참조하십시오.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 액세스  
 서버에서 실행 중인 패키지 목록을 보려면 상태가 2인 패키지에 대해 [catalog.executions&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-executions-ssisdb-database.md) 뷰를 쿼리합니다.  
  
 관리되는 API를 통해 프로그래밍 방식으로 액세스  
 <xref:Microsoft.SqlServer.Management.IntegrationServices> 네임스페이스 및 해당 클래스를 참조하세요.  
  
## 실행 중인 패키지 중지  
 **활성 작업** 대화 상자에서 실행 중인 패키지를 중지하도록 요청할 수 있습니다. 자세한 내용은 [Active Operations Dialog Box](../../integration-services/performance/active-operations-dialog-box.md)를 참조하세요.  
  
 실행 중인 패키지를 중지하는 데 사용할 수 있는 다른 방법은 다음 항목을 참조하십시오.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 액세스  
 서버에서 실행 중인 패키지를 중지하려면 [catalog.stop_operation&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-stop-operation-ssisdb-database.md) 저장 프로시저를 호출합니다.  
  
 관리되는 API를 통해 프로그래밍 방식으로 액세스  
 <xref:Microsoft.SqlServer.Management.IntegrationServices> 네임스페이스 및 해당 클래스를 참조하세요.  
  
## 실행된 패키지 기록 보기  
 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 실행된 패키지의 기록을 보려면 **모든 실행** 보고서를 사용합니다. **모든 실행** 보고서 및 다른 표준 보고서에 대한 자세한 내용은 [Integration Services 서버를 위한 보고서](../../integration-services/performance/reports-for-the-integration-services-server.md)를 참조하세요.  
  
 실행 중인 패키지의 기록을 보는 데 사용할 수 있는 다른 방법에 대한 자세한 내용은 다음 항목을 참조하십시오.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 액세스  
 실행된 패키지에 대한 정보를 보려면 [catalog.executions&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-executions-ssisdb-database.md) 뷰를 쿼리합니다.  
  
 관리되는 API를 통해 프로그래밍 방식으로 액세스  
 <xref:Microsoft.SqlServer.Management.IntegrationServices> 네임스페이스 및 해당 클래스를 참조하세요.  
  
## 관련 항목:  
 [프로젝트 및 패키지 실행](https://msdn.microsoft.com/library/hh213290.aspx)   
 [패키지 실행 보고서 문제 해결](https://msdn.microsoft.com/library/gg471512.aspx)  
  
  