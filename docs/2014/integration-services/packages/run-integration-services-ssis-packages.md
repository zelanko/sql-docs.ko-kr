---
title: 프로젝트 및 패키지 실행 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, running
- SSIS packages, running
- packages [Integration Services], running
- SQL Server Integration Services packages, running
- executing packages [Integration Services]
- running packages [Integration Services]
- Integration Services, (See also Integration Services packages)
ms.assetid: c5fecc23-6f04-4fb2-9a29-01492ea41404
author: janinezhang
ms.author: janinez
ms.openlocfilehash: fae1082d765bb8ab0c99edea252c89649558a9da
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84964793"
---
# <a name="execution-of-projects-and-packages"></a>프로젝트 및 패키지 실행
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 실행하려면 해당 패키지가 저장된 위치에 따라 여러 도구 중 하나를 사용할 수 있습니다. 도구는 다음 표에 나열되어 있습니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 패키지를 저장하려면 프로젝트 배포 모델을 사용하여 프로젝트를 서버에 배포합니다. 자세한 내용은 [Deploy Projects to Integration Services Server](../deploy-projects-to-integration-services-server.md)을 참조하세요.  
  
 SSIS 패키지 저장소, msdb 데이터베이스 또는 파일 시스템에 패키지를 저장하려면 패키지 배포 모델을 사용합니다. 자세한 내용은 [패키지 배포 &#40;SSIS&#41;](legacy-package-deployment-ssis.md)를 참조 하세요.  
  
|도구|Integration Services 서버에 저장된 패키지|SSIS 패키지 저장소 또는 msdb 데이터베이스에 저장된 패키지|SSIS 패키지 저장소에 포함되는 위치 외부에 있는 파일 시스템에 저장된 패키지|  
|----------|-----------------------------------------------------------------|--------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|  
|**SQL Server Data Tools**|아니요|예<br /><br /> 그러나 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 저장소(msdb 데이터베이스 포함)에서 프로젝트에 기존 패키지를 추가할 수 있습니다. 이러한 방식으로 프로젝트에 기존 패키지를 추가하면 파일 시스템에 패키지의 로컬 복사본을 만들 수 있습니다.|예|  
|**SQL Server Management Studio(Integration Services 서버를 호스트하는 데이터베이스 엔진의 인스턴스에 연결된 경우)**<br /><br /> 자세한 내용은 [Execute Package Dialog Box](../execute-package-dialog-box.md)를 참조하세요.|예|예<br /><br /> 그러나 이러한 위치에서 서버에 패키지를 가져올 수 있습니다.|예<br /><br /> 그러나 파일 시스템에서 서버에 패키지를 가져올 수 있습니다.|  
|**SQL Server Management Studio(SSIS 패키지 저장소를 관리하는 Integration Services 서비스에 연결된 경우)**|예|예|예<br /><br /> 그러나 파일 시스템에서 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 저장소로 패키지를 가져올 수 있습니다.|  
|**dtexec**<br /><br /> 자세한 내용은 [dtexec Utility](dtexec-utility.md)를 참조하세요.|예|예|예|  
|**dtexecui**<br /><br /> 자세한 내용은 [패키지 실행 유틸리티&#40;DtExecUI&#41; UI 참조](execute-package-utility-dtexecui-ui-reference.md)를 참조하세요.|예|예|예|  
|**SQL Server 에이전트**<br /><br /> 패키지를 예약하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업을 사용합니다.<br /><br /> 자세한 내용은 [SQL Server Agent Jobs for Packages](sql-server-agent-jobs-for-packages.md)을 참조하세요.|예|예|예|  
|**기본 제공 저장 프로시저**<br /><br /> 자세한 내용은 [catalog.start_execution&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database)을 참조하세요.|예|아니요|예|  
|****  네임스페이스의 형식 및 멤버를 사용한 관리형 API<xref:Microsoft.SqlServer.Management.IntegrationServices>|예|아니요|예|  
|****  네임스페이스의 형식 및 멤버를 사용한 관리형 API<xref:Microsoft.SqlServer.Dts.Runtime>|현재는 아님|예|예|  
  
## <a name="execution-and-logging"></a>실행 및 로깅  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지에 대한 로깅을 활성화할 수 있으며 로그 파일에서 런타임 정보를 확인할 수 있습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 로깅](../performance/integration-services-ssis-logging.md)을 참조하세요.  
  
 작업 보고서를 사용하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포되어 실행되는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 모니터링할 수 있습니다. 이 보고서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 사용할 수 있습니다. 자세한 내용은 [Reports for the Integration Services Server](../reports-for-the-integration-services-server.md)을(를) 참조하세요.  
  
## <a name="related-tasks"></a>관련 작업  
  
-   [SQL Server 에이전트를 사용하여 패키지 예약](../schedule-a-package-by-using-sql-server-agent.md)  
  
-   [SQL Server Data Tools에서 패키지 실행](../run-a-package-in-sql-server-data-tools.md)  
  
-   [SQL Server Management Studio를 사용하여 SSIS 서버에서 패키지 실행](../run-a-package-on-the-ssis-server-using-sql-server-management-studio.md)  
  
## <a name="see-also"></a>참고 항목  
 [dtexec 유틸리티](dtexec-utility.md)   
 [SQL Server 가져오기 및 내보내기 마법사](../import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)  
  
  
