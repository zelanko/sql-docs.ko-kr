---
title: "Integration Services 서비스 관리 | Microsoft Docs"
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
  - "Integration Services 서비스, 구성"
  - "서비스 [Integration Services], 구성"
ms.assetid: 45554117-a0df-4830-b41c-5ebb33b764a5
caps.latest.revision: 63
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 63
---
# Integration Services 서비스 관리
    
> **중요!!** 이 항목에서는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 관리하는 Windows 서비스인 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스에 대해 설명합니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 는 이전 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]버전과의 호환성을 위한 서비스를 지원합니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터는 Integration Services 서버의 패키지와 같은 개체를 관리할 수 있습니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]구성 요소를 설치할 때 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스도 함께 설치됩니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 기본적으로 시작되며 서비스의 시작 유형은 자동으로 설정됩니다. 그러나 서비스를 사용하여 저장 및 실행 중인 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 패키지를 관리하려면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 도 설치해야 합니다.  
  
> **참고:** 레거시 Integration Services 서비스의 인스턴스에 직접 연결하려면 Integration Services 서비스가 실행 중인 SQL Server의 버전에 맞는 SSMS(SQL Server Management Studio) 버전을 사용해야 합니다. 예를 들어 SQL Server 2016의 인스턴스에서 실행 중인 레거시 Integration Services 서비스에 연결하려면 SQL Server 2016용으로 릴리스된 SSMS의 버전을 사용해야 합니다. [SSMS(SQL Server Management Studio) 다운로드합니다](https://msdn.microsoft.com/library/mt238290.aspx).
>
>   SSMS **서버에 연결** 대화 상자에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스의 이전 버전을 실행 중인 서버의 이름을 입력할 수 없습니다. 그러나 원격 서버에 저장된 패키지를 관리하는 경우 해당 원격 서버에 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스 인스턴스에 연결할 필요가 없습니다. 대신 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 원격 서버에 저장된 패키지를 표시하도록 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 서비스에 대한 구성 파일을 편집합니다. 자세한 내용은 [Integration Services 서비스 구성&#40;SSIS 서비스&#41;](../../integration-services/service/configuring-the-integration-services-service-ssis-service.md)을 참조하세요.  
  
 컴퓨터에는 하나의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스 인스턴스만 설치할 수 있습니다. 서비스는 특정 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 국한되지 않습니다. 서비스가 실행 중인 컴퓨터의 이름을 사용하여 서비스에 연결합니다.  
  
 MMC(Microsoft Management Console) 스냅인인 SQL Server 구성 관리자나 SQL Server 서비스 중 하나를 사용하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스를 관리할 수 있습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 패키지를 관리하려면 먼저 서비스를 시작해야 합니다.  
  
 기본적으로 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]와 동시에 설치되는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 인스턴스의 msdb 데이터베이스에 있는 패키지를 관리하도록 구성됩니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스가 동시에 설치되지 않는 경우 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 로컬 기본 인스턴스에 있는 msdb 데이터베이스에 저장된 패키지를 관리하도록 구성됩니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 명명된 인스턴스나 원격 인스턴스 또는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 여러 인스턴스에 저장된 패키지를 관리하려면 서비스의 구성 파일을 수정해야 합니다. 자세한 내용은 [Integration Services 서비스 구성&#40;SSIS 서비스&#41;](../../integration-services/service/configuring-the-integration-services-service-ssis-service.md)을 참조하세요.  
  
 기본적으로 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 서비스를 중지할 때 패키지 실행을 중지하도록 구성되어 있습니다. 그러나 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 패키지가 중지될 때까지 기다리지 않으며 일부 패키지는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스가 중지된 후에도 계속 실행될 수 있습니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스를 중지한 후에도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사, [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너, 패키지 실행 유틸리티 및 **dtexec** 명령 프롬프트 유틸리티(dtexec.exe)를 사용하여 패키지를 계속 실행할 수 있습니다. 그러나 실행 중인 패키지는 모니터링할 수 없습니다.  
  
 기본적으로 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 NETWORK SERVICE 계정의 컨텍스트에서 실행됩니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 이벤트를 Windows 이벤트 로그에 기록합니다. 서비스 이벤트는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 볼 수 있습니다. 또한 Windows 이벤트 뷰어를 사용하여 서비스 이벤트를 볼 수도 있습니다.  
  
### 서비스 스냅인을 사용하여 Integration Services 서비스 속성을 설정하려면  
  
-   [Integration Services 서비스 속성 설정](../../integration-services/service/set-the-properties-of-the-integration-services-service.md)  
  
### Integration Services 서비스의 서비스 이벤트를 보려면  
  
-   [Integration Services 서비스의 뷰 이벤트](../../integration-services/service/view-events-for-the-integration-services-service.md)  
  
## 관련 항목:  
 [Integration Services 서비스&#40;SSIS 서비스&#41;](../../integration-services/service/integration-services-service-ssis-service.md)   
 [Integration Services 서비스 구성&#40;SSIS 서비스&#41;](../../integration-services/service/configuring-the-integration-services-service-ssis-service.md)   
 [SQL Server 가져오기 및 내보내기 마법사](../Topic/SQL%20Server%20Import%20and%20Export%20Wizard.md)   
 [dtexec 유틸리티](../../integration-services/packages/dtexec-utility.md)   
 [프로젝트 및 패키지 실행](https://msdn.microsoft.com/library/ms141708(v=sql.130).aspx)  
  
  