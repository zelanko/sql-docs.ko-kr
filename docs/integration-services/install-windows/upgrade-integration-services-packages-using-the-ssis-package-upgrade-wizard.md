---
title: SSIS 패키지 업그레이드 마법사를 사용하여 Integration Services 패키지 업그레이드 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, upgrading
- upgrading Integration Services packages
ms.assetid: 9359275a-48f5-4d1e-8ae7-e797759e3ccf
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 452ad0e1fec7ac1f4773a1d6a2491ba903f83884
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86915866"
---
# <a name="upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard"></a>SSIS 패키지 업그레이드 마법사를 사용하여 Integration Services 패키지 업그레이드

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  이전 버전의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 만들어진 패키지를 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 사용되는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 형식으로 업그레이드할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 이 과정을 돕는 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 업그레이드 마법사를 제공합니다. 원래 패키지를 백업하도록 마법사를 구성할 수 있으므로 업그레이드에 문제가 있을 경우 원래 패키지를 계속 사용할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 업그레이드 마법사는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 가 설치될 때 설치됩니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 업그레이드 마법사는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Standard, Enterprise 및 Developer Edition에서 사용할 수 있습니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 업그레이드하는 방법은 [Integration Services 패키지 업그레이드](../../integration-services/install-windows/upgrade-integration-services-packages.md)를 참조하세요.  
  
 이 항목의 나머지 부분에서는 마법사를 실행하고 원래 패키지를 백업하는 방법에 대해 설명합니다.  
  
## <a name="running-the-ssis-package-upgrade-wizard"></a>SSIS 패키지 업그레이드 마법사 실행  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 업그레이드 마법사는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]또는 명령줄에서 실행할 수 있습니다.  
  
#### <a name="to-run-the-wizard-from-sql-server-data-tools"></a>SQL Server Data Tools에서 마법사를 실행하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 만들거나 엽니다.  
  
2.  솔루션 탐색기에서 **SSIS 패키지** 노드를 마우스 오른쪽 단추로 클릭하고 **모든 패키지 업그레이드** 를 클릭하여 이 노드의 모든 패키지를 업그레이드합니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 이후 패키지가 포함된 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 프로젝트를 열면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 은 자동으로 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 업그레이드 마법사를 엽니다.  
  
#### <a name="to-run-the-wizard-from-sql-server-management-studio"></a>SQL Server Management Studio에서 마법사를 실행하려면  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에 연결하고 **저장된 패키지** 노드를 확장하고 **파일 시스템** 또는 **MSDB** 노드를 마우스 오른쪽 단추로 클릭한 다음 **패키지 업그레이드**를 클릭합니다.  
  
#### <a name="to-run-the-wizard-at-the-command-prompt"></a>명령 프롬프트에서 마법사를 실행하려면  
  
-   명령 프롬프트에서 **C:\Program Files\Microsoft SQL Server\130\DTS\Binn** 폴더의 SSISUpgrade.exe 파일을 실행합니다.  
  
## <a name="backing-up-the-original-packages"></a>원래 패키지 백업  
 원래 패키지를 백업하려면 원래 패키지와 업그레이드된 패키지가 파일 시스템의 같은 폴더에 저장되어 있어야 합니다. 마법사를 실행하는 방법에 따라 이 스토리지 위치는 자동으로 선택될 수 있습니다.  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] 에서 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]패키지 업그레이드 마법사를 실행하면 자동으로 원래 패키지와 업그레이드된 패키지가 파일 시스템의 같은 폴더에 저장됩니다.  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] 또는 명령 프롬프트에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 패키지 업그레이드 마법사를 실행하면 원래 패키지와 업그레이드된 패키지에 대해 다른 스토리지 위치를 지정할 수 있습니다. 원래 패키지를 백업하려면 원본 패키지와 업그레이드된 패키지가 파일 시스템의 같은 폴더에 저장되도록 지정해야 합니다. 다른 스토리지 옵션을 지정하면 마법사는 원래 패키지를 백업할 수 없게 됩니다.  
  
 마법사는 원래 패키지를 백업할 때 **SSISBackupFolder** 폴더에 원래 패키지의 복사본을 저장합니다. 마법사는 원래 패키지 및 업그레이드된 패키지가 포함된 폴더에 하위 폴더로 이 **SSISBackupFolder** 폴더를 만듭니다.  
  
#### <a name="to-back-up-the-original-packages-in-sql-server-management-studio-or-at-the-command-prompt"></a>SQL Server Management Studio 또는 명령 프롬프트에서 원래 패키지를 백업하려면  
  
1.  파일 시스템의 한 위치에 원래 패키지를 저장합니다.  
  
    > [!NOTE]  
    >  마법사의 백업 옵션은 파일 시스템에 저장된 패키지에서만 작동합니다.  
  
2.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 명령 프롬프트에서 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 업그레이드 마법사를 실행합니다.  
  
3.  마법사의 **원본 위치 선택** 페이지에서 **패키지 원본** 속성을 **파일 시스템**으로 설정합니다.  
  
4.  마법사의 **대상 위치 선택** 페이지에서 **원본 위치에 저장** 을 선택하여 업그레이드된 패키지를 원래 패키지 같은 위치에 저장합니다.  
  
    > [!NOTE]  
    >  마법사의 백업 옵션은 업그레이드된 패키지가 원래 패키지와 같은 폴더에 저장되어 있는 경우에만 사용할 수 있습니다.  
  
5.  마법사의 **패키지 관리 옵션 선택** 페이지에서 **원래 패키지 백업** 옵션을 선택합니다.  
  
#### <a name="to-back-up-the-original-packages-in-sql-server-data-tools"></a>SQL Server Data Tools에서 원래 패키지를 백업하려면  
  
1.  파일 시스템의 한 위치에 원래 패키지를 저장합니다.  
  
2.  마법사의 **패키지 관리 옵션 선택** 페이지에서 **원래 패키지 백업** 옵션을 선택합니다.  
  
    > [!WARNING]  
    >  마법사를 자동으로 실행하는 **에서** 이후 프로젝트를 열면 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 원래 패키지 백업 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]옵션이 표시되지 않습니다.  
  
3.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 업그레이드 마법사를 실행합니다.  
  
  
