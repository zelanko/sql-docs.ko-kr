---
title: 패키지 관리(SSIS 서비스) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Integration Services packages, managing
- packages [Integration Services], managing
- Integration Services packages, managing
- storing packages
- Stored Packages folder
- current packages
- Running Packages folder
- status information [Integration Services]
- SSIS packages, managing
- storage [Integration Services]
- monitoring [Integration Services], packages
- Integration Services service, package management
- services [Integration Services], package management
ms.assetid: 0261ed9e-3b01-4e37-a9d4-d039c41029b6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: beee5a99f345a4f70f31bfec78b4fb6d9280ab0a
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52761293"
---
# <a name="package-management-ssis-service"></a>패키지 관리(SSIS 서비스)
  패키지 관리에는 다음 태스크를 비롯한 태스크가 포함됩니다.  
  
-   실행 중인 패키지 모니터링  
  
-   패키지 스토리지 관리  
  
-   패키지 가져오기 및 내보내기  
  
> [!IMPORTANT]  
>  이 항목에서는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 관리하는 Windows 서비스인 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스에 대해 설명합니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 는 이전 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]버전과의 호환성을 위한 서비스를 지원합니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터는 Integration Services 서버의 패키지와 같은 개체를 관리할 수 있습니다.  
  
## <a name="package-store"></a>패키지 저장소  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지 액세스를 위해 **패키지 실행** 하 고 **패키지를 저장**합니다. **실행 중인 패키지** 폴더에는 서버에서 현재 실행 중인 패키지가 나열됩니다. **저장된 패키지** 폴더에는 패키지 저장소에 저장된 패키지가 나열됩니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스에서는 이 폴더에 나열된 패키지만 관리합니다. 패키지 저장소는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스 구성 파일에 나열된 msdb 데이터베이스나 파일 시스템 폴더 중 하나 또는 둘 다로 구성될 수 있습니다. 이 구성 파일에는 관리할 msdb와 파일 시스템 폴더가 지정되어 있습니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스에서 관리하지 않는 파일 시스템의 다른 위치에 패키지가 저장되어 있을 수도 있습니다.  
  
 msdb에 저장하는 패키지는 sysssispackages라는 테이블에 저장됩니다. msdb에 패키지를 저장할 때 패키지를 논리적 폴더로 그룹화할 수도 있습니다. 논리적 폴더를 사용하면 패키지를 용도별로 정리하거나 sysssispackages 테이블의 패키지를 필터링하는 데 유용합니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 새 논리적 폴더를 만들 수 있습니다. 기본적으로 msdb에 추가하는 논리적 폴더는 자동으로 패키지 저장소에 포함됩니다.  
  
 msdb의 패키지를 그룹화하기 위해 만드는 논리적 폴더는 msdb의 sysssispackagefolders 테이블에서 행으로 표시됩니다. sysssispackagefolders의 folderid 및 parentfolderid 열은 폴더 계층 구조를 정의합니다. msdb의 논리적 루트 폴더는 sysssispackagefolders에서 parentfolderid 열에 Null 값이 있는 행입니다. 자세한 내용은 [sysssispackages&#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/sysssispackages-transact-sql) 및 [sysssispackagefolders&#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/sysssispackagefolders-transact-sql)를 참조하세요.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 열고 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에 연결하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스에서 관리하는 msdb 폴더가 저장된 패키지 폴더 내에 표시됩니다. 구성 파일에 루트 파일 시스템 폴더가 지정되어 있으면 저장된 패키지 폴더에는 파일 시스템의 해당 폴더와 모든 하위 폴더에 저장된 패키지도 나열됩니다.  
  
 모든 파일 시스템 폴더에 패키지를 저장할 수 있지만 해당 폴더를 패키지 저장소의 구성 파일에 있는 폴더 목록에 추가하지 않으면 **저장된 패키지** 폴더의 하위 폴더에 해당 패키지가 나열되지 않습니다. 구성 파일에 대한 자세한 내용은 [Integration Services 서비스 구성&#40;SSIS 서비스&#41;](integration-services-service-ssis-service.md)을 참조하세요.  
  
 **실행 중인 패키지** 폴더에는 하위 폴더가 없으므로 확장할 수 없습니다.  
  
 기본적으로 **저장 된 패키지** 폴더에 두 개의 폴더가 포함 되어 있습니다. **파일 시스템** 하 고 **MSDB**합니다. **파일 시스템** 폴더에는 파일 시스템에 저장된 패키지가 나열됩니다. 이러한 파일의 위치는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스의 구성 파일에서 지정합니다. 기본 폴더는 %Program Files%\Microsoft SQL Server\100\DTS에 있는 Packages입니다. **MSDB** 폴더에는 서버의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] msdb 데이터베이스에 저장된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 패키지가 나열됩니다. sysssispackages 테이블에는 msdb에 저장된 패키지가 포함됩니다.  
  
 패키지 저장소의 패키지 목록을 보려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 열고 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에 연결해야 합니다. 자세한 내용은 [SQL Server Management Studio에서 Integration Services 패키지 보기&#40;SSIS 서비스&#41;](../view-integration-services-packages-in-sql-server-management-studio-ssis-service.md)버전과의 호환성을 위한 서비스를 지원합니다.  
  
## <a name="monitoring-running-packages"></a>실행 중인 패키지 모니터링  
 **실행 중인 패키지** 폴더에는 현재 실행 중인 패키지가 나열됩니다. **의** 요약 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]페이지에서 현재 패키지에 대한 정보를 보려면 **실행 중인 패키지** 폴더를 클릭합니다. **요약** 페이지에 실행 중인 패키지의 실행 시간과 같은 정보가 나열됩니다. 필요에 따라 최신 정보를 표시하려면 폴더의 내용을 새로 고칩니다.  
  
 **요약** 페이지에서 실행 중인 단일 패키지에 대한 정보를 보려면 해당 패키지를 클릭합니다. **요약** 페이지에 패키지의 버전 및 설명과 같은 정보가 표시됩니다.  
  
 **실행 중인 패키지** 폴더에서 패키지를 마우스 오른쪽 단추로 클릭한 다음 **중지**를 클릭하여 실행 중인 패키지를 중지할 수 있습니다.  
  
## <a name="managing-package-storage"></a>패키지 스토리지 관리  
 패키지 구성을 위해 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스의 구성 파일에 나열되는 루트 패키지 저장 폴더에 사용자 지정 폴더를 추가할 수 있습니다. 기본적으로 루트 폴더는 **파일 시스템** 및 **MSDB** 폴더입니다. 예를 들어 데이터 정리에 사용된 모든 패키지를 포함하는 **데이터 정리** 폴더를 **파일 시스템** 폴더에 추가할 수 있습니다. 또한 필요에 따라 사용자 지정 폴더 내에 또 다른 사용자 지정 폴더를 추가한 중첩된 폴더 계층을 만들 수도 있습니다. 사용자 지정 폴더는 삭제하거나 이름을 바꿀 수 있지만 구성 파일이 지정하는 루트 폴더의 이름은 바꾸거나 삭제할 수 없습니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 가 나열하는 루트 폴더를 업데이트하려면 구성 파일을 업데이트해야 합니다.  
  
 자세한 내용은 [Integration Services 서비스 구성&#40;SSIS 서비스&#41;](../configuring-the-integration-services-service-ssis-service.md)버전과의 호환성을 위한 서비스를 지원합니다.  
  
## <a name="importing-and-exporting-packages"></a>패키지 가져오기 및 내보내기  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지는 msdb 데이터베이스 또는 파일 시스템에 저장할 수 있습니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 가 제공하는 가져오기 또는 내보내기 기능을 사용하여 패키지를 한 유형의 저장소에서 다른 유형의 저장소로 복사할 수 있습니다. 또한 같은 유형의 스토리지에서 패키지를 가져오기 하여 다른 이름을 지정하면 패키지의 복사본을 만들 수 있습니다. 패키지 가져오기 및 내보내기는 **dtutil** 명령 프롬프트 유틸리티(dtutil.exe)로도 수행할 수 있습니다.  
  
 자세한 내용은 [dtutil Utility](../dtutil-utility.md)를 참조하세요.  
  
## <a name="related-tasks"></a>관련 작업  
  
-   [패키지 가져오기 및 내보내기&#40;SSIS 서비스&#41;](../import-and-export-packages-ssis-service.md)  
  
-   [SQL Server Management Studio에서 Integration Services 패키지 보기&#40;SSIS 서비스&#41;](../view-integration-services-packages-in-sql-server-management-studio-ssis-service.md)  
  
## <a name="see-also"></a>관련 항목:  
 [Integration Services 서비스&#40;SSIS 서비스&#41;](integration-services-service-ssis-service.md)  
  
  
