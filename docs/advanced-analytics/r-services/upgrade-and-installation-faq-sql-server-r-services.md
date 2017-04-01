---
title: "업그레이드 및 설치 FAQ(SQL Server R Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 001e66b9-6c3f-41b3-81b7-46541e15f9ea
caps.latest.revision: 58
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 47
---
# 업그레이드 및 설치 FAQ(SQL Server R Services)
  이 항목에서는 설치에 대한 일반적인 질문과 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]의 미리 보기 릴리스 업그레이드에 대한 질문에 대한 대답을 제공합니다.  
  
 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]를 처음 설치하는 경우 [SQL Server R Services&#40;In-Database&#41; 설정](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)에 설명된 대로 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 R 구성 요소를 설정하는 절차를 따릅니다.  

   
## <a name="important-changes-from-pre-releae-versions"></a>시험판 버전에서의 중요한 변경 내용  
 시험판 버전의 SQL Server 2016을 설치했거나 SQL Server 2016 공개 릴리스 전에 게시된 설치 지침을 사용하는 경우 시험판과 RTM 버전 간에 설치 프로세스가 완전히 다르다는 것을 알아야 합니다. 이러한 변경 내용에는 SQL Server 설치 마법사에서 사용할 수 있는 옵션 및 설치 후 단계가 둘 다 포함됩니다. 
   
> [!WARNING] [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 시험판 버전의 새로운 설치는 더 이상 지원되지 않습니다. 최대한 빨리 업그레이드하는 것이 좋습니다.  
+ CTP3, CTP3.1, CTP3.2, RC0 또는 RC1에 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]를 설치한 경우 구성 후 설치 스크립트를 다시 실행하여 이전 버전의 R 구성 요소 및 R Services를 제거해야 합니다. 
+ 구성 후 설치 스크립트는 고객이 시험판 버전을 제거할 수 있도록 돕기 위해 제공됩니다.  최신 버전을 설치할 때는 스크립트를 실행하지 마세요.

## <a name="how-to-uninstall-previous-versions-of-r-services"></a>이전 버전의 R Services를 제거하는 방법

이전 버전의 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 및 관련된 R 구성 요소를 올바른 순서로 제거하는 것이 중요합니다.

### <a name="1-run-script-to-deregister-windows-user-group-and-components-before-uninstalling-previous-components"></a>1. 이전 구성 요소를 제거하기 전에 스크립트를 실행하여 Windows 사용자 그룹 및 구성 요소 등록을 취소합니다.
[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 시험판 버전을 설치한 경우 먼저 `/uninstall` 인수를 사용하여 `RegisteREext.exe` 스크립트를 실행해야 합니다.

이렇게 하면 이전 구성 요소의 등록이 취소되고 실행 패드와 연결된 Windows 사용자 그룹이 제거됩니다. 이렇게 하지 않으면 설치하는 새 인스턴스에 필요한 Windows 사용자 그룹을 만들 수 없습니다.
  
예를 들어 기본 인스턴스에 R Services를 설치한 경우 스크립트가 설치된 디렉터리에서 이 명령을 실행합니다.  
  
~~~~
    RegisterRExt.exe /UNINSTALL  
~~~~ 
  
명명된 인스턴스에 R Services를 설치한 경우 *INSTANCE:* 뒤에 인스턴스 이름을 지정합니다.  
  
~~~~ 
RegisterRExt.exe /UNINSTALL /INSTANCE:<instancename>   
~~~~  

모든 구성 요소를 제거하기 위해 스크립트를 두 번 이상 실행해야 할 수도 있습니다.

> [!NOTE]
> 이 스크립트의 기본 위치는 설치한 시험판 버전에 따라 다릅니다. 잘못된 버전의 스크립트를 실행하려고 하면 오류가 발생할 수도 있습니다. 
> 
>  + CTP 3.1, 3.2 또는 3.3이 있는 경우 구성 요소를 제거하려면 먼저 Microsoft 다운로드 센터에서 업데이트된 버전의 [설치 후 구성 스크립트](http://go.microsoft.com/fwlink/?LinkId=723194)를 다운로드해야 합니다. 업데이트된 스크립트는 이전 구성 요소의 등록 취소를 지원합니다. 링크를 클릭하고 **이름으로 저장** 을 선택하여 스크립트를 로컬 폴더에 저장합니다. 기존 스크립트의 이름을 바꾼 다음 스크립트를 실행할 폴더에 새 스크립트를 복사합니다. 
>  + RC0의 경우 올바른 스크립트 파일이 설치되었으며 `C:\Program Files\Microsoft\MRO-for-RRE\8.0\R-3.2.2\library\RevoScaleR\rxLibs\x64` 폴더에 있습니다.  
>  + 릴리스 버전(13.0.1601.5 이상)의 경우 구성 요소를 설치하거나 구성하는 데 스크립트가 필요하지 않습니다. 스크립트는 이전 구성 요소를 제거하는 용도로만 사용해야 합니다. 


### <a name="2-uninstall-any-older-versions-of-the-revolution-enterprise-tools-including-components-installed-with-ctp-releases"></a>2. CTP 릴리스와 함께 설치된 구성 요소를 포함하여 이전 버전의 Revolution Enterprise 도구를 모두 제거합니다.

R 구성 요소의 제거 순서가 중요합니다. 항상 [!INCLUDE[rsql_rre-noversion](../../includes/rsql-rre-noversion-md.md)]를 먼저 제거합니다. 그런 다음 [!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)]을 제거합니다.  

 실수로 R Open을 먼저 제거한 다음 Revolution R Enterprise를 제거하려고 할 때 오류가 발생한 경우, 한 가지 해결 방법은 Revolution R Open 또는 Microsoft R Open을 다시 설치한 다음 두 구성 요소를 정확한 순서로 제거하는 것입니다.  

### <a name="3-uninstall-any-other-version-of-microsoft-r-open"></a>3. 다른 버전의 Microsoft R Open을 모두 제거합니다.

마지막으로, 다른 버전의 Microsoft R Open을 모두 제거합니다.
 
### <a name="4-upgrade-sql-server"></a>4. SQL Server 업그레이드  
  
시험판 구성 요소가 모두 제거된 후 컴퓨터를 다시 시작합니다. 이 작업은 SQL Server 설치 요구 사항이며, 다시 시작이 완료될 때까지 업데이트된 설치를 진행할 수 없습니다.     

이 작업이 완료된 후 SQL Server 설치 프로그램을 실행하고 다음 지침에 따라 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]를 설치합니다. [SQL Server R Services 설정](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md).  
  
추가 구성 요소가 필요하지 않으며, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치에 의해 R 패키지 및 연결 패키지가 설치됩니다. 


## <a name="upgrading-r-components"></a>R 구성 요소 업그레이드

SQL Server 2016에 대한 핫픽스 또는 향상된 기능이 릴리스되면 인스턴스에 이미 R Services 기능이 포함되어 있는 경우 R 구성 요소도 업그레이드되거나 새로 고쳐집니다. 

그러나 인터넷에 연결되지 않은 서버를 업그레이드하거나 패치하는 경우 새로 고침을 시작하기 전에 업데이트된 버전의 R 구성 요소를 수동으로 다운로드해야 합니다. 자세한 내용은 [인터넷에 연결하지 않고 R 구성 요소 설치](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md)를 참조하세요.

## <a name="problems-uninstalling-older-versions-of-r"></a>이전 버전의 R을 제거하는 중 문제 발생  
이전 버전의 Revolution R Open 또는 Revolution R Enterprise가 제거 프로세스에서 완전히 제거되지 않는 경우도 있습니다.  
  
 이전 버전을 제거하는 데 문제가 있는 경우 레지스트리를 편집하여 관련 키를 제거할 수도 있습니다.  
  
 Windows 레지스트리를 열고 `HKLM\Software\Microsoft\Windows\CurrentVersion\Uninstall` 키를 찾습니다.  
  
 다음 항목이 있고 키에 단일 값 `sEstimatedSize2`만 포함되어 있는 경우 항목을 삭제합니다.  
  
-   E0B2C29E-B8FC-490B-A043-2CAE75634972        (8.0.2의 경우)  
  
-   46695879-954E-4072-9D32-1CC84D4158F4        (8.0.1의 경우)  
  
-   2DF16DF8-A2DB-4EC6-808B-CB5A302DA91B        (8.0.0의 경우)  
  
-   5A2A1571-B8CD-4AAF-9303-8DF463DABE5A        (7.5.0의 경우)  


## <a name="new-license-agreement-for-r-components-required-for-unattended-installs"></a>무인 설치에 필요한 R 구성 요소에 대한 새 사용권 계약  
 명령줄을 사용하여 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]가 이미 설치되어 있는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 인스턴스를 업그레이드하는 경우 명령줄을 수정하여 새 사용권 계약 매개 변수 */IACCEPTROPENLICENSEAGREEMENT*를 사용해야 합니다. 
 
 올바른 인수를 사용하지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치에 실패할 수 있습니다.  
  
## <a name="after-running-setup-includersqlproductnametokenrsqlproductnamemdmd-is-still-not-enabled"></a>설치 프로그램을 실행해도 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]를 사용할 수 없음  
 외부 스크립트 실행을 지원하는 기능은 설치된 경우에도 기본적으로 사용되지 않습니다. 이는 노출 영역 축소를 위해 의도된 것입니다.  
  
 R 스크립트를 사용하려면 관리자가 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 다음 문을 실행할 수 있습니다.  
  
1.  R을 사용하려는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 인스턴스에서 이 문을 실행합니다.  
  
    ```  
    sp_configure 'external scripts enabled',1 
    reconfigure with override  
    ```  
  
2.  인스턴스를 다시 시작합니다.  
  
3.  인스턴스가 다시 시작된 후 **SQL Server 구성 관리자** 또는 **서비스** 패널을 열고 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 서비스가 실행되고 있는지 확인합니다.  

> [!TIP] 미리 구성된 R Services 인스턴스를 설치하려면 R Services가 사용되는 엔터프라이즈 버전을 포함하는 Azure 가상 컴퓨터 이미지를 사용합니다. 자세한 내용은 [Azure 가상 컴퓨터에 설치 SQL Server R Services 설치](../../advanced-analytics/r-services/installing-sql-server-r-services-on-an-azure-virtual-machine.md)를 참조하세요.
 

## <a name="setup-of-includersqlproductnametokenrsqlproductnamemdmd-not-available-in-a-failover-cluster"></a>장애 조치(Failover) 클러스터에서 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 설치를 사용할 수 없음  
 현재, 장애 조치(Failover) 클러스터에는 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]를 설치할 수 없습니다.  
    
 그러나 Always On을 사용하고 가용성 그룹의 일부인 독립 실행형 컴퓨터에 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]를 설치할 수 있습니다. Always On 가용성 그룹에서 R Services를 사용하는 방법에 대한 자세한 내용은 [Always On 가용성 그룹: 상호 운용성](../../database-engine/availability-groups/windows/always-on-availability-groups-interoperability-sql-server.md)을 참조하세요.  

또 다른 옵션은 R 스크립트 실행을 위해 다른 SQL Server 인스턴스에 복제본을 설치하는 것입니다. 복제 또는 로그 전달을 사용하여 복제본을 만들 수 있습니다.
 
## <a name="launchpad-service-cannot-be-started"></a>실행 패드 서비스를 시작할 수 없음  

실행 패드가 시작되지 않도록 할 수 있는 몇 가지 문제가 있습니다.
+ **8dot3 표기법을 사용할 수 없음**.  R Services(In-Database)를 설치하려면 기능이 설치되어 있는 드라이브에서 **8dot3** 표기법을 사용하여 짧은 파일 이름을 만들 수 있도록 지원해야 합니다.  8.3 파일 이름은 짧은 파일 이름이라고도 하며, 이전 버전의 Microsoft Windows와 호환성을 위해 또는 긴 파일 이름에 대한 대체 파일 이름으로 사용됩니다. 

  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]를 설치하는 볼륨에서 짧은 파일 이름을 지원하지 않는 경우 SQL Server에서 R을 시작하는 프로세스에서 올바른 실행 파일을 찾지 못할 수 있으며 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]가 시작되지 않습니다.  
  
   해결 방법으로, SQL Server가 설치되고 R Services가 설치되어 있는 볼륨에서 8dot3 표기법을 사용해야 합니다. 그런 다음 R Services 구성 파일에서 작업 디렉터리의 짧은 이름을 제공해야 합니다. 

    1. 8dot3 표기법을 사용하려면 [fsutil 8dot3name](https://technet.microsoft.com/library/ff621566(v=ws.11).aspx)에 설명된 대로 *8dot3name* 인수를 사용하여 **fsutil** 유틸리티를 실행합니다.
    2. 8dot3 표기법을 사용하도록 설정한 후 RLauncher.config 파일을 엽니다. 기본 설치에서 RLauncher.config 파일은 C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn에 있습니다.
    3. WORKING_DIRECTORY의 속성을 기록해 둡니다.
    4. WORKING_DIRECTORY에 지정된 폴더의 짧은 파일 경로를 지정하는 *file* 인수와 함께 fsutil 유틸리티를 사용합니다.
    5. 구성 파일을 편집하여 WORKING_DIRECTORY의 짧은 이름을 사용합니다.   
     
또는 8dot3 표기법과 호환되는 경로를 가진 다른 디렉터리를 WORKING_DIRECTORY에 대해 지정할 수 있습니다.     
   
   > [!NOTE] 이 제한은 향후 릴리스에서 제거됩니다. 
 
+ **실행 패드를 실행하는 계정이 변경되었거나 필요한 권한이 제거되었습니다.** 기본적으로 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]는 시작 시 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 설치 프로그램에서 필요한 모든 권한이 있도록 구성된 NT Service\MSSQLLaunchpad 계정을 사용합니다.

  따라서 실행 패드에 다른 계정을 할당하거나 SQL Server 컴퓨터에서 권한이 정책에 의해 제거된 경우 계정에 필요한 권한이 없을 수 있으며 다음 오류가 표시될 수 있습니다. *ERROR_LOGON_TYPE_NOT_GRANTED 1385(0x569) 로그온 실패: 사용자는 이 컴퓨터에서는 요청된 로그온 유형을 허가받지 않았습니다. *

  새 서비스 계정에 필요한 권한을 부여하려면 **로컬 보안 정책** 응용 프로그램을 사용하고 다음 사용 권한을 포함하도록 계정의 사용 권한을 업데이트합니다.
  + 프로세스의 메모리 할당량 조정(SeIncreaseQuotaPrivilege)
  + 트래버스 검사 무시(SeChangeNotifyPrivilege)
  + 서비스로 로그온(SeServiceLogonRight)
  + 프로세스 수준 토큰 바꾸기(SeAssignPrimaryTokenPrivilege)

  SQL Server 서비스를 실행할 수 있는 권한에 대한 자세한 내용은 [Windows 서비스 계정 및 권한 구성](https://msdn.microsoft.com/library/ms143504.aspx#Windows)을 참조하세요.
  
## <a name="side-by-side-installation-not-supported"></a>나란히 설치할 수 없음  
 R의 다른 버전 또는 Revolution Analytics의 다른 릴리스를 사용한 병렬 설치를 만들지 마십시오.  

## <a name="offline-installation-of-r-components-for-localized-version-of-sql-server"></a>지역화된 버전의 SQL Server에 대한 R 구성 요소의 오프라인 설치 
인터넷 액세스가 없는 컴퓨터에 R Services를 설치하는 경우 두 가지 추가 단계를 수행해야 합니다. SQL Server 설치 프로그램을 실행하기 전에 R 구성 요소 설치 관리자를 로컬 폴더로 다운로드한 다음 설치 관리자 파일을 편집하여 올바른 언어가 설치되도록 해야 합니다. 

R 구성 요소에 사용되는 언어 식별자는 설치되는 SQL Server 설치 프로그램 언어와 같아야 합니다. 같지 않으면 **다음** 단추를 사용할 수 없으며 설치를 완료할 수 없습니다.

자세한 내용은 [인터넷에 연결하지 않고 R 구성 요소 설치](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md)를 참조하세요. 
  
## <a name="unable-to-launch-runtime-for-r-script"></a>R 스크립트에 대해 런타임을 시작할 수 없음
[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]는 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]에서 R 작업을 실행하는 데 사용하는 Windows 사용자 그룹을 만듭니다. 이 사용자 그룹이 Windows 통합 인증을 사용하는 원격 사용자를 대신하여 R을 실행하려면 R Services를 실행하는 인스턴스에 로그인할 수 있어야 합니다.
  
 R 사용자에 대한 Windows 그룹(**SQLRUsers**)에 이 권한이 없는 환경에서는 다음과 같은 오류가 표시될 수 있습니다.  
  
-   R 스크립트를 실행하려고 할 때  
  
     *'R' 스크립트에 대해 런타임을 시작할 수 없습니다. 'R' 런타임의 구성을 확인하세요.*  
  
     *외부 스크립트 오류가 발생했습니다. 런타임을 시작할 수 없습니다.*  
  
-   [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 서비스에 의해 생성되는 오류:  
  
     *시작 관리자 RLauncher.dll을 초기화하지 못했습니다.*  
  
     *등록된 시작 관리자 dll이 없습니다!*  
  
-   NT SERVICE\MSSQLLAUNCHPAD 계정에 로그인할 수 없음을 나타내는 보안 로그  
  
이 사용자 그룹에 필요한 사용 권한을 부여하는 방법에 대한 자세한 내용은 [SQL Server R Services 설정](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)을 참조하세요. 

> [!NOTE]
> 
> SQL 로그인을 사용하여 원격 워크스테이션에서 R 스크립트를 실행하는 경우에는 이 제한이 적용되지 않습니다. 

  
## <a name="remote-execution-via-odbc"></a>ODBC를 통한 원격 실행   
 데이터 과학 워크스테이션을 사용하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터에 연결하여 **RevoScaleR** 함수로 R 명령을 실행하는 경우 서버에 데이터를 기록하는 ODBC 호출을 사용할 때 오류가 발생할 수 있습니다. 
 
 이유는 이전 섹션에서 설명한 것과 같습니다. 시작 시 R Services는 R 작업 실행에 사용되는 작업자 계정 그룹을 만듭니다. 그러나 이러한 계정이 서버에 연결할 수 없는 경우 사용자 대신 ODBC 호출을 실행할 수 없습니다. 
 
 SQL 로그인 자격 증명은 R 클라이언트에서 차례로 SQL Server 인스턴스와 ODBC에 명시적으로 전달되기 때문에 SQL 로그인을 사용하여 원격 워크스테이션에서 R 스크립트를 실행하는 경우에는 이 제한이 적용되지 않습니다.
  
암시된 인증을 사용하려면 이 작업자 계정 그룹에 다음과 같은 사용 권한을 부여해야 합니다.  
    
1. R 코드를 실행할 인스턴스에서 관리자 권한으로 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 엽니다. 

2. 다음 스크립트를 실행합니다. 기본값, 컴퓨터 및 인스턴스 이름을 변경한 경우 사용자 그룹 이름을 편집해야 합니다.
    ```sql
    USE [master]
    GO
    
    CREATE LOGIN [computername\SQLRUserGroup] FROM WINDOWS WITH DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO  
    ```

[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] UI를 사용하여 이 작업을 수행하는 단계와 자세한 내용은 [SQL Server R Services 설정](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)을 참조하세요.

    
## <a name="errors-during-setup-because-r-components-cannot-be-installed"></a>R 구성 요소를 설치할 수 없으므로 설정 중 오류 발생  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램을 사용하여 R Services(In-Database)를 설치하는 경우 Microsoft R Open 사용 조건이 포함된 페이지에서 **동의**를 클릭하면 설치 프로그램이 구성 요소를 찾은 후 다른 구성 요소가 설치될 때 설치를 시작합니다. 그러나 다음과 같은 경우에는 구성 요소를 설치하지 못할 수 있습니다.  
  
-   오프라인 설치를 수행 중이며 구성 요소를 다운로드할 수 없는 경우.  
  
     [인터넷에 액세스하지 않고 R 구성 요소 설치](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md)  
  
-   업데이트를 확인하는 옵션을 사용 중이며 업데이트 서비스에서 올바른 버전의 구성 요소를 찾을 수 없어 오류가 반환되는 경우.  
  
  RC3에서 수정된 알려진 문제입니다.  
  
 
  
## <a name="upgrade-of-r-server-standalone-to-rc3-requires-uninstallation-using-the-rc2-setup-utility"></a>R 서버(독립 실행형)를 RC3으로 업그레이드하려면 RC2 설치 유틸리티를 사용하여 제거해야 합니다.
 Microsoft R Server(독립 실행형)는 처음에 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] RC2에서 제공되었습니다. RC3 버전의 Microsoft R Server로 업그레이드하려면 먼저 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] RC2 설치 프로그램을 사용해서 제거한 후 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] RC3 설치 프로그램을 사용해서 다시 설치해야 합니다.  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램을 사용해서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] RC2용 R 서버(독립 실행형)를 제거합니다.  
  
2.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]을 RC3으로 업그레이드하고 R Services(In-Database)를 설치하는 옵션을 선택합니다. 그러면 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 인스턴스가 RC3으로 업그레이드됩니다. 추가 구성은 필요하지 않습니다.  
  
3.  RC3용 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 설치 프로그램을 한 번 더 실행하여 Microsoft R Server(독립 실행형)를 설치합니다.  

RTM 버전의 Microsoft R Server로 업그레이드하는 경우에는 이 해결 방법이 필요하지 않습니다.

## <a name="see-also"></a>관련 항목:  
 [SQL Server R Services 시작](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)   
 [Microsoft R Server&#40;독립 실행형&#41; 시작](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)  
  
  