---
title: BACPAC 파일을 가져와 새 사용자 데이터베이스 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 01/31/2017
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb. importdac.results.f1
- sql13.swb.importdac.settings.f1
- sql13.swb.importdac.storagebrowser.f1
- sql13.swb.importdac.results.f1
- sql13.swb.importdac.progress.f1
- sql13.swb. importdac.summary.f1
- sql13.swb.importdac.summary.f1
- sql13.swb. importdac.progress.f1
- sql13.swb.importdac.welcome.f1
- sql13.swb. importdac.settings.f1
helpviewer_keywords:
- Data-tier application
- SQL Server DAC
- Migrate database
- DAC
ms.assetid: 736d8d9a-39f1-4bf8-b81f-2e56c134d12e
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2227cb838c52bf309373a6d67f4d006841e30a4f
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51673672"
---
# <a name="import-a-bacpac-file-to-create-a-new-user-database"></a>BACPAC 파일을 가져와 새 사용자 데이터베이스 만들기
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  DAC(데이터 계층 응용 프로그램) 파일(.bacpac 파일)을 가져와 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 새 인스턴스에 또는 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]에 원본 데이터베이스를 데이터와 함께 복사할 수 있습니다. 내보내기 및 가져오기 작업을 결합하여 인스턴스 간에 DAC나 데이터베이스를 마이그레이션하거나 논리 백업을 만들 수 있습니다. 예를 들어 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에 배포된 데이터베이스의 온-프레미스 복사본을 만들 수 있습니다.  
  
## <a name="before-you-begin"></a>시작하기 전 주의 사항  
 가져오기 프로세스에서는 새로운 DAC를 두 단계로 작성합니다.  
  
1.  DAC 배포 시 DAC 패키지 파일의 정의로부터 새로운 DAC가 만들어지는 것과 마찬가지로, 가져오기 프로세스에서는 내보내기 파일에 저장된 DAC 정의를 사용하여 새 DAC와 관련 데이터베이스가 만들어집니다.  
  
2.  내보내기 파일의 데이터에서 대량 복사본 가져오기  
  
## <a name="sql-server-utility"></a>SQL Server 유틸리티  
 DAC를 데이터베이스 엔진의 관리되는 인스턴스로 가져오는 경우 가져온 DAC는 유틸리티 컬렉션 집합이 다음에 인스턴스에서 유틸리티 제어 지점으로 전송될 때 SQL Server 유틸리티로 통합됩니다. DAC에 있게 됩니다는 **배포 된 데이터 계층 응용 프로그램** 의 노드는 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **유틸리티 탐색기** 에 보고 된 **배포 된 데이터 계층 응용 프로그램**세부 정보 페이지입니다.  
  
## <a name="database-options-and-settings"></a>데이터베이스 옵션 및 설정  
 기본적으로 가져오기 중에 만들어진 데이터베이스에는 CREATE DATABASE 문의 모든 기본 설정이 적용됩니다. 단, 데이터베이스 데이터 정렬 및 호환성 수준은 DAC 내보내기 파일에 정의된 값으로 설정됩니다. DAC 내보내기 파일은 원본 데이터베이스의 값을 사용합니다.  
  
 TRUSTWORTHY, DB_CHAINING 및 HONOR_BROKER_PRIORITY와 같은 일부 데이터베이스 옵션은 가져오기 프로세스 도중 조정할 수 없습니다. 파일 그룹의 수, 파일의 수 및 크기와 같은 물리적 속성은 가져오기 프로세스 도중 변경할 수 없습니다. 가져오기가 완료된 후 ALTER DATABASE 문, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell을 사용하여 데이터베이스를 맞춤 구성할 수 있습니다. 자세한 내용은 [Databases](../../relational-databases/databases/databases.md)를 참조하세요.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]SP4(서비스 팩 4) 이상을 실행하는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스 또는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 에만 DAC를 가져올 수 있습니다. 이후 버전에서 DAC를 내보내는 경우 DAC에 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 지원되지 않는 개체가 포함될 수 있습니다. 이러한 DAC를 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]인스턴스에 배포할 수 없습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 출처를 알 수 없거나 신뢰할 수 없는 DAC 내보내기 파일은 가져오지 않는 것이 좋습니다. 이러한 파일에 포함된 악성 코드가 의도하지 않은 Transact-SQL 코드를 실행하거나 스키마를 수정하여 오류가 발생할 수 있습니다. 출처를 알 수 없거나 신뢰할 수 없는 내보내기 파일을 사용하려면 먼저 DAC의 압축을 풀고 저장 프로시저 및 다른 사용자 정의 코드와 같은 코드를 검사하세요. 이러한 검사를 수행하는 방법은 [Validate a DAC Package](validate-a-dac-package.md)를 참조하세요.  
  
## <a name="security"></a>보안  
 보안을 개선하기 위해 SQL Server 인증 로그인은 암호 없이 DAC 내보내기 파일에 저장됩니다. 파일을 가져오면 생성된 암호와 함께 비활성 로그인이 생성됩니다. 로그인을 활성화하려면 ALTER ANY LOGIN 권한이 있는 로그인을 사용하여 로그인하고 ALTER LOGIN을 사용하여 로그인을 활성화하여 사용자에게 알려 줄 수 있는 새 암호를 할당합니다. Windows 인증 로그인의 경우 암호가 SQL Server에서 관리되지 않으므로 이 과정이 필요 없습니다.  
  
## <a name="permissions"></a>Permissions  
 **sysadmin** 또는 **serveradmin** 고정 서버 역할의 멤버를 통하거나 **dbcreator** 고정 서버 역할에 포함되고 ALTER ANY LOGIN 권한이 있는 로그인을 통해서만 DAC를 가져올 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sa **라는 기본 제공** 시스템 관리자 계정도 DAC를 가져올 수 있습니다. [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 에 대한 로그인이 있는 DAC를 가져오려면 loginmanager 또는 serveradmin 역할의 멤버 자격이 필요합니다. [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에 대한 로그인이 없는 DAC를 가져오려면 dbmanager 또는 serveradmin 역할의 멤버 자격이 필요합니다.  
  
## <a name="using-the-import-data-tier-application-wizard"></a>데이터 계층 응용 프로그램 가져오기 마법사 사용  
 **마법사를 시작하려면 다음 단계를 따르십시오.**  
  
1.  온-프레미스 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]인스턴스에 연결합니다.  
  
2.  **개체 탐색기**에서 **데이터베이스**를 마우스 오른쪽 단추로 클릭한 후 **데이터 계층 응용 프로그램 가져오기** 메뉴 항목을 선택하여 마법사를 시작합니다.  
  
3.  마법사 대화 상자를 완료합니다.  
  
    -   [소개 페이지](#Introduction)  
  
    -   [가져오기 설정 페이지](#Import_settings)  
  
    -   [데이터베이스 설정 페이지](#Database_settings)  
  
    -   [요약 페이지](#Summary)  
  
    -   [진행률 페이지](#Progress)  
  
    -   [결과 페이지](#Results)  
  
###  <a name="Introduction"></a> 소개 페이지  
 이 페이지에서는 데이터 계층 응용 프로그램 가져오기 마법사의 단계에 대해 설명합니다.  
  
 **옵션**  
  
-   **이 페이지를 다시 표시 안 함** - 앞으로 소개 페이지가 표시되지 않도록 하려면 이 확인란을 클릭합니다.  
  
-   **다음** - **가져오기 설정** 페이지로 진행합니다.  
  
-   **취소** - 작업을 취소하고 마법사를 닫습니다.  
  
###  <a name="Import_settings"></a> 가져오기 설정 페이지  
 이 페이지에서 가져올 .bacpac 파일의 위치를 지정할 수 있습니다.  
  
-   **로컬 디스크에서 가져오기** - **찾아보기...** 를 클릭하고 로컬 컴퓨터로 이동하거나 제공된 공간에 경로를 지정합니다. 경로 이름에 파일 이름과 .bacpac 확장명을 모두 포함해야 합니다.  
  
-   **Azure에서 가져오기** - Microsoft Azure 컨테이너에서 BACPAC 파일을 가져옵니다. 이 옵션의 유효성을 검사하려면 Microsoft Azure 컨테이너에 연결해야 합니다. 또한 이 옵션을 사용하려면 임시 파일을 보관할 로컬 디렉터리를 지정해야 합니다. 지정된 위치에 임시 파일이 만들어지고 작업이 완료될 때까지 해당 위치에 유지됩니다.  
  
     Azure를 검색할 때 단일 계정으로 컨테이너 간을 전환할 수 있습니다. 가져오기 작업을 계속하려면 단일 .bacpac 파일을 지정해야 합니다. **이름**, **크기**또는 **수정한 날짜**별로 열을 정렬할 수 있습니다.  
  
     계속하려면 가져올 .bacpac 파일을 지정하고 **열기**를 클릭합니다.  
  
###  <a name="Database_settings"></a> 데이터베이스 설정 페이지  
 이 페이지에서 만들려는 데이터베이스의 세부 정보를 지정할 수 있습니다.  
  
 **로컬 SQL Server 인스턴스의 경우**  
  
-   **새 데이터베이스 이름** – 가져올 데이터베이스의 이름을 지정합니다.  
  
-   **데이터 파일 경로** - 데이터 파일을 보관할 로컬 디렉터리를 지정합니다. **찾아보기…** 를 클릭합니다. 를 클릭하고 로컬 컴퓨터로 이동하거나 제공된 공간에 경로를 지정합니다.  
  
-   **로그 파일 경로** – 로그 파일을 저장할 로컬 디렉터리를 입력합니다. **찾아보기…** 를 클릭합니다. 를 클릭하고 로컬 컴퓨터로 이동하거나 제공된 공간에 경로를 지정합니다.  
  
 계속하려면 **다음**을 클릭합니다.  
  
 **Azure SQL Database:**  
  
 - **[BACPAC 파일을 가져와 새 Azure SQL Database를 만들기](https://azure.microsoft.com/documentation/articles/sql-database-import/)** 에서는 Azure Portal, PowerShell, SSMS 또는 SqlPackage를 사용하는 단계별 지침을 제공합니다.  
 - 다양한 서비스 계층을 자세히 살펴보려면 **[SQL Database 옵션 및 성능: 각 서비스 계층에서 제공되는 항목 이해](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)** 를 확인해 보세요.  

### <a name="validation-page"></a>유효성 검사 페이지  
 이 페이지에서 작업을 차단한 문제를 검토할 수 있습니다. 계속하려면 차단 문제를 해결하고 **유효성 검사 다시 실행** 을 클릭하여 유효성 검사에 성공했는지 확인합니다.  
  
 계속하려면 **다음**을 클릭합니다.  
  
###  <a name="Summary"></a> 요약 페이지  
 이 페이지에서 작업에 대해 지정한 원본 및 대상 설정을 검토할 수 있습니다. 지정한 설정을 사용하여 가져오기 작업을 완료하려면 **마침**을 클릭합니다. 가져오기 작업을 취소하고 마법사를 종료하려면 **취소**를 클릭합니다.  
  
###  <a name="Progress"></a> 진행률 페이지  
 이 페이지에는 작업 상태를 나타내는 진행률 표시줄이 표시됩니다. 자세한 상태를 보려면 **자세히 보기** 옵션을 클릭합니다.  
  
 계속하려면 **다음**을 클릭합니다.  
  
###  <a name="Results"></a> 결과 페이지  
 이 페이지에는 데이터베이스 가져오기 및 만들기 작업의 결과가 성공 또는 실패로 보고됩니다. 오류가 발생한 동작에는 모두 **결과** 열에 링크가 있습니다. 링크를 클릭하면 해당 동작의 오류에 대한 보고서가 표시됩니다.  
  
 **닫기** 를 클릭하여 마법사를 닫습니다.  
  
## <a name="see-also"></a>참고 항목  
[BACPAC 파일을 가져와 새 Azure SQL Database를 만들기](https://azure.microsoft.com/documentation/articles/sql-database-import/)  
 [데이터 계층 응용 프로그램](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [데이터 계층 응용 프로그램 내보내기](../../relational-databases/data-tier-applications/export-a-data-tier-application.md)  
  
  
