---
title: SQL Server 가져오기 및 내보내기 마법사 시작 | Microsoft Docs
ms.custom: ''
ms.date: 06/20/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Import and Export Wizard
- starting SQL Server Import and Export Wizard
- Import and Export Wizard
- starting Import and Export Wizard
ms.assetid: 5fc4f6d1-1f6f-444e-9aeb-827f85e1c405
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: de2a16ccd38bad4fd36d5ca16cadd2e3264e6baf
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58270997"
---
# <a name="start-the-sql-server-import-and-export-wizard"></a>SQL Server 가져오기 및 내보내기 마법사 시작


이 항목에서 설명하는 방법 중 하나를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사를 시작하여 지원되는 데이터 원본에서 데이터를 가져오거나 내보낼 수 있습니다.

> [!IMPORTANT]
> 이 항목에서는 마법사를 **시작** 하는 방법만 설명합니다. 다른 내용을 찾으려면 [관련 태스크 및 콘텐츠](#related)를 참조하세요.

다음과 같은 방법으로 마법사를 시작할 수 있습니다.
-   지원되는 데이터 원본을 가져오거나 내보내려면 [시작 메뉴](#startStart)를 참조하세요.
-   지원되는 데이터 원본을 가져오거나 내보내려면 [명령 프롬프트](#startCmd)를 참조하세요. 
-   SQL Server로 가져오거나 SQL Server에서 내보내는 경우 [SSMS(SQL Server Management Studio)](#startSSMS)를 참조하세요.
-   SQL Server로 가져오거나 SQL Server에서 내보내는 경우 [SSDT(SQL Server Data Tools)가 포함된 Visual Studio](#startVS)를 참조하세요.

## <a name="prerequisite---is-the-wizard-installed-on-your-computer"></a>필수 구성 요소 - 컴퓨터에 마법사가 설치되어 있습니까?
마법사를 실행하려고 하지만 컴퓨터에 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 설치되지 않은 경우 SSDT(SQL Server Data Tools)를 설치하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사를 설치할 수 있습니다. 자세한 내용은 [SSDT(SQL Server Data Tools) 다운로드](https://msdn.microsoft.com/library/mt204009.aspx)를 참조하세요.

> [!NOTE]
> 64비트 버전의 SQL Server 가져오기 및 내보내기 마법사를 사용하려면 SQL Server를 설치해야 합니다. SSDT(SQL Server Data Tools) 및 SSMS(SQL Server Management Studio)는 32비트 애플리케이션이며, 32비트 버전의 마법사를 포함하여 32비트 파일만 설치합니다.

## <a name="startStart"></a> 시작 메뉴  
### <a name="start-the-sql-server-import-and-export-wizard-from-the-start-menu"></a>시작 메뉴에서 SQL Server 가져오기 및 내보내기 마법사 시작
1.  **시작** 메뉴에서 **Microsoft SQL Server 2016**을 찾아 펼칩니다.
3.  다음 옵션 중 하나를 클릭합니다.
  
    -   **SQL Server 2016 데이터 가져오기 및 내보내기(64비트)**
          
    -   **SQL Server 2016 데이터 가져오기 및 내보내기(32비트)**  
  
    데이터 원본에 32비트 데이터 공급자가 필요한 것을 알고 있는 경우가 아니면 64비트 버전의 마법사를 실행합니다.
 
    ![마법사 시작 시작](../../integration-services/import-export-data/media/start-wizard-start.jpg)
  
## <a name="startCmd"></a> Command prompt
### <a name="start-the-sql-server-import-and-export-wizard-from-the-command-prompt"></a>명령 프롬프트에서 SQL Server 가져오기 및 내보내기 마법사 시작  
명령 프롬프트 창의 다음 위치 중 하나에서 **DTSWizard.exe** 를 실행합니다.  
  
-   **C:\Program Files\Microsoft SQL Server\130\DTS\Binn** (64비트 버전)  
  
-   **C:\Program Files (x86)\Microsoft SQL Server\130\DTS\Binn** (32비트 버전)  
  
데이터 원본에 32비트 데이터 공급자가 필요한 것을 알고 있는 경우가 아니면 64비트 버전의 마법사를 실행합니다.

![마법사 시작 cmd](../../integration-services/import-export-data/media/start-wizard-cmd.jpg)  
  
## <a name="startSSMS"></a> SSMS(SQL Server Management Studio)
### <a name="start-the-sql-server-import-and-export-wizard-from-sql-server-management-studio-ssms"></a>SSMS(SQL Server Management Studio)에서 SQL Server 가져오기 및 내보내기 마법사 시작    
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.
    
2.  **데이터베이스**를 확장합니다.
3.  데이터베이스를 마우스 오른쪽 단추로 클릭합니다.
4.  **태스크**를 가리킵니다.
5.  다음 옵션 중 하나를 클릭합니다.
  
    -   **데이터 가져오기**
      
    -   **데이터 내보내기**  

    ![마법사 시작 SSMS](../../integration-services/import-export-data/media/start-wizard-ssms.jpg) 

SQL Server가 설치되어 있지 않거나 SQL Server가 있지만 SQL Server Management Studio가 설치되어 있지 않은 경우 [SSMS(SQL Server Management Studio) 다운로드](../../ssms/download-sql-server-management-studio-ssms.md)를 참조하세요.
  
## <a name="startVS"></a> Visual Studio
### <a name="start-the-sql-server-import-and-export-wizard-from-visual-studio-with-sql-server-data-tools-ssdt"></a>SSDT(SQL Server Data Tools)를 사용하여 Visual Studio에서 SQL Server 가져오기 및 내보내기 마법사 시작 
 Visual Studio( [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]포함)에서 Integration Services 프로젝트를 열고 다음 중 하나를 수행합니다. 
  
-   **프로젝트** 메뉴에서 **SSIS가져오기 및 내보내기 마법사**를 클릭합니다. 

    ![마법사 시작 프로젝트](../../integration-services/import-export-data/media/start-wizard-project.jpg) 
    
    \- 또는 -
    
-   솔루션 탐색기에서 **SSIS 패키지** 폴더를 마우스 오른쪽 단추로 클릭한 다음 **SSIS 가져오기 및 내보내기 마법사**를 클릭합니다.

    ![마법사 시작 패키지](../../integration-services/import-export-data/media/start-wizard-packages.jpg)

Visual Studio가 설치되어 있지 않거나 Visual Studio가 있지만 SQL Server Data Tools가 설치되어 있지 않은 경우 [SSDT(SQL Server Data Tools) 다운로드](../../ssdt/download-sql-server-data-tools-ssdt.md)를 참조하세요.

## <a name="get-the-wizard"></a>마법사 가져오기
마법사를 실행하려고 하지만 컴퓨터에 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 설치되지 않은 경우 SSDT(SQL Server Data Tools)를 설치하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사를 설치할 수 있습니다. 자세한 내용은 [SSDT(SQL Server Data Tools) 다운로드](https://msdn.microsoft.com/library/mt204009.aspx)를 참조하세요.

## <a name="get-help-while-the-wizard-is-running"></a>마법사를 실행하는 동안 도움말 보기
> [!TIP]
> 마법사의 모든 페이지 또는 대화 상자에서 F1 키를 누르면 현재 페이지에 대한 설명서를 볼 수 있습니다.   

 ## <a name="whats-next"></a>다음 단계  
 마법사를 시작할 때 첫 번째 페이지는 **SQL Server 가져오기 및 내보내기 마법사 시작**입니다. 이 페이지에서는 어떤 작업도 수행할 필요가 없습니다. 자세한 내용은 [SQL Server 가져오기 및 내보내기 마법사 시작](../../integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md)을 참조하세요.  
  
## <a name="related"></a> 관련 태스크 및 콘텐츠  
 다음은 몇 가지 다른 기본 작업입니다.
-   **마법사의 작동 원리에 대한 빠른 예제를 참조하세요.**

    -   **스크린샷을 보려면.** 단일 페이지([가져오기 및 내보내기 마법사의 간단한 예제 시작](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md))에서 간단한 종단 간 예제를 살펴봅니다.

    -   **비디오를 시청하려면.** 마법사를 보여 주고 Excel로 데이터를 내보내는 방법을 명료하고 간단하게 설명하는 4분 길이의 YouTube 동영상([SQL Server 가져오기 및 내보내기 마법사를 사용하여 Excel로 내보내기](https://go.microsoft.com/fwlink/?linkid=829049))을 시청합니다.

-   **마법사의 작동 원리에 대해 자세히 알아보기.**

    -   **마법사에 대해 자세히 알아보기.** 마법사에 대한 개요를 살펴보려면 [SQL Server 가져오기 및 내보내기 마법사를 사용하여 데이터 가져오기 및 내보내기](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)를 참조하세요.

    -   **마법사의 단계에 대해 자세히 알아보기** - 마법사의 단계에 대한 정보를 찾으려면 [SQL Server 가져오기 및 내보내기 마법사의 단계](../../integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard.md)를 참조하세요. 또한 마법사의 각 페이지마다 별도의 설명서 페이지가 있습니다.

    -   **데이터 원본 및 대상에 연결하는 방법에 대해 자세히 알아보기** - 데이터에 연결하는 방법에 대한 정보를 찾으려면 [SQL Server 가져오기 및 내보내기 마법사를 사용하여 데이터 원본에 연결](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md)의 목록에서 원하는 페이지를 선택하세요. 일반적으로 사용되는 몇 가지 데이터 원본마다 별도의 설명서 페이지가 있습니다.


