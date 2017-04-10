---
title: "Start the SQL Server Import and Export Wizard | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SQL Server 가져오기 및 내보내기 마법사"
  - "SQL Server 가져오기 및 내보내기 마법사 시작"
  - "가져오기 및 내보내기 마법사"
  - "가져오기 및 내보내기 마법사 시작"
ms.assetid: 5fc4f6d1-1f6f-444e-9aeb-827f85e1c405
caps.latest.revision: 130
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 112
---
# Start the SQL Server Import and Export Wizard
다음 방법 중 하나로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사를 시작할 수 있습니다.
-   지원되는 데이터 원본을 가져오거나 내보내려면 [시작 메뉴](#startStart) 또는 [명령 프롬프트](#startCmd)에서 마법사를 시작합니다.
-   SQL Server로 가져오거나 SQL Server에서 내보내는 경우 [SSMS(SQL Server Management Studio)](#startSSMS)에서 마법사를 시작합니다.
-   SQL Server Integration Services 프로젝트를 연 경우 [SSDT(SQL Server Data Tools)가 포함된 Visual Studio](#startVS)에서 마법사를 시작합니다.

이 항목에서는 마법사를 **시작**하는 방법만 설명합니다.
-   마법사에 대한 개요를 살펴보려면 [SQL Server 가져오기 및 내보내기 마법사를 사용하여 데이터 가져오기 및 내보내기](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)를 참조하세요.
-   마법사의 단계에 대한 정보를 살펴보려면 콘텐츠 탐색 메뉴에서 원하는 페이지를 선택합니다. 마법사의 각 페이지에 대한 개별 설명서 페이지가 있습니다. 또는 마법사의 모든 페이지 또는 대화 상자에서 F1 키를 누르면 현재 페이지에 대한 설명서를 볼 수 있습니다.

**마법사를 가져옵니다.** 마법사를 실행하려고 하지만 컴퓨터에 [!INCLUDE[msCoName] (../Token/msCoName_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 설치되지 않은 경우 SSDT(SQL Server Data Tools)를 설치하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사를 설치할 수 있습니다. 자세한 내용은 [SSDT(SQL Server Data Tools) 다운로드](https://msdn.microsoft.com/library/mt204009.aspx)를 참조하세요.  

## <a name="a-namestartstarta-start-the-wizard-from-the-start-menu"></a><a name="startStart"></a> 시작 메뉴에서 마법사 시작  
1.  **시작** 메뉴에서 **모든 앱**을 클릭합니다.
2.  **Microsoft SQL Server 2016**을 찾아서 확장합니다.
3.  다음 옵션 중 하나를 클릭합니다.
  
    -   **SQL Server 2016 데이터 가져오기 및 내보내기(64비트)**
          
    -   **SQL Server 2016 데이터 가져오기 및 내보내기(32비트)**  
  
데이터 원본에 32비트 데이터 공급자가 필요한 것을 알고 있는 경우가 아니면 64비트 버전의 마법사를 실행합니다.
 
![마법사 시작 시작](../../integration-services/import-export-data/media/start-wizard-start.jpg)
  
## <a name="a-namestartcmda-start-the-wizard-from-the-command-prompt"></a><a name="startCmd"></a> 명령 프롬프트에서 마법사 시작  
명령 프롬프트 창의 다음 위치 중 하나에서 **DTSWizard.exe**를 실행합니다.  
  
-   **C:\Program Files\Microsoft SQL Server\130\DTS\Binn**(64비트 버전)  
  
-   **C:\Program Files (x86)\Microsoft SQL Server\130\DTS\Binn**(32비트 버전)  
  
데이터 원본에 32비트 데이터 공급자가 필요한 것을 알고 있는 경우가 아니면 64비트 버전의 마법사를 실행합니다.

![마법사 시작 cmd](../../integration-services/import-export-data/media/start-wizard-cmd.jpg)  
  
## <a name="a-namestartssmsa-start-the-wizard-from-sql-server-management-studio-ssms"></a><a name="startSSMS"></a> SSMS(SQL Server Management Studio)에서 마법사 시작  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 연결합니다.
2.  **데이터베이스**를 확장합니다.
3.  데이터베이스를 마우스 오른쪽 단추로 클릭합니다.
4.  **태스크**를 가리킵니다.
5.  다음 옵션 중 하나를 클릭합니다.
  
    -   **데이터 가져오기**
      
    -   **데이터 내보내기**  

![마법사 시작 SSMS](../../integration-services/import-export-data/media/start-wizard-ssms.jpg) 

SQL Server가 설치되어 있지 않거나 SQL Server가 있지만 SQL Server Management Studio가 설치되어 있지 않은 경우 [SSMS(SQL Server Management Studio) 다운로드](https://msdn.microsoft.com/library/mt238290.aspx)를 참조하세요.
    
## <a name="a-namestartvsa-start-the-wizard-from-visual-studio-with-sql-server-data-tools-ssdt"></a><a name="startVS"></a> SSDT(SQL Server Data Tools)가 포함된 Visual Studio에서 마법사 시작  
 Visual Studio([!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 포함)에서 Integration Services 프로젝트를 열고 다음 중 하나를 수행합니다.  
  
-   **프로젝트** 메뉴에서 **SSIS가져오기 및 내보내기 마법사**를 클릭합니다. 

    ![마법사 시작 프로젝트](../../integration-services/import-export-data/media/start-wizard-project.jpg) 
    
    \- 또는 -
    
-   솔루션 탐색기에서 **SSIS 패키지** 폴더를 마우스 오른쪽 단추로 클릭한 다음 **SSIS 가져오기 및 내보내기 마법사**를 클릭합니다.

    ![마법사 시작 패키지](../../integration-services/import-export-data/media/start-wizard-packages.jpg)

Visual Studio가 설치되어 있지 않거나 Visual Studio가 있지만 SQL Server Data Tools가 설치되어 있지 않은 경우 [SSDT(SQL Server Data Tools) 다운로드](https://msdn.microsoft.com/library/mt204009.aspx)를 참조하세요. 

## <a name="get-help-while-the-wizard-is-running"></a>마법사를 실행하는 동안 도움말 보기
> [!TIP] 마법사의 모든 페이지 또는 대화 상자에서 F1 키를 누르면 현재 페이지에 대한 설명서를 볼 수 있습니다.   

 ## <a name="whats-next"></a>다음 단계  
 마법사를 시작할 때 첫 번째 페이지는 **SQL Server 가져오기 및 내보내기 마법사 시작**입니다. 이 페이지에서는 어떤 작업도 수행할 필요가 없습니다. 자세한 내용은 [SQL Server 가져오기 및 내보내기 마법사 시작](../../integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md)을 참조하세요.  
  
  