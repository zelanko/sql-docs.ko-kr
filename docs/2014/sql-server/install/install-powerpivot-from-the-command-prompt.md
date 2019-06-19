---
title: 명령 프롬프트에서 PowerPivot을 설치 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 7f1f2b28-c9f5-49ad-934b-02f2fa6b9328
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: e6da1b23bd23634e3edb8d92093cab6ce71a2783
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66094556"
---
# <a name="install-powerpivot-from-the-command-prompt"></a>명령 프롬프트에서 PowerPivot 설치
  명령줄에서 설치 프로그램을 실행하여 SQL Server SharePoint용 PowerPivot를 설치할 수 있습니다. 명령에 `/ROLE` 매개 변수를 포함하고 `/FEATURES` 매개 변수는 제외해야 합니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 SharePoint Server 2010 Enterprise Edition SP1(서비스 팩 1)이 설치되어 있어야 합니다.  
  
 Analysis Services를 프로비전하기 위해 도메인 계정을 사용해야 합니다.  
  
 컴퓨터가 SharePoint 팜과 동일한 도메인에 가입되어 있어야 합니다.  
  
##  <a name="Commands"></a> /ROLE 기반 설치 옵션  
 SharePoint용 PowerPivot 배포의 경우 `/ROLE` 매개 변수가 `/FEATURES` 매개 변수를 대신하여 사용됩니다. 유효한 값은 다음과 같습니다.  
  
-   `SPI_AS_ExistingFarm`  
  
-   `SPI_AS_NewFarm`  
  
 이 두 역할은 모두 SharePoint용 PowerPivot이 SharePoint 팜에서 실행될 수 있도록 하는 응용 프로그램, 구성 및 배포 파일을 설치합니다. 두 역할 중 하나를 지정하면 설치 프로그램이 SharePoint 통합에 필요한 하드웨어 및 소프트웨어 요구 사항을 확인합니다.  
  
 기존 팜 옵션은 SharePoint 팜이 이미 설치되어 있다고 가정합니다. 새 팜 옵션을; 새 팜을 만들어야 하는 것으로 가정 팜의 데이터베이스 서버로 데이터베이스 엔진 인스턴스를 사용할 수 있도록 명령줄 구문에서 데이터베이스 엔진 인스턴스의 추가 지원 합니다.  
  
 이전 릴리스와 달리 모든 서버 구성 태스크는 설치 후 태스크로 수행됩니다. 설치 및 구성 단계를 자동화하는 경우 PowerShell을 사용하여 서버를 구성할 수 있습니다. 자세한 내용은 [Windows PowerShell을 사용 하 여 PowerPivot 구성](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md)합니다.  
  
## <a name="example-commands"></a>예제 명령  
 다음 예제는 각 옵션의 사용법을 보여 줍니다. 예제 1 `SPI_AS_ExistingFarm`합니다.  
  
```  
Setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=install /ROLE=SPI_AS_ExistingFarm /INSTANCENAME=PowerPivot /INDICATEPROGRESS/ASSVCACCOUNT=<DomainName\UserName> /ASSVCPASSWORD=<StrongPassword> /ASSYSADMINACCOUNTS=<DomainName\UserName>   
```  
  
 예제 2는 `SPI_AS_NewFarm`을 보여 줍니다. 데이터베이스 엔진을 프로비전하기 위한 매개 변수가 포함되어 있음을 알 수 있습니다.  
  
```  
Setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=install /ROLE=SPI_AS_NewFarm /INSTANCENAME=PowerPivot /INDICATEPROGRESS/SQLSVCACCOUNT=<DomainName\UserName> /SQLSVCPASSWORD=<StrongPassword> /SQLSYSADMINACCOUNTS=<DomainName\UserName> /AGTSVCACCOUNT=<DomainName\UserName> /AGTSVCPASSWORD=<StrongPassword> /ASSVCACCOUNT=<DomainName\UserName> /ASSVCPASSWORD=<StrongPassword> /ASSYSADMINACCOUNTS=<DomainName\UserName>   
```  
  
##  <a name="Join"></a> 명령 구문 수정  
 다음 단계를 사용하여 예제 명령 구문을 수정할 수 있습니다.  
  
1.  다음 명령을 메모장에 복사합니다.  
  
    ```  
    Setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=install /ROLE=SPI_AS_ExistingFarm /INSTANCENAME=PowerPivot /INDICATEPROGRESS/ASSVCACCOUNT=<DomainName\UserName> /ASSVCPASSWORD=<StrongPassword> /ASSYSADMINACCOUNTS=<DomainName\UserName>   
    ```  
  
     `/q` 매개 변수가 설치 프로그램을 자동 모드에서 실행하며 사용자 인터페이스를 숨깁니다.  
  
     `/IAcceptSQLServerLicenseTerms`는 무인 설치에 대해 `/q` 또는 `/qs` 매개 변수를 지정하는 경우 필요합니다.  
  
     `/action` 매개 변수는 설치를 수행하도록 설치 프로그램에 지시합니다.  
  
     `/role` 매개 변수를 지정하면 SharePoint용 PowerPivot에 필요한 Analysis Services 프로그램 및 구성 파일이 설치됩니다. 이 역할 역시 기존 팜 연결 정보를 검색 및 사용하여 SharePoint 구성 데이터베이스에 액세스합니다. 이 매개 변수는 필수적 요소입니다. 설치할 구성 요소를 지정하려면 `/features` 매개 변수 대신 이 매개 변수를 사용합니다.  
  
     `/instancename` 매개 변수는 명명된 인스턴스로 'PowerPivot'을 지정합니다. 이 값은 하드 코딩되어 변경할 수 없으며, 교육용으로 명령에 지정되므로 서비스 설치 방법을 확인할 수 있습니다.  
  
     `/indicateprogress` 매개 변수를 사용하면 명령 프롬프트 창에서 진행률을 모니터링할 수 있습니다.  
  
2.  `PID` 매개 변수는 명령에서 생략되므로 Evaluation 버전이 설치됩니다. Enterprise 버전을 설치하려면 설치 명령에 PID를 추가하고 올바른 제품 키를 제공하십시오.  
  
    ```  
  
    /PID=<product key for an Enterprise installation>  
  
    ```  
  
3.  자리 표시자를 바꿉니다 \<도메인 \ 사용자 이름 > 및 \<StrongPassword > 유효한 사용자 계정 및 암호를 사용 하 여 합니다.  
  
     `/assvaccount` 하 고 **/assvcpassword** 매개 변수를 사용 하 여를 구성 합니다 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] 응용 프로그램 서버 인스턴스. 이들 자리 표시자는 올바른 계정 정보로 바꿉니다.  
  
     합니다 **/assysadminaccounts** SQL Server 설치 프로그램을 실행 하는 사용자의 id 매개 변수를 설정 해야 합니다. 시스템 관리자는 한 명 이상 지정해야 합니다. SQL Server 설치 프로그램은 기본 제공 관리자 그룹 멤버에 대해 자동 sysadmin 권한을 더 이상 부여하지 않습니다.  
  
4.  줄 바꿈을 제거합니다.  
  
5.  전체 명령을 선택 하 고 클릭 **복사** 편집 메뉴에서.  
  
6.  관리자 명령 프롬프트를 엽니다. 이 작업을 수행 하려면 **시작**, 명령 프롬프트를 마우스 오른쪽 단추로 **관리자 권한으로 실행**합니다.  
  
7.  SQL Server 설치 미디어가 포함된 드라이브 또는 공유 폴더로 이동합니다.  
  
8.  수정한 명령을 명령줄에 붙여 넣습니다. 이렇게 하려면 명령 프롬프트 창의 왼쪽된 위 모서리에 있는 아이콘을 가리킵니다 **편집할**를 클릭 하 고 **붙여넣기**합니다.  
  
9. 키를 눌러 **Enter** 명령을 실행 합니다. 설치가 완료될 때까지 기다립니다. 명령 프롬프트 창에서 설치 진행률을 모니터링할 수 있습니다.  
  
10. 설치를 확인하려면 \Program Files\SQL Server\120\Setup Bootstrap\Log의 summary.txt 파일을 확인하십시오. 서버가 오류 없이 설치된 경우 최종 결과는 "통과"여야 합니다.  
  
11. 서버를 구성합니다. 최소한 솔루션을 배포하고 서비스 응용 프로그램을 만들고 각 사이트 모음에 대해 기능을 사용하도록 설정해야 합니다. 자세한 내용은 [PowerPivot 구성 또는 복구 SharePoint 2010 용 &#40;PowerPivot 구성 도구&#41; ](../../../2014/analysis-services/configure-repair-powerpivot-sharepoint-2010.md) 하거나 [중앙 관리에서 PowerPivot 서버 관리 및 구성 ](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md).  
  
## <a name="see-also"></a>관련 항목  
 [PowerPivot 서비스 계정 구성](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md)   
 [SharePoint 2010용 PowerPivot 설치](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  
