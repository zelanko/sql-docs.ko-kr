---
title: Dqsinstaller.exe를 실행 하 여 Data Quality 서버 설치 완료
description: Dqsinstaller.exe를 실행 하 여 DQS (SQL Server Data Quality Services 설치를 완료 하는 방법에 대해 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 7a8c96e0-1328-4f35-97fc-b6d9cb808bae
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 19805b5c5d41b5b39217c88cf565d9bd64c1ed9c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75558002"
---
# <a name="run-dqsinstallerexe-to-complete-data-quality-server-installation"></a>DQSInstaller.exe를 실행하여 Data Quality 서버 설치 완료

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  
  [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 설치를 완료하려면 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]를 설치한 후 DQSInstaller.exe 파일을 실행해야 합니다. 이 항목에서는 **시작** 화면, **시작** 메뉴, Windows 탐색기 또는 명령 프롬프트에서 DQSInstaller.exe를 실행하는 방법에 대해 설명합니다. DQSInstaller.exe 파일을 실행하기 위해 어떤 방법이나 선택할 수 있습니다.  
  
##  <a name="Prerequisites"></a> 필수 조건  
  
-   SQL Server를 설치하는 동안 SQL Server 설치 프로그램의 기능 선택 페이지에 있는 **데이터베이스 엔진 서비스** 에서 **Data Quality Services** 를 선택하고 SQL Server 설치를 완료해야 합니다. 자세한 내용은 [Install Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)을 참조하세요.  
  
-   Windows 사용자 계정은 SQL Server 데이터베이스 엔진 인스턴스에서 sysadmin 고정 서버 역할의 멤버여야 합니다.  
  
-   DQSInstaller.exe를 실행하는 컴퓨터에서 Administrators 그룹의 멤버로 로그온해야 합니다.  
  
##  <a name="WindowsExplorer"></a>시작 화면, 시작 메뉴 또는 Windows 탐색기에서 Dqsinstaller.exe를 실행 합니다.  
  
1.  
  [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]를 설치하려는 컴퓨터에서 다음 중 하나를 사용하여 DQSInstaller.exe 파일을 실행합니다.  
  
    -   **시작 화면**: **시작** 화면에서 **Data Quality 서버 설치 프로그램을 클릭 합니다.**  
  
    -   **시작 메뉴**: 작업 표시줄에서 **시작**을 클릭 하 고 **모든 프로그램**을 가리킨 다음 [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]을 클릭 합니다. 그런 다음 [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]에서 **Data Quality Services**와 **Data Quality 서버 설치 프로그램**을 차례로 클릭합니다.  
  
    -   **Windows 탐색기**: dqsinstaller.exe 파일을 찾습니다. SQL Server의 기본 인스턴스를 설치한 경우 DQSInstaller.exe 파일은 C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn에 있습니다. DQSInstaller.exe 파일을 두 번 클릭합니다.  
  
2.  설치 상태를 보여 주는 명령 프롬프트 창이 나타납니다. 다음 세 가지를 알 수 있습니다.  
  
    1.  설치 프로그램에서 DQSInstaller.exe 파일 실행 중 수행되는 동작들에 대한 정보가 포함된 설치 로그 파일인 DQS_install.log를 만듭니다. SQL Server의 기본 인스턴스를 설치한 경우 DQS_install.log 파일은 C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Log에 있습니다.  
  
    2.  설치 프로그램에서 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]설치를 위해 기본 서버 데이터 정렬 SQL_Latin1_General_CP1_CI_AS를 사용합니다.  
  
        > [!IMPORTANT]  
        >  명령 프롬프트에서 DQSInstaller.exe를 실행하는 경우에만 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 설치에 다른 서버 데이터 정렬 값을 제공할 수 있습니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [명령 프롬프트에서 DQSInstaller.exe 실행](#CommandPrompt) 을 참조하십시오.  
  
    3.  설치 프로그램에서는 컴퓨터에 최근 설치된 업데이트로 인해 컴퓨터에서 다시 시작이 보류 중인지 확인합니다. 보류 중인 다시 시작이 있는 경우 동일한 내용을 알리는 메시지가 나타나고 사용자는 Y를 눌러 계속하거나 N을 눌러 설치를 중단할 수 있습니다. 보류 중인 다시 시작이 있는 경우 설치를 중단하고 컴퓨터를 다시 시작한 다음 DQSInstaller.exe를 다시 실행하는 것이 좋습니다.  
  
3.  데이터베이스 마스터 키에 대한 암호를 입력하라는 메시지가 표시됩니다. 데이터베이스 마스터 키는 나중에 [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS)에서 참조 데이터 공급자를 설정할 때 DQS_MAIN 데이터베이스에 저장되는 참조 데이터 서비스 공급자 키를 암호화하기 위해 필요합니다.  
  
    > [!IMPORTANT]  
    >  암호는 8 자 이상 이어야 하며 다음 네 가지 범주 중 세 가지 문자를 포함 해야 합니다. 영어 대문자 (A, B, C,... Z), 영어 소문자 (a, b, c,... z), 숫자 (0, 1, 2,... 9) 및 영숫자가 아닌 문자 또는 특수 문자 (~! @ # $% ^& * () _-+ =\\ | {}[]:;"' <>,.? /). 예: P@ssword 현재 암호가 요구 사항을 따르지 않을 경우 설치 프로그램에서 다른 암호를 입력하라는 메시지가 표시됩니다.  
  
4.  암호를 제공하고, 다시 암호를 확인한 다음 Enter 키를 눌러 설치를 계속합니다.  
  
    > [!IMPORTANT]  
    >  데이터베이스 마스터 키에 지정된 암호는 이후 백업에서 DQS 데이터베이스를 복원하도록 선택할 경우에 필요하므로 보관해야 합니다. DQS 데이터베이스 복원 방법은 [Backing Up and Restoring DQS Databases](../../data-quality-services/backing-up-and-restoring-dqs-databases.md)을 참조하십시오.  
  
5.  MDS(Master Data Services) 데이터베이스가 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]와 같은 SQL Server 인스턴스에 있는 경우 설치 프로그램은 MDS(Master Data Services) 로그인에 매핑된 사용자를 만들고 DQS_MAIN 데이터베이스의 dqs_administrator 역할을 부여합니다. MDS(Master Data Services) 설치와 MDS(Master Data Services) 데이터베이스 만들기에 대한 자세한 내용은 [Install Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)를 참조하십시오.  
  
6.  설치가 성공적으로 완료되면 완료 메시지가 표시됩니다. 아무 키나 눌러 명령 프롬프트 창을 닫습니다.  
  
##  <a name="CommandPrompt"></a>명령 프롬프트에서 Dqsinstaller.exe를 실행 합니다.  
 다음 명령줄 매개 변수를 사용하여 명령 프롬프트에서 DQSInstaller.exe를 실행할 수 있습니다.  
  
|DQSInstaller.exe 매개 변수|Description|예제 구문|  
|--------------------------------|-----------------|-------------------|  
|-collation|
  [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]설치에 사용되는 서버 데이터 정렬입니다.<br /><br /> DQS는 대/소문자를 구분하지 않는 데이터 정렬만 지원합니다. 대/소문자를 구분하는 데이터 정렬을 지정하는 경우 설치 프로그램은 지정된 데이터 정렬의 대/소문자 구분 없는 버전을 사용하려고 합니다. 대/소문자 구분 없는 버전이 없거나 해당 데이터 정렬을 SQL에서 지원하지 않는 경우 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 설치가 실패합니다.<br /><br /> 서버 데이터 정렬이 지정되지 않는 경우 기본 데이터 정렬 SQL_Latin1_General_CP1_CI_AS가 사용됩니다.|`dqsinstaller.exe -collation <collation_name>`|  
|-upgradedlls|DQS 데이터베이스(DQS_MAIN, DQS_PROJECTS 및 DQS_STAGING_DATA)를 다시 만드는 것을 건너뛰고, [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 데이터베이스에서 DQS가 사용하는 SQLCLR(SQL 공용 언어 런타임) 어셈블리만 업데이트합니다.<br /><br /> 자세한 내용은 [.NET Framework 업데이트 후 SQLCLR 어셈블리 업그레이드](../../data-quality-services/install-windows/upgrade-sqlclr-assemblies-after-net-framework-update.md)를 참조하세요.|`dqsinstaller.exe -upgradedlls`|  
|-exportkbs|모든 기술 자료를 DQS 백업 파일(.dqsb)로 내보냅니다. 또한 모든 기술 자료를 내보내기 위해 사용하려는 전체 경로 및 파일 이름을 지정해야 합니다.<br /><br /> 자세한 내용은 [Dqsinstaller.exe를 사용하여 DQS 기술 자료 내보내기 및 가져오기](../../data-quality-services/install-windows/export-and-import-dqs-knowledge-bases-using-dqsinstaller-exe.md)을(를) 참조하세요.|`dqsinstaller.exe -exportkbs <path><filename>`<br /><br /> 예를 들어 `dqsinstaller.exe -exportkbs c:\DQSBackup.dqsb`|  
|-importkbs|
  [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 설치를 완료한 후 DQS 백업 파일(.dqsb)에서 모든 기술 자료를 가져옵니다. 또한 모든 기술 자료를 가져오기 위해 사용하려는 전체 경로 및 파일 이름을 지정해야 합니다.<br /><br /> 자세한 내용은 [Dqsinstaller.exe를 사용하여 DQS 기술 자료 내보내기 및 가져오기](../../data-quality-services/install-windows/export-and-import-dqs-knowledge-bases-using-dqsinstaller-exe.md)을(를) 참조하세요.|`dqsinstaller.exe -importkbs <path><filename>`<br /><br /> 예를 들어 `dqsinstaller.exe -importkbs c:\DQSBackup.dqsb`|  
|-upgrade|DQS 데이터베이스 스키마를 업그레이드합니다. 이전에 구성한 DQS 인스턴스에 SQL Server 업데이트를 설치한 후 이 매개 변수를 사용해야 합니다. 자세한 내용은 [SQL Server 업데이트 설치 후 DQS 데이터베이스 스키마 업그레이드](../../data-quality-services/install-windows/upgrade-dqs-databases-schema-after-installing-sql-server-update.md)을 참조하세요.|`dqsinstaller.exe -upgrade`|  
|-uninstall|현재 SQL Server 인스턴스에서 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 를 제거합니다.<br /><br /> 기존 Data Quality 서버 설치에 있는 모든 기술 자료를 DQS 백업 파일(.dqsb)로 내보낸 후 Data Quality 서버를 제거할 수 있습니다. 자세한 내용은 [Dqsinstaller.exe를 사용하여 DQS 기술 자료 내보내기 및 가져오기](../../data-quality-services/install-windows/export-and-import-dqs-knowledge-bases-using-dqsinstaller-exe.md)을(를) 참조하세요.<br /><br /> ** \* 중요 \* \* ** 명령줄 매개 변수 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 를 사용 하 여 SQL server 인스턴스에서를 제거 하는 경우 제거 프로세스의 일부로 모든 DQS 개체가 삭제 됩니다. `-uninstall` 
  [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] Data Quality 서버 개체 제거 [에서 설명한 대로](../../sql-server/install/remove-data-quality-server-objects.md)을 제거한 후 이를 수동으로 삭제할 필요가 없습니다.|**Data Quality 서버를 제거 하려면 다음을 수행 합니다.**<br /><br /> `dqsinstaller.exe -uninstall`<br /><br /> **모든 기술 자료를 파일로 내보낸 후 Data Quality 서버를 제거 하려면 다음을 수행 합니다.**<br /><br /> `dqsinstaller.exe -uninstall <path><filename>`<br /><br /> 예를 들어 `dqsinstaller.exe -uninstall c:\DQSBackup.dqsb`|  
  
 **명령 프롬프트에서 Dqsinstaller.exe를 실행 하려면 다음을 수행 합니다.**  
  
1.  명령 프롬프트를 시작합니다.  
  
2.  명령 프롬프트에서 디렉터리를 DQSInstaller.exe가 있는 위치로 변경합니다. SQL Server의 기본 인스턴스를 설치한 경우 DQSInstaller.exe 파일은 C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn에 있습니다.  
  
    ```  
    cd C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn  
    ```  
  
3.  명령 프롬프트에서 명령줄 매개 변수를 사용하거나 사용하지 않고 DQSInstaller.exe를 실행합니다.  
  
    -   **명령줄 매개 변수를 사용 하지 않는**경우:를 입력 `dqsinstaller.exe`한 다음 enter 키를 누릅니다.  
  
    -   **명령줄 매개 변수를 사용 하**는 경우: 위의 표에 설명 된 대로 필요한 명령을 입력 한 다음 enter 키를 누릅니다.  
  
4.  필요한 동작은 지정된 명령을 기반으로 수행됩니다. 명령줄 매개 변수를 사용하지 않고 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 를 설치하기로 한 경우 나머지 단계는 이전 섹션 [시작 화면, 시작 메뉴 또는 Windows 탐색기에서 DQSInstaller.exe 실행](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md#WindowsExplorer)의 2~6단계에 설명된 것과 같습니다.  
  
## <a name="next-steps"></a>다음 단계  
  
-   해당 작업 프로필에 따라 사용자에게 적합한 DQS 역할을 부여합니다. 
  [사용자에게 DQS 역할 부여](../../data-quality-services/install-windows/grant-dqs-roles-to-users.md)를 참조하세요.  
  
-   
  [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 가 원격으로 [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]에 액세스할 경우 이 컴퓨터에서 SQL Server 구성 관리자를 사용하여 TCP/IP 프로토콜을 사용하도록 설정합니다.  
  
-   DQS 작업을 위해 원본 데이터에 액세스할 수 있고 처리된 데이터를 데이터베이스 테이블로 내보낼 수 있는지 확인합니다. 
  [DQS 작업을 위해 데이터 액세스](../../data-quality-services/install-windows/access-data-for-the-dqs-operations.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Data Quality Services 설치](../../data-quality-services/install-windows/install-data-quality-services.md)   
 [.NET Framework 업데이트 후 SQLCLR 어셈블리 업그레이드](../../data-quality-services/install-windows/upgrade-sqlclr-assemblies-after-net-framework-update.md)   
 [Export and Import DQS Knowledge Bases Using DQSInstaller.exe](../../data-quality-services/install-windows/export-and-import-dqs-knowledge-bases-using-dqsinstaller-exe.md)  
  
  
