---
title: "관리 (SSIS 서비스) 패키지 | Microsoft Docs"
ms.custom: 
ms.date: 11/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.dtsserver.importpackage.f1
- sql13.dts.dtsserver.exportpackage.f1
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
caps.latest.revision: 59
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f5acdf3ae4f27685fce7aab56aab423044491ee1
ms.openlocfilehash: 51d6e32f04d470c7f4ddfc8d3c4b6d994e0bd764
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="package-management-ssis-service"></a>패키지 관리(SSIS 서비스)
  패키지 관리에 모니터링, 관리, 패키지 가져오기 및 내보내기에 포함 됩니다.  
 
 ## <a name="package-store"></a>패키지 저장소  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]패키지에 액세스 하기 위한 두 개의 최상위 폴더를 제공 합니다. 
 - **패키지 실행** 
 - **저장된 패키지**

 **실행 중인 패키지** 폴더에는 서버에서 현재 실행 중인 패키지가 나열됩니다. **저장된 패키지** 폴더에는 패키지 저장소에 저장된 패키지가 나열됩니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스에서는 이 폴더에 나열된 패키지만 관리합니다. 패키지 저장소는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스 구성 파일에 나열된 msdb 데이터베이스나 파일 시스템 폴더 중 하나 또는 둘 다로 구성될 수 있습니다. 이 구성 파일에는 관리할 msdb와 파일 시스템 폴더가 지정되어 있습니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스에서 관리하지 않는 파일 시스템의 다른 위치에 패키지가 저장되어 있을 수도 있습니다.  
  
 Msdb에 저장 된 패키지는 sysssispackages 테이블에 저장 됩니다. 패키지를 msdb에 저장 하면 논리적 폴더로 그룹화 할 수 있습니다. 논리적 폴더를 사용 하 여 유용 목적으로 하 여 패키지를 구성 하거나 sysssispackages 테이블에 대 한 패키지를 필터링 합니다. 에 새 논리적 폴더를 만들고 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]합니다. 기본적으로 msdb에 추가하는 논리적 폴더는 자동으로 패키지 저장소에 포함됩니다.  
  
 만들면 논리적 폴더는 msdb에서 sysssispackagefolders 테이블의 행으로 표현 됩니다. sysssispackagefolders의 folderid 및 parentfolderid 열은 폴더 계층 구조를 정의합니다. Msdb의 논리적 루트 폴더는 parentfolderid 열에 null 값을 가진 sysssispackagefolders의 행입니다. 자세한 내용은 참조 [sysssispackages &#40; Transact SQL &#41; ](../../relational-databases/system-tables/sysssispackages-transact-sql.md) 및 [sysssispackagefolders (Transact SQL &)](../../relational-databases/system-tables/sysssispackagefolders-transact-sql.md)합니다.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 열고 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에 연결하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스에서 관리하는 msdb 폴더가 저장된 패키지 폴더 내에 표시됩니다. 구성 파일에 루트 파일 시스템 폴더가 지정되어 있으면 저장된 패키지 폴더에는 파일 시스템의 해당 폴더와 모든 하위 폴더에 저장된 패키지도 나열됩니다.  
  
 모든 파일 시스템 폴더에 패키지를 저장할 수 있지만 해당 폴더를 패키지 저장소의 구성 파일에 있는 폴더 목록에 추가하지 않으면 **저장된 패키지** 폴더의 하위 폴더에 해당 패키지가 나열되지 않습니다. 구성 파일에 대한 자세한 내용은 [Integration Services 서비스&#40;SSIS 서비스&#41;](../../integration-services/service/integration-services-service-ssis-service.md)버전과의 호환성을 위한 서비스를 지원합니다.  
  
 **실행 중인 패키지** 폴더에는 하위 폴더가 없으므로 확장할 수 없습니다.  
  
 기본적으로 **저장된 패키지** 폴더에는 **파일 시스템** 및 **MSDB**라는 두 개의 하위 폴더가 있습니다. **파일 시스템** 폴더에는 파일 시스템에 저장된 패키지가 나열됩니다. 이러한 파일의 위치는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스의 구성 파일에서 지정합니다. 기본 폴더는 %Program Files%\Microsoft SQL Server\100\DTS에 있는 Packages입니다. **MSDB** 폴더에는 서버의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] msdb 데이터베이스에 저장된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 패키지가 나열됩니다. sysssispackages 테이블에는 msdb에 저장된 패키지가 포함됩니다.  
  
 패키지 저장소의 패키지 목록을 보려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 열고 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에 연결해야 합니다.  
  
## <a name="monitor-running-packages"></a>실행 중인 패키지 모니터링  
 **실행 중인 패키지** 폴더는 현재 실행 중인 패키지를 나열 합니다. **의** 요약 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]페이지에서 현재 패키지에 대한 정보를 보려면 **실행 중인 패키지** 폴더를 클릭합니다. **요약** 페이지에 실행 중인 패키지의 실행 시간과 같은 정보가 나열됩니다. 필요에 따라 최신 정보를 표시하려면 폴더의 내용을 새로 고칩니다.  
  
 **요약** 페이지에서 실행 중인 단일 패키지에 대한 정보를 보려면 해당 패키지를 클릭합니다. **요약** 페이지에 패키지의 버전 및 설명과 같은 정보가 표시됩니다.  
  
실행 중인 패키지 중지는 **실행 중인 패키지** 패키지를 마우스 오른쪽 단추로 클릭 한 다음 클릭 하 여 폴더 **중지**합니다.  
  
## <a name="view-packages-in-ssms"></a>SSMS에서 패키지 보기
    
 이 절차에서는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에 연결하고 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스에서 관리하는 패키지 목록을 보는 방법을 설명합니다.  
  
### <a name="to-connect-to-integration-services"></a>Integration Services에 연결하려면  
  
1.  **시작**을 클릭하고 **모든 프로그램**, **Microsoft SQL Server**를 차례로 가리킨 다음 **SQL Server Management Studio**를 클릭합니다.  
  
2.  **서버에 연결** 대화 상자의 **서버 유형** 목록에서 **Integration Services** 를 선택하고 **서버 이름** 상자에 서버 이름을 지정한 다음 **연결**을 클릭합니다.  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에 연결할 수 없으면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스가 실행되고 있지 않는 것일 수 있습니다. 이 서비스의 상태를 확인하려면 **시작**을 클릭하고 **모든 프로그램**, **Microsoft SQL Server**, **구성 도구**를 차례로 가리킨 다음 **SQL Server 구성 관리자**를 클릭합니다. 왼쪽 창에서 **SQL Server 서비스**를 클릭하고 오른쪽 창에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스를 찾습니다. 서비스가 실행되지 않았으면 서비스를 시작합니다.  
  
     [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]엽니다. 기본적으로 SQL Server Management Studio의 왼쪽 아래에는 개체 탐색기 창이 열립니다. 개체 탐색기가 열려 있지 않으면 **보기** 메뉴에서 **개체 탐색기** 를 클릭합니다.  
  
### <a name="to-view-the-packages-that-integration-services-service-manages"></a>Integration Services 서비스에서 관리하는 패키지를 보려면  
  
1.  개체 탐색기에서 저장된 패키지 폴더를 확장합니다.  
  
2.  저장된 패키지 하위 폴더를 확장하여 패키지를 표시합니다.  

## <a name="import-and-export-packages"></a>패키지 가져오기 및 내보내기
 
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb 데이터베이스의 sysssispackages 테이블 또는 파일 시스템에 패키지를 저장할 수 있습니다.  
  
 패키지 저장소는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스에서 모니터링 및 관리하는 논리 저장소이며 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스의 구성 파일에 지정된 msdb 데이터베이스 및 파일 시스템 폴더를 포함할 수 있습니다.  
  
 다음 유형의 저장소 간에 패키지를 가져오고 내보낼 수 있습니다.  
  
-   파일 시스템 내의 파일 시스템 폴더  
  
-   SSIS 패키지 저장소 내 폴더. 두 기본 폴더의 이름은 각각 File System 및 MSDB입니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb 데이터베이스  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]통해 패키지를 가져오고 내보낼 수 있으며 이렇게 하면 패키지의 위치 및 저장소 형식을 변경 합니다. 가져오기 및 내보내기 기능을 사용하여 파일 시스템, 패키지 저장소 또는 msdb 데이터베이스에 패키지를 추가할 수 있으며 하나의 저장소 형식에서 다른 저장소 형식으로 패키지를 복사할 수 있습니다. 예를 들어 msdb에 저장된 패키지를 파일 시스템으로 복사할 수 있으며 반대의 경우도 가능합니다.  
  
 **dtutil** 명령 프롬프트 유틸리티(dtutil.exe)를 사용하여 패키지를 다른 형식으로 복사할 수 있습니다. 자세한 내용은 [dtutil Utility](../../integration-services/dtutil-utility.md)를 참조하세요.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지는 다음과 같은 위치에서 가져오거나 내보낼 수 있습니다.  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스, 파일 시스템 또는 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 저장소에 저장된 패키지를 가져올 수 있습니다. 가져온 패키지는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 나 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 저장소의 폴더에 저장됩니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스, 파일 시스템 또는 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 저장소에 저장된 패키지를 다른 저장소 형식 또는 위치로 내보낼 수 있습니다.  
  
 그러나 버전이 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]간에 패키지를 가져오거나 내보내는 경우 다음과 같은 몇 가지 제한 사항이 있습니다.  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]인스턴스에서는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]인스턴스에서 패키지를 가져올 수만 있고 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]로 패키지를 내보낼 수는 없습니다.  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]인스턴스에서는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]인스턴스에서 패키지를 가져오거나 인스턴스로 패키지를 내보낼 수 없습니다.  
  
 다음 절차에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하여 패키지를 가져오거나 내보내는 방법에 대해 설명합니다.  
  
### <a name="to-import-a-package-by-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용하여 패키지 가져오려면  
  
1.  **시작**을 클릭하고 **Microsoft** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 가리킨 다음 **SQL Server Management Studio**를 클릭합니다.  
  
2.  **서버에 연결** 대화 상자에서 다음 옵션을 설정합니다.  
  
    -   **서버 유형** 상자에서 **Integration Services**를 선택합니다.  
  
    -   에 **서버 이름** 상자에 서버 이름을 제공 하거나 클릭  **\<더 찾아보기... >** 사용할 서버를 찾습니다.  
  
3.  개체 탐색기가 열려 있지 않으면 **보기** 메뉴에서 **개체 탐색기**를 클릭합니다.  
  
4.  개체 탐색기에서 **저장된 패키지** 폴더를 확장합니다.  
  
5.  하위 폴더를 확장하여 패키지를 가져오려는 폴더를 찾습니다.  
  
6.  폴더를 마우스 오른쪽 단추로 클릭하고 **패키지 가져오기**를 클릭한 다음 다음 중 하나를 수행합니다.  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에서 가져오려면 **SQL Server** 옵션을 선택한 후 서버를 지정하고 인증 모드를 선택합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 선택한 경우 사용자 이름과 암호를 제공합니다.  
  
         찾아보기 단추 **(…)**를 클릭하고 가져올 패키지를 선택한 후 **확인**을 클릭합니다.  
  
    -   파일 시스템에서 가져오려면 **파일 시스템** 옵션을 선택합니다.  
  
         찾아보기 단추 **(…)**를 클릭하고 가져올 패키지를 선택한 후 **열기**를 클릭합니다.  
  
    -   [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 저장소에서 가져오려면 **SSIS 패키지 저장소** 옵션을 선택하고 서버를 지정합니다.  
  
         찾아보기 단추 **(…)**를 클릭하고 가져올 패키지를 선택한 후 **확인**을 클릭합니다.  
  
7.  선택적으로 패키지 이름을 업데이트합니다.  
  
8.  패키지의 보호 수준을 업데이트하려면 찾아보기 단추 **(…)** 를 클릭하고 **패키지 보호 수준** 대화 상자를 사용하여 다른 보호 수준을 선택합니다. **암호로 중요한 데이터 암호화** 또는 **암호로 모든 데이터 암호화** 옵션을 선택한 경우 암호를 입력하고 확인합니다.  
  
9. **확인** 을 클릭하여 가져오기를 완료합니다.  
  
### <a name="to-export-a-package-by-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용하여 패키지 내보내려면  
  
1.  **시작**을 클릭하고 **Microsoft** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 가리킨 다음 **SQL Server Management Studio**를 클릭합니다.  
  
2.  **서버에 연결** 대화 상자에서 다음 옵션을 설정합니다.  
  
    -   **서버 유형** 상자에서 **Integration Services**를 선택합니다.  
  
    -   에 **서버 이름** 상자에 서버 이름을 제공 하거나 클릭  **\<더 찾아보기... >** 사용할 서버를 찾습니다.  
  
3.  개체 탐색기가 열려 있지 않으면 **보기** 메뉴에서 **개체 탐색기**를 클릭합니다.  
  
4.  개체 탐색기에서 **저장된 패키지** 폴더를 확장합니다.  
  
5.  하위 폴더를 확장하고 내보내려는 패키지를 찾습니다.  
  
6.  패키지를 마우스 오른쪽 단추로 클릭하고 **내보내기**를 클릭한 후 다음 중 하나를 수행합니다.  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 내보내려면 **SQL Server** 옵션을 선택한 후 서버를 지정하고 인증 모드를 선택합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 선택한 경우 사용자 이름과 암호를 제공합니다.  
  
         찾아보기 단추 **(…)**를 클릭하고 **SSIS 패키지** 폴더를 확장하여 패키지를 저장하려는 폴더를 찾습니다. 선택적으로 패키지의 기본 이름을 업데이트한 후 **확인**을 클릭합니다.  
  
    -   파일 시스템으로 내보내려면 **파일 시스템** 옵션을 선택합니다.  
  
         찾아보기 단추 **(…)** 를 클릭하여 패키지를 내보내려는 폴더를 찾고, 패키지 파일의 이름을 입력한 후 **저장**을 클릭합니다.  
  
    -   [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 저장소로 내보내려면 **SSIS 패키지 저장소** 옵션을 선택하고 서버를 지정합니다.  
  
         찾아보기 단추 **(…)**를 클릭하고 **SSIS 패키지** 폴더를 확장하여 패키지를 저장하려는 폴더를 선택합니다. 선택적으로 **패키지 이름** 입력란에 패키지의 새 이름을 입력합니다. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  패키지의 보호 수준을 업데이트하려면 찾아보기 단추 **(…)** 를 클릭하고 **패키지 보호 수준** 대화 상자를 사용하여 다른 보호 수준을 선택합니다. **암호로 중요한 데이터 암호화** 또는 **암호로 모든 데이터 암호화** 옵션을 선택한 경우 암호를 입력하고 확인합니다.  
  
8.  **확인** 을 클릭하여 내보내기를 완료합니다.  

## <a name="import-package-dialog-box-ui-reference"></a>패키지 가져오기 대화 상자 UI 참조
  **에서 사용 가능한** 패키지 가져오기 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]대화 상자를 사용하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 가져오고 해당 패키지의 보호 수준을 설정 또는 수정할 수 있습니다.  
  
### <a name="options"></a>옵션  
 **패키지 위치**  
 가져온 패키지를 저장할 저장소 위치 유형을 선택합니다. 사용할 수 있는 옵션은 다음과 같습니다.  
  
 **SQL Server**  
  
 **파일 시스템**  
  
 **SSIS 패키지 저장소**  
  
 **Server**  
 서버 이름을 입력하거나 목록에서 서버를 선택합니다.  
  
 **인증**  
 Windows 인증 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 선택합니다. 이 옵션은 저장소 위치가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인 경우에만 사용할 수 있습니다.  
  
> [!IMPORTANT]  
>  가능하면 Windows 인증을 사용하십시오.  
  
 **인증 유형**  
 인증 유형을 선택합니다.  
  
 **사용자 이름**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 경우 사용자 이름을 입력합니다.  
  
 **암호**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 경우 암호를 입력합니다.  
  
 **패키지 경로**  
 패키지 경로를 입력하거나 찾아보기 단추 **(...)** 를 클릭한 다음 패키지를 찾습니다.  
  
 **패키지 이름**  
 필요에 따라 패키지의 이름을 바꿉니다. 기본 이름은 가져올 패키지의 이름입니다.  
  
 **보호 수준**  
 찾아보기 단추 **(...)** 를 클릭한 다음 **패키지 보호 수준** 대화 상자에서 보호 수준을 업데이트합니다. 자세한 내용은 [패키지 및 프로젝트 보호 수준 대화 상자](../../integration-services/security/access-control-for-sensitive-data-in-packages.md#protection_dialog)를 참조하세요.  

## <a name="export-package-dialog-box-ui-reference"></a>패키지 내보내기 대화 상자 UI 참조
  **에서 사용 가능한** 패키지 내보내기 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]대화 상자를 사용하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 다른 위치로 내보내고 필요에 따라 패키지의 보호 수준을 수정할 수 있습니다.  
  
### <a name="options"></a>옵션  
 **패키지 위치**  
 패키지를 내보낼 저장소 유형을 선택합니다. 사용할 수 있는 옵션은 다음과 같습니다.  
  
 **SQL Server**  
  
 **파일 시스템**  
  
 **SSIS 패키지 저장소**  
  
 **Server**  
 서버 이름을 입력하거나 목록에서 서버를 선택합니다.  
  
 **인증**  
 Windows 인증 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 선택합니다. 이 옵션은 저장소 위치가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인 경우에만 사용할 수 있습니다.  
  
> [!IMPORTANT]  
>  가능하면 Windows 인증을 사용하십시오.  
  
 **인증 유형**  
 인증 유형을 선택합니다.  
  
 **사용자 이름**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 경우 사용자 이름을 입력합니다.  
  
 **암호**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 경우 암호를 입력합니다.  
  
 **패키지 경로**  
 패키지 경로를 입력하거나 찾아보기 단추 **(...)** 를 클릭한 다음 패키지를 저장할 폴더를 찾습니다.  
  
 **보호 수준**  
 찾아보기 단추 **(...)** 를 클릭한 다음 **패키지 보호 수준** 대화 상자에서 보호 수준을 업데이트합니다. 자세한 내용은 [패키지 및 프로젝트 보호 수준 대화 상자](../../integration-services/security/access-control-for-sensitive-data-in-packages.md#protection_dialog)를 참조하세요.  

## <a name="back-up-and-restore-packages"></a>백업 하 고 패키지를 복원
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지는 파일 시스템, msdb 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터베이스에 저장할 수 있습니다. msdb에 저장한 패키지는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업 및 복원 기능을 사용하여 백업하거나 복원할 수 있습니다.  
  
 msdb 데이터베이스 백업 및 복원에 대한 자세한 내용은 다음 항목을 클릭하세요.  
  
-   [SQL Server 데이터베이스 백업 및 복원](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
-   [시스템 데이터베이스 백업 및 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에는 패키지 관리에 사용할 수 있는 **dtutil** 명령 프롬프트 유틸리티(dtutil.exec)가 포함되어 있습니다. 자세한 내용은 [dtutil Utility](../../integration-services/dtutil-utility.md)를 참조하세요.  
  
### <a name="configuration-files"></a>구성 파일  
 패키지에 포함된 모든 구성 파일은 파일 시스템에 저장됩니다. msdb 데이터베이스를 백업할 때는 이러한 파일이 함께 백업되지 않으므로 msdb에 저장된 패키지의 보안을 설정하는 계획의 일부로 주기적으로 구성 파일을 백업해야 합니다. msdb 데이터베이스의 백업에 구성을 포함시키려면 파일 기반 구성 대신 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 유형 사용을 고려해야 합니다.  
  
### <a name="packages-stored-in-the-file-system"></a>파일 시스템에 저장된 패키지  
 파일 시스템에 저장한 패키지의 백업은 서버의 파일 시스템 백업 계획에 포함되어야 합니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스 구성 파일의 기본 이름은 MsDtsSrvr.ini.xml이며 서비스에서 모니터링하는 서버의 폴더를 나열합니다. 이러한 폴더는 백업해야 합니다. 또한 패키지를 서버의 다른 폴더에 저장할 수 있으며 이러한 폴더도 백업에 포함해야 합니다.  

## <a name="see-also"></a>관련 항목:  
 [Integration Services 서비스&#40;SSIS 서비스&#41;](../../integration-services/service/integration-services-service-ssis-service.md)  
  
  

