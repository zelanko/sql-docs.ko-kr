---
title: 패키지 백업 및 복원 (SSIS 서비스) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS packages, backup and restore
- backing up packages [Integration Services]
- packages [Integration Services], backup and restore
- SQL Server Integration Services packages, backup and restore
- restoring packages [Integration Services]
- Integration Services packages, backup and restore
ms.assetid: c67d3b83-a6c8-40de-920f-9236de4ac87f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b5c775393f7815084e8a79aae4be7f0974886f3e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66056928"
---
# <a name="package-backup-and-restore-ssis-service"></a>패키지 백업 및 복원(SSIS 서비스)
    
> [!IMPORTANT]  
>  이 항목에서는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지를 관리하는 Windows 서비스인 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스에 대해 설명합니다. [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 는 이전 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]버전과의 호환성을 위한 서비스를 지원합니다. [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]부터는 Integration Services 서버의 패키지와 같은 개체를 관리할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 시스템 데이터베이스인 파일 시스템 또는 msdb에 저장할 수 있습니다. msdb에 저장한 패키지는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 백업 및 복원 기능을 사용하여 백업하거나 복원할 수 있습니다.  
  
 msdb 데이터베이스 백업 및 복원에 대한 자세한 내용은 다음 항목을 클릭하세요.  
  
-   [SQL Server 데이터베이스 백업 및 복원](../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
-   [시스템 데이터베이스 백업 및 복원&#40;SQL Server&#41;](../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]에는 패키지를 관리 하는 데 사용할 수 있는 **dtutil** 명령 프롬프트 유틸리티 (dtutil)가 포함 되어 있습니다. 자세한 내용은 [dtutil Utility](dtutil-utility.md)를 참조하세요.  
  
## <a name="configuration-files"></a>구성 파일  
 패키지에 포함된 모든 구성 파일은 파일 시스템에 저장됩니다. msdb 데이터베이스를 백업할 때는 이러한 파일이 함께 백업되지 않으므로 msdb에 저장된 패키지의 보안을 설정하는 계획의 일부로 주기적으로 구성 파일을 백업해야 합니다. msdb 데이터베이스의 백업에 구성을 포함시키려면 파일 기반 구성 대신 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 유형 사용을 고려해야 합니다.  
  
## <a name="packages-stored-in-the-file-system"></a>파일 시스템에 저장된 패키지  
 파일 시스템에 저장한 패키지의 백업은 서버의 파일 시스템 백업 계획에 포함되어야 합니다. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스 구성 파일의 기본 이름은 MsDtsSrvr.ini.xml이며 서비스에서 모니터링하는 서버의 폴더를 나열합니다. 이러한 폴더는 백업해야 합니다. 또한 패키지를 서버의 다른 폴더에 저장할 수 있으며 이러한 폴더도 백업에 포함해야 합니다.  
  
  
