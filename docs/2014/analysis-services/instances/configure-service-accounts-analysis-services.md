---
title: 서비스 계정 (Analysis Services) 구성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- security [Analysis Services], logon accounts
- logon accounts [Analysis Services]
- accounts [Analysis Services]
- logon accounts [Analysis Services], about logon accounts
ms.assetid: b481bd51-e077-42f6-8598-ce08c1a38716
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8dfde906f7cadc01b9c7a4abbe32be1bd0408986
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66080184"
---
# <a name="configure-service-accounts-analysis-services"></a>서비스 계정 구성(Analysis Services)
  제품 전체의 계정 프로비전은 [Windows 서비스 계정 및 권한 구성](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)에 자세히 설명되어 있으며, 이 항목에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 비롯한 모든 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]서비스에 대한 포괄적인 서비스 계정 정보를 제공합니다. 올바른 계정 유형, 설치 프로그램에서 할당한 Windows 권한, 파일 시스템 권한, 레지스트리 권한 등에 대한 자세한 내용은 이 항목을 참조하세요.  
  
 이 항목에서는 테이블 형식 및 클러스터형 설치에 필요한 추가 사용 권한을 비롯하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 대한 추가 정보를 제공합니다. 또한 서버 작업을 지원하는 데 필요한 사용 권한도 다룹니다. 예를 들어 처리 및 쿼리 작업이 서비스 계정에서 실행되도록 구성할 수 있습니다. 이렇게 하려면 추가 사용 권한을 부여해야 합니다.  
  
-   [Analysis Services에 할당된 Windows 권한](#bkmk_winpriv)  
  
-   [Analysis Services에 할당된 파일 시스템 권한](#bkmk_FilePermissions)  
  
-   [특정 서버 작업에 대한 추가 권한 부여](#bkmk_tasks)  
  
 추가 구성 단계는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스 및 서비스 계정의 SPN(서비스 사용자 이름)을 등록하는 단계이며, 여기서는 설명하지 않습니다. 이 단계에서는 이중 홉 시나리오로 클라이언트 애플리케이션에서 백 엔드 데이터 원본으로 통과 인증을 사용합니다. 이 단계는 Kerberos 제한 위임에 대해 구성된 서비스에만 적용됩니다. 자세한 내용은 [Configure Analysis Services for Kerberos constrained delegation](configure-analysis-services-for-kerberos-constrained-delegation.md) 을 참조하세요.  
  
## <a name="logon-account-recommendations"></a>로그온 계정 권장 사항  
 장애 조치(failover) 클러스터에서 Analysis Services의 모든 인스턴스는 Windows 도메인 사용자 계정을 사용하도록 구성되어야 합니다. 모든 인스턴스에 동일한 계정을 할당합니다. 자세한 내용은 [Analysis Services를 클러스터링하는 방법](https://msdn.microsoft.com/library/dn736073.aspx) 을 참조하세요.  
  
 독립 실행형 인스턴스는 기본 가상 계정 **NT Service\MSSQLServerOLAPService** (기본 인스턴스의 경우) 또는 **NT Service\MSOLAP$** _instance-name_ (명명된 인스턴스의 경우)을 사용해야 합니다. 이 권장 사항은 운영 체제가 Windows Server 2008 R2 이상이고 SQL Server 2012 이상의 Analysis Services가 실행된다고 가정할 때 모든 서버 모드의 Analysis Services 인스턴스에 적용됩니다.  
  
## <a name="granting-permissions-to-analysis-services"></a>Analysis Services에 권한 부여  
 이 섹션에서는 Analysis Services에서 로컬 내부 작업(예: 실행 파일 시작, 구성 파일 읽기, 데이터 디렉터리에서 데이터베이스 로드)을 수행하는 데 필요한 권한에 대해 설명합니다. 외부 데이터 액세스를 위한 권한 설정 방법과 다른 서비스 및 애플리케이션과의 상호 운용성에 대한 지침은 이 항목의 뒤에 나오는 [특정 서버 작업에 대한 추가 권한 부여](#bkmk_tasks) 를 참조하세요.  
  
 내부 작업의 경우 Analysis Services의 권한 소유자가 로그인 계정이 아니고 서비스별 SID를 포함하는 설치 프로그램에서 생성된 로컬 Windows 보안 그룹입니다. 보안 그룹에 권한을 할당하는 방법은 이전 버전의 Analysis Services와 일치합니다. 또한 로그온 계정은 시간에 따라 변경될 수 있지만 서비스별 SID와 로컬 보안 그룹은 서버 설치 수명 기간 동안 지속됩니다. Analysis Services에서는 권한 보유를 위해 로그온 계정 대신 보안 그룹을 선택하는 것이 좋습니다. 파일 시스템 권한 또는 Windows 권한에 상관없이 서비스 인스턴스에 수동으로 권한을 부여할 경우 항상 서버 인스턴스에 대해 만들어진 로컬 보안 그룹에 권한을 부여해야 합니다.  
  
 보안 그룹의 이름은 패턴을 따릅니다. 접두사는 항상 `SQLServerMSASUser$`이고 그 뒤에 컴퓨터 이름이 오고 마지막에 인스턴스 이름이 옵니다. 기본 인스턴스는 `MSSQLSERVER`입니다. 명명된 인스턴스는 설정 중에 지정된 이름입니다.  
  
 로컬 보안 설정에서 이 보안 그룹을 확인할 수 있습니다.  
  
-   Compmgmt.msc 실행 | **로컬 사용자 및 그룹** | **그룹** | `SQLServerMSASUser$`\<서버 이름 >`$MSSQLSERVER` (기본 인스턴스의 경우)에 대 한 합니다.  
  
-   구성원을 볼 보안 그룹을 두 번 클릭합니다.  
  
 그룹의 유일한 구성원은 서비스별 SID입니다. 오른쪽에 로그온 계정이 있습니다. 로그온 계정 이름은 cosmetic이고, 서비스별 SID에 컨텍스트를 제공합니다. 이후에 로그온 계정을 변경한 다음 이 페이지로 돌아가면 보안 그룹과 서비스별 SID는 변경되지 않고 로그온 계정 레이블이 다른 것을 알 수 있습니다.  
  
##  <a name="bkmk_winpriv"></a> Analysis Services 서비스 계정에 할당된 Windows 권한  
 Analysis Services는 서비스를 시작하고 시스템 리소스를 요청하는 데 운영 체제의 사용 권한이 필요합니다. 서버 모드 및 인스턴스가 클러스터링되었는지 여부에 따라 요구 사항이 다릅니다. Windows 권한에 익숙하지 않은 경우 자세한 내용은 [권한](https://msdn.microsoft.com/library/windows/desktop/aa379306\(v=vs.85\).aspx) 및 [권한 상수(Windows)](/windows/desktop/SecAuthZ/privilege-constants) 를 참조하세요.  
  
 Analysis Services의 모든 인스턴스에는 **서비스로 로그온** (SeServiceLogonRight) 권한이 필요합니다. SQL Server 설치 프로그램에서 설치 중 지정된 서비스 계정에 이 권한을 자동으로 할당합니다. 다차원 및 데이터 마이닝 모드에서 실행되는 서버의 경우 이 권한이 Analysis Services 서비스 계정에서 독립 실행형 서버 설치에 필요한 유일한 Windows 권한이며, 이 권한이 설치 프로그램에서 Analysis Services에 대해 구성하는 유일한 권한입니다. 클러스터형 및 테이블 형식 인스턴스의 경우 추가 Windows 권한을 수동으로 추가해야 합니다.  
  
 장애 조치(Failover) 클러스터 인스턴스는 테이블 형식 또는 다차원 모드에서 **예약 우선 순위 높임** (SeIncreaseBasePriorityPrivilege) 권한을 가져야 합니다.  
  
 테이블 형식 인스턴스는 인스턴스가 설치된 이후에 수동으로 부여해야 하는 다음과 같은 세 가지 추가 권한을 사용합니다.  
  
|||  
|-|-|  
|**프로세스 작업 집합 향상** (SeIncreaseWorkingSetPrivilege)|이 권한은 기본적으로 **사용자** 보안 그룹을 통해 모든 사용자가 사용할 수 있습니다. 이 그룹의 권한을 제거하여 서버를 잠근 경우 Analysis Services가 다음 오류를 로깅하며 시작하지 못할 수 있습니다. 오류: "클라이언트에 필수 권한이 없습니다." 이 오류가 발생하는 경우 해당 Analysis Services 보안 그룹에 권한을 부여하여 Analysis Services에 대한 권한을 복원합니다.|  
|**프로세스에 대한 메모리 할당량 조정** (SeIncreaseQuotaSizePrivilege)|이 권한은 프로세스가 실행을 완료하기에 충분한 리소스를 보유하지 못한 경우 인스턴스용으로 설정된 메모리 임계값에 따라 추가 메모리를 요청하는 데 사용됩니다.|  
|**메모리의 페이지 잠금** (SeLockMemoryPrivilege)|이 권한은 페이징이 완전히 해제된 경우에만 필요합니다. 기본적으로 테이블 형식 서버 인스턴스는 Windows 페이징 파일을 사용하지만 `VertiPaqPagingPolicy`를 0으로 설정하면 해당 인스턴스의 Windows 페이징 사용을 방지할 수 있습니다.<br /><br /> `VertiPaqPagingPolicy`를 1(기본값)로 설정하면 테이블 형식 서버 인스턴스가 Windows 페이징 파일을 사용합니다. 할당은 잠기지 않으므로 필요에 따라 Windows에서 페이지 아웃할 수 있습니다. 페이징을 사용하기 때문에 메모리에서 페이지를 잠글 필요가 없습니다. 기본 구성에 따라서 (여기서 `VertiPaqPagingPolicy` = 1), 부여할 필요가 없습니다 합니다 **메모리의 페이지 잠금** 테이블 형식 인스턴스에 대 한 권한.<br /><br /> `VertiPaqPagingPolicy` 0. Analysis Services에 대한 페이징을 해제한 경우 할당이 잠기며, **메모리의 페이지 잠금** 권한이 테이블 형식 인스턴스에 부여된 것으로 가정합니다. 이 설정 및 **메모리의 페이지 잠금** 권한이 지정된 경우 시스템의 메모리가 부족할 때 Analysis Services에 할당된 메모리를 Windows에서 페이지 아웃할 수 없습니다. Analysis Services는 합니다 **메모리의 페이지 잠금** 권한을 적용 `VertiPaqPagingPolicy` = 0. Windows 페이징을 해제하지 않는 것이 좋습니다. 페이징을 해제하면 페이징이 허용된 경우에 제대로 수행될 수도 있는 작업의 메모리 부족 오류 비율이 증가합니다. 참조 [Memory Properties](../server-properties/memory-properties.md) 에 대 한 자세한 내용은 `VertiPaqPagingPolicy`합니다.|  
  
#### <a name="to-view-or-add-windows-privileges-on-the-service-account"></a>서비스 계정에서 Windows 권한을 보거나 추가하려면  
  
1.  GPEDIT.msc | 로컬 컴퓨터 정책 | 컴퓨터 구성 | Windows 설정 | 보안 설정 | 로컬 정책 | 사용자 권한 지정을 실행합니다.  
  
2.  포함 된 기존 정책을 검토 `SQLServerMSASUser$`합니다. 이 계정은 Analysis Services가 설치된 컴퓨터에 있는 로컬 보안 그룹입니다. Windows 권한과 파일 폴더 사용 권한이 모두 이 보안 그룹에 부여됩니다. **서비스로 로그온** 정책을 두 번 클릭하여 시스템에서 보안 그룹이 어떻게 지정되어 있는지 확인합니다. 보안 그룹의 전체 이름은 Analysis Services를 명명된 인스턴스로 설치했는지 여부에 따라 다릅니다. 계정 권한을 추가할 경우 실제 서비스 계정을 사용하지 않고 이 보안 그룹을 사용합니다.  
  
3.  GPEDIT에서 계정 권한을 추가하려면 **프로세스 작업 집합 향상** 을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
4.  **사용자 또는 그룹 추가**를 클릭합니다.  
  
5.  Analysis Services 인스턴스의 사용자 그룹을 입력합니다. 서비스 계정은 로컬 보안 그룹의 구성원이며, 로컬 컴퓨터 이름을 계정의 도메인으로 추가해야 합니다.  
  
     다음 목록은 컴퓨터의 이름이 로컬 도메인인 "SQL01-WIN12" 컴퓨터에 있는 기본 인스턴스와 "Tabular"로 명명된 인스턴스에 대한 두 가지 예를 보여 줍니다.  
  
    -   SQL01-WIN12\SQL01-WIN12$SQLServerMSASUser$MSSQLSERVER  
  
    -   SQL01-WIN12\SQL01-WIN12$SQLServerMSASUser$TABULAR  
  
6.  **프로세스의 메모리 할당량 조정**에 대해 반복하고 필요에 따라 **메모리의 페이지 잠금** 또는 **예약 우선 순위 높임**에 대해서도 반복합니다.  
  
> [!NOTE]  
>  이전 버전의 설치 프로그램에서는 **성능 로그 사용자** 그룹에 Analysis  Services  서비스 계정이 실수로 추가되었습니다. 이 결함이 해결되었지만 기존 설치에는 이 불필요한 그룹 멤버 자격이 있을 수도 있습니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서비스 계정에 **Performance Log Users** 그룹의 멤버 자격이 필요하지 않기 때문에 이 그룹에서 서비스 계정을 제거할 수 있습니다.  
  
##  <a name="bkmk_FilePermissions"></a> Analysis Services 서비스 계정에 할당된 파일 시스템 권한  
  
> [!NOTE]  
>  각 프로그램 폴더와 관련된 권한 목록은 [Windows 서비스 계정 및 권한 구성](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md) 을 참조하세요.  
>   
>  IIS 구성에 관련된 파일 권한 정보 및 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 대한 자세한 내용은 [IIS&#40;인터넷 정보 서비스&#41; 8.0에서 Analysis Services에 대한 HTTP 액세스 구성](configure-http-access-to-analysis-services-on-iis-8-0.md)을 참조하세요.  
  
 지정된 데이터 폴더에서 데이터베이스를 로드 또는 언로드하는 데 필요한 사용 권한을 비롯하여 서버 작업에 필요한 모든 파일 시스템 권한은 SQL Server 설치 프로그램에서 설치 중 할당합니다.  
  
 데이터 파일, 프로그램 실행 파일, 구성 파일, 로그 파일 및 임시 파일에 대한 사용 권한 소유자는 SQL Server 설치 프로그램에서 만든 로컬 보안 그룹입니다.  
  
 설치하는 인스턴스마다 하나의 보안 그룹이 있습니다. 보안 그룹 이름은 따라 하거나 **SQLServerMSASUser$ MSSQLSERVER** 기본 인스턴스의 경우 또는 `SQLServerMSASUser$` \<servername >$\<n a m e > 명명 된 인스턴스에 대 한 합니다. 설치 프로그램은 서버 작업 수행에 필요한 파일 권한으로 이 보안 그룹을 프로비전합니다. \MSAS12.MSSQLSERVER\OLAP\BIN 디렉터리에서 보안 권한을 확인하면 보안 그룹(서비스 계정 또는 서비스별 SID가 아님)이 해당 디렉터리에 대한 권한 보유지임을 알 수 있습니다.  
  
 보안 그룹에는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스 시작 계정의 서비스별 SID(보안 식별자)만 멤버로 포함되어 있습니다. 설치 프로그램에서 서비스별 SID를 로컬 보안 그룹에 추가합니다. SID 멤버 자격이 있는 로컬 보안 그룹을 사용할 경우 데이터베이스 엔진과 비교하여 SQL Server 설치 프로그램이 Analysis Services를 프로비전하는 방식에서 작지만 분명한 차이점이 있습니다.  
  
 파일 권한이 손상되었다고 생각되는 경우 다음 단계에 따라 서비스가 계속해서 올바르게 프로비전되는지 확인하세요.  
  
1.  서비스 제어 명령줄 도구(sc.exe)를 사용하여 기본 서비스 인스턴스의 SID를 가져옵니다.  
  
     `SC showsid MSSqlServerOlapService`  
  
     명명된 인스턴스의 경우(여기서는 인스턴스 이름이 Tabular임) 다음 구문을 사용합니다.  
  
     `SC showsid MSOlap$Tabular`  
  
2.  사용 하 여 **컴퓨터 관리자** | **로컬 사용자 및 그룹** | **그룹** SQLServerMSASUser $멤버자격을검사하려면\<서버 이름 >$\<n a m e > 보안 그룹입니다.  
  
     구성원 SID가 1단계의 서비스별 SID와 일치해야 합니다.  
  
3.  **Windows 탐색기** | **Program Files** | **Microsoft SQL Server** | MSASxx.MSSQLServer | **OLAP** | **bin** 을 사용하여 2단계의 보안 그룹에 보안 속성이 부여된 폴더를 확인합니다.  
  
> [!NOTE]  
>  SID를 제거하거나 수정하지 마세요. 실수로 삭제 된 서비스별 SID를 복원 하려면 참조 [ https://support.microsoft.com/kb/2620201 ](https://support.microsoft.com/kb/2620201)합니다.  
  
 **서비스별 SID에 대한 추가 정보**  
  
 모든 Windows 계정에는 연결된 [SID](http://en.wikipedia.org/wiki/Security_Identifier)가 있지만, 서비스에도 SID가 있으므로 서비스별 SID라고도 합니다. 서비스별 SID는 서비스 인스턴스가 설치될 때 서비스의 고유하고 영구적인 부분으로 생성됩니다. 서비스별 SID는 서비스 이름에서 생성되는 로컬 컴퓨터 수준 SID입니다. 기본 인스턴스에서 사용자 이름은 NT SERVICE\MSSQLServerOLAPService입니다.  
  
 서비스별 SID의 이점은 파일 권한에 영향을 미치지 않고 매우 광범위하게 표시할 수 있는 로그온 계정을 임의로 변경할 수 있다는 것입니다. 예를 들어 Analysis Services 인스턴스를 두 개 설치한 경우, 기본 인스턴스와 명명된 인스턴스가 동일한 Windows 사용자 계정에서 실행되면 로그온 계정이 공유되는 동안 각 서비스 인스턴스는 고유한 서비스별 SID를 갖습니다. 이 SID는 로그온 계정의 SID와는 완전히 다릅니다. 서비스별 SID는 파일 권한 및 Windows 권한에 사용됩니다. 반면에 로그온 계정 SID는 인증 및 권한 부여 시나리오에 사용되며 용도에 따라 다른 SID가 사용됩니다.  
  
 SID는 변경이 불가능하므로 서비스 설치 중 생성된 파일 시스템 ACL을 서비스 계정의 변경 빈도와 상관없이 무제한으로 사용할 수 있습니다. 추가된 보안 조치로, SID를 통해 권한을 지정하는 ACL은 다른 서비스가 동일한 계정에서 실행되더라도 프로그램 실행 파일 및 데이터 폴더가 서비스의 단일 인스턴스에서만 액세스되도록 합니다.  
  
##  <a name="bkmk_tasks"></a> 특정 서버 작업에 대한 추가 Analysis Services 권한 부여  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]를 시작하는 데 사용되는 서비스 계정 또는 로그온 계정의 보안 컨텍스트에서 일부 태스크를 실행하고 태스크를 요청하는 사용자의 보안 컨텍스트에서 나머지 태스크를 실행합니다.  
  
 다음 표에서는 서비스 계정으로 실행되는 태스크를 지원하는 데 필요한 추가 권한에 대해 설명합니다.  
  
|서버 작업|작업 항목|이유|  
|----------------------|---------------|-------------------|  
|외부 관련 데이터 원본에 원격 액세스|서비스 계정의 데이터베이스 로그인 생성|처리는 외부 데이터 원본(일반적으로 관계형 데이터베이스)에서 데이터를 검색하는 단계를 의미합니다. 검색된 데이터는 이후에 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에 로드됩니다. 외부 데이터를 검색하기 위한 자격 증명 옵션 중 하나는 서비스 계정을 사용하는 것입니다. 이 자격 증명 옵션은 서비스 계정에 대한 데이터베이스 로그인을 만들고 원본 데이터베이스에 대한 읽기 권한을 부여하는 경우에만 작동합니다. 이 태스크에 서비스 계정 옵션이 사용되는 방법은 [가장 옵션 설정&#40;SSAS - 다차원&#41;](../multidimensional-models/set-impersonation-options-ssas-multidimensional.md)을 참조하세요. 이와 마찬가지로 ROLAP가 스토리지 모드로 사용되는 경우 동일한 가장 옵션을 사용할 수 있습니다. 이 경우에는 계정에 원본 데이터에 대한 쓰기 권한도 있어야 ROLAP 파티션 처리(집계 저장)가 가능합니다.|  
|DirectQuery|서비스 계정의 데이터베이스 로그인 생성|DirectQuery는 테이블 형식 모델에 들어가기에는 너무 크거나 기본 메모리 내 스토리지 옵션보다 DirectQuery를 적합하게 만드는 다른 특징이 있는 외부 데이터 세트을 쿼리하는 데 사용되는 테이블 형식 기능입니다. DirectQuery 모드에서 사용할 수 있는 연결 옵션 중 하나는 서비스 계정을 사용하는 것입니다. 이 옵션도 서비스 계정에 대상 데이터 원본에 대한 읽기 권한 및 데이터베이스 로그인이 있는 경우에만 작동합니다. 이 태스크에 서비스 계정 옵션이 사용되는 방법은 [가장 옵션 설정&#40;SSAS - 다차원&#41;](../multidimensional-models/set-impersonation-options-ssas-multidimensional.md)을 참조하세요. 또는 현재 사용자의 자격 증명을 사용하여 데이터를 검색할 수 있습니다. 대부분의 경우 이 옵션은 더블홉 연결을 필요로 하므로 서비스 계정이 다운스트림 서버에 ID를 위임할 수 있도록 Kerberos 제한 위임에 대한 서비스 계정을 구성해야 합니다. 자세한 내용은 [Configure Analysis Services for Kerberos constrained delegation](configure-analysis-services-for-kerberos-constrained-delegation.md)을 참조하세요.|  
|다른 SSAS 인스턴스에 대한 원격 액세스|원격 서버에서 정의한 Analysis Services 데이터베이스 역할에 서비스 계정 추가|원격 파티션 및 다른 원격 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 연결된 개체 참조는 원격 컴퓨터 또는 디바이스에 대한 권한이 필요한 시스템 기능입니다. 사용자가 원격 파티션을 만들고 채우거나 연결된 개체를 설정할 때 해당 작업은 현재 사용자의 보안 컨텍스트에서 실행됩니다. 이후에 이러한 작업을 자동화하는 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 서비스 계정의 보안 컨텍스트에서 원격 인스턴스에 액세스합니다. 원격 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스의 연결된 개체에 액세스하려면 로그온 계정이 특정 차원에 대한 읽기 권한과 같이 원격 인스턴스의 해당 개체를 읽을 수 있는 권한을 가져야 합니다. 이와 마찬가지로 원격 파티션을 사용하려면 서비스 계정에 원격 인스턴스에 대한 관리 권한이 있어야 합니다. 이러한 권한은 허용된 작업을 특정 개체와 연결하는 역할을 사용하여 원격 Analysis Services 인스턴스에 대해 부여됩니다. 처리 및 쿼리 작업을 허용하는 모든 권한을 부여하는 방법은 [데이터베이스 권한 부여&#40;Analysis Services&#41;](../multidimensional-models/grant-database-permissions-analysis-services.md)를 참조하세요. 원격 파티션에 대한 자세한 내용은 [원격 파티션 만들기 및 관리&#40;Analysis Services&#41;](../multidimensional-models/create-and-manage-a-remote-partition-analysis-services.md)를 참조하세요.|  
|쓰기 저장(writeback)|원격 서버에서 정의한 Analysis Services 데이터베이스 역할에 서비스 계정 추가|클라이언트 애플리케이션에서 사용되는 경우 쓰기 저장은 데이터 분석 중에 새로운 데이터 값을 만들 수 있도록 허용하는 다차원 모델의 기능입니다. 차원이나 큐브 내에서 쓰기 저장이 사용되는 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서비스 계정은 원본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관계형 데이터베이스에서 쓰기 저장 테이블에 대한 쓰기 권한을 가져야 합니다. 이 테이블이 없어 새로 만들어야 하는 경우에는 지정된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스 내에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정에 CREATE  TABLE  권한도 있어야 합니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관계형 데이터베이스의 쿼리 로그 테이블에 쓰기|서비스 계정의 데이터베이스 로그인 생성 및 쿼리 로그 테이블에 대한 쓰기 권한 할당|이후 분석을 위해 데이터베이스 테이블에서 사용 현황 데이터를 수집하기 위해 쿼리 로깅을 사용하도록 설정할 수 있습니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서비스 계정은 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에서 쿼리 로그 테이블에 대한 쓰기 권한을 가져야 합니다. 이 테이블이 없어 새로 만들어야 하는 경우에는 지정된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스 내에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그온 계정에 CREATE  TABLE  권한도 있어야 합니다. 자세한 내용은 [사용 빈도 기반 최적화 마법사를 사용하여 SQL Server Analysis Services 성능 향상(블로그)](http://www.mssqltips.com/sqlservertip/2876/improve-sql-server-analysis-services-performance-with-the-usage-based-optimization-wizard/) 및 [Analysis Services의 쿼리 로깅(블로그)](http://weblogs.asp.net/miked/archive/2013/07/31/query-logging-in-analysis-services.aspx)을 참조하세요.|  
  
## <a name="see-also"></a>관련 항목  
 [Windows 서비스 계정 및 권한 구성](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)   
 [SQL Server 서비스 계정 및 서비스별 SID(블로그)](http://www.travisgan.com/2013/06/sql-server-service-account-and-per.html)   
 [SQL Server는 서비스 SID를 사용하여 서비스 격리(KB 문서)를 제공합니다.](https://support.microsoft.com/kb/2620201)   
 [액세스 토큰(MSDN)](/windows/desktop/SecAuthZ/access-tokens)   
 [보안 식별자(MSDN)](/windows/desktop/SecAuthZ/security-identifiers)   
 [액세스 토큰(Wikipedia)](http://en.wikipedia.org/wiki/Access_token)   
 [액세스 제어 목록(Wikipedia)](http://en.wikipedia.org/wiki/Access_control_list)  
  
  
