---
title: 시스템 관리자가 잠겨 있을 때 SQL Server에 연결 | Microsoft Docs
description: 시스템 관리자가 실수로 잠긴 경우 SQL Server에 대한 액세스 권한을 다시 얻는 방법을 알아봅니다.
ms.custom: contperfq4
ms.date: 05/20/2020
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- sa account
- connecting when locked out [SQL Server]
- locked out [SQL Server]
ms.assetid: c0c0082e-b867-480f-a54b-79f2a94ceb67
author: markingmyname
ms.author: maghan
ms.openlocfilehash: eec9e95ccbc326d3d2f64d224cf11f3d059bb8f7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85717085"
---
# <a name="connect-to-sql-server-when-system-administrators-are-locked-out"></a>시스템 관리자가 잠긴 경우 SQL Server에 연결 
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
이 문서에서는 잠긴 상태일 때 시스템 관리자로서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에 대한 액세스 권한을 다시 얻는 방법을 설명합니다.  시스템 관리자는 다음 중 한 가지 이유로 인해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 액세스 권한을 상실할 수 있습니다.  
  
-   sysadmin 고정 서버 역할의 멤버인 모든 로그인이 실수로 제거되었습니다.  
  
-   sysadmin 고정 서버 역할의 멤버인 모든 Windows 그룹이 실수로 제거되었습니다.  
  
-   sysadmin 고정 서버 역할의 멤버인 로그인이 회사를 그만두었거나 소재가 불명확한 개인에게 할당되어 있습니다.  
  
-   sa 계정이 비활성화되어 있거나 이 계정의 암호를 아는 사람이 없습니다.  
  
## <a name="resolution"></a>해결 방법

액세스 문제를 해결하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 단일 사용자 모드로 시작하는 것이 좋습니다. 이 모드를 사용하면 액세스 권한을 다시 얻는 동안 다른 연결이 발생하지 않습니다. 이 모드에서는 SQL Server 인스턴스에 연결하고 **sysadmin** 서버 역할에 로그인을 추가할 수 있습니다. 이 솔루션에 대한 자세한 단계는 [단계별 지침](#step-by-step-instructions) 섹션에서 확인할 수 있습니다.


명령줄에서 `-m` 또는 `-f` 옵션을 사용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 단일 사용자 모드로 시작할 수 있습니다. 그러면 컴퓨터에서 로컬 관리자 그룹의 모든 멤버가 **sysadmin** 고정 서버 역할의 멤버로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결할 수 있습니다.  

인스턴스를 단일 사용자 모드로 시작할 때는 먼저 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스를 중지해야 합니다. 그렇지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 먼저 연결되어 서버에 대한 유일한 가용 연결을 사용하기 때문에 로그인할 수 없게 됩니다.

또한 로그인하기 전에 알 수 없는 클라이언트 응용 프로그램에서 사용 가능한 유일한 연결을 차지할 수도 있습니다. 이 문제를 방지하려면 응용 프로그램 이름 뒤에 `-m` 옵션을 사용하여 지정된 응용 프로그램에서의 연결을 단일 연결로 제한할 수 있습니다. 예를 들어 `-m"sqlcmd"`를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 함께 사용하면 자신을 **sqlcmd** 클라이언트 프로그램으로 인식하는 단일 연결로 연결이 제한됩니다. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 쿼리 편집기를 통해 연결하려면 `-m"Microsoft SQL Server Management Studio - Query"`를 사용합니다.  


> [!IMPORTANT]  
> `-m`를 응용 프로그램 이름에 보안 기능으로 사용해선 안 됩니다. 클라이언트 응용 프로그램은 연결 문자열 설정을 통해 응용 프로그램 이름을 지정하므로 가짜 이름을 이용하면 쉽게 스푸핑할 수 있습니다.

다음 표에는 명령줄에서 단일 사용자 모드로 인스턴스를 시작하는 다양한 방법이 요약되어 있습니다.

| 옵션 | Description | 사용 시기 |
|:---|:---|:---|
|`-m` | 연결을 단일 연결로 제한 | 인스턴스에 연결을 시도하는 다른 사용자가 없거나 인스턴스에 연결하는 데 어떤 애플리케이션 이름을 사용하는지 모르는 경우. |
|`-m"sqlcmd"`| 자신을 **sqlcmd** 클라이언트 프로그램으로 인식하는 단일 연결로 연결을 제한| **sqlcmd**를 사용하여 인스턴스에 연결할 계획이며 다른 응용 프로그램에서 사용 가능한 유일한 연결을 차지하지 못하게 하려는 경우. |
|`-m"Microsoft SQL Server Management Studio - Query"`| 자신을 **Microsoft SQL Server Management Studio - 쿼리** 응용 프로그램으로 인식하는 단일 연결로 연결을 제한| [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 쿼리 편집기를 사용하여 인스턴스에 연결할 계획이며 다른 응용 프로그램에서 사용 가능한 유일한 연결을 차지하지 못하게 하려는 경우. |
|`-f`| 연결을 단일 연결로 제한하고 인스턴스를 최소 구성으로 시작 | 다른 구성 때문에 시작할 수 없는 경우. |
| &nbsp; | &nbsp; | &nbsp; |
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 단일 사용자 모드로 시작하는 방법에 대한 단계별 지침은 [단일 사용자 모드로 SQL Server 시작](../../database-engine/configure-windows/start-sql-server-in-single-user-mode.md)을 참조하십시오.

## <a name="step-by-step-instructions"></a>단계별 지침

다음 단계별 지침은 실수로 액세스 권한이 제거된 SQL Server 로그인에 시스템 관리자 권한을 부여하는 방법을 설명합니다.

이 지침은 다음 조건을 가정합니다.

* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 Windows 8 이상에서 실행됩니다. 적용 가능한 경우 이전 버전의 SQL Server 또는 Windows에서는 지침이 조금 조정됩니다.

* [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]가 컴퓨터에 설치되어 있습니다.  

로컬 관리자 그룹의 멤버로 Windows에 로그인된 상태에서 이 지침을 수행합니다.

1.  Windows 시작 메뉴에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager 아이콘을 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 선택하여 관리자 자격 증명을 Configuration Manager에 전달합니다.  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자의 왼쪽 창에서 **SQL Server 서비스**를 선택합니다. 오른쪽 창에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 찾습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 기본 인스턴스에는 컴퓨터 이름 뒤에 **(MSSQLSERVER)** 가 있습니다. 명명된 인스턴스는 등록된 서버에서와 같은 이름(대문자)으로 나타납니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
3.  **시작 매개 변수** 탭의 **시작 매개 변수 지정** 상자에 `-m`를 입력하고 **추가**를 클릭합니다. 클릭합니다.  
  
    > [!NOTE]  
    >  몇몇 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에는 **시작 매개 변수** 탭이 없습니다. 이 탭이 없는 경우 **고급** 탭에서 **시작 매개 변수**를 두 번 클릭합니다. 매개 변수가 아주 작은 창에서 열립니다. 기존 매개 변수를 변경하지 않도록 주의하십시오. 맨 끝에 새 매개 변수 `;-m` (대시와 소문자 m)을 입력하고 **확인**를 클릭합니다.  
  
4.  **확인**을 클릭하고 다시 시작 메시지가 나타나면 서버 이름을 마우스 오른쪽 단추로 클릭한 다음 **다시 시작**을 클릭합니다.  
  
5.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 다시 시작하면 서버는 단일 사용자 모드가 됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 실행되고 있지 않은지 확인합니다. 시작된 경우 사용자의 유일한 연결을 사용합니다.  
  
6.  시작 메뉴에서 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 아이콘을 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 선택합니다. SSMS에 관리자 자격 증명이 전달됩니다.
  
    > [!NOTE]  
    >  이전 버전의 Windows에서는 **관리자 권한으로 실행** 옵션이 하위 메뉴로 나타납니다.  
  
     일부 구성에서는 SSMS가 여러 연결을 시도합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 단일 사용자 모드이기 때문에 여러 연결이 실패합니다. 시나리오에 따라 다음 작업 중 하나를 수행합니다.  
  
    1.  관리자 자격 증명을 포함하는 Windows 인증을 사용하여 개체 탐색기에 연결합니다. **보안**과 **로그인**을 차례로 확장하고 로그인을 두 번 클릭합니다. **서버 역할** 페이지에서 **sysadmin**을 선택하고 **확인**을 클릭합니다.  
  
    2.  관리자 자격 증명을 포함하는 Windows 인증을 사용하여 개체 탐색기 대신 쿼리 창에 연결합니다. 개체 탐색기에 연결할 수 없는 경우에만 이 방식으로 연결할 수 있습니다. 다음과 같은 코드를 실행하여 **sysadmin** 고정 서버 역할의 구성원인 새 Windows 인증 로그인을 추가합니다. 다음 예제에서는 `CONTOSO\PatK`이라는 도메인 사용자를 추가합니다.  
  
        ```  
        CREATE LOGIN [CONTOSO\PatK] FROM WINDOWS;  
        ALTER SERVER ROLE sysadmin ADD MEMBER [CONTOSO\PatK];  
        ```  
  
    3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 혼합 인증 모드에서 실행 중인 경우 관리자 자격 증명을 포함하는 Windows 인증을 사용하여 쿼리 창에 연결합니다. 다음과 같은 코드를 실행하여 **sysadmin** 고정 서버 역할의 구성원인 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 로그인을 만듭니다.  
  
        ```  
        CREATE LOGIN TempLogin WITH PASSWORD = '************';  
        ALTER SERVER ROLE sysadmin ADD MEMBER TempLogin;  
        ```  
  
        > [!WARNING]  
        >  ************는 강력한 암호로 대체합니다.  
  
    4.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 혼합 인증 모드에서 실행 중이며 **sa** 계정의 암호를 재설정하려는 경우 관리자 자격 증명을 포함하는 Windows 인증을 사용하여 쿼리 창에 연결합니다. 다음 구문을 사용하여 **sa** 계정의 암호를 변경 합니다.  
  
        ```  
        ALTER LOGIN sa WITH PASSWORD = '************';  
        ```  
  
        > [!WARNING]  
        >  ************는 강력한 암호로 대체합니다.  

7. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]를 닫습니다.  
  
8. 다음 몇 가지 단계는 SQL Server 다시 다중 사용자 모드로 전환합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자의 왼쪽 창에서 **SQL Server 서비스**를 선택합니다.

9. 오른쪽 창에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
10. **시작 매개 변수** 탭의 **기존 매개 변수** 상자에서 `-m` 을 선택하고 **제거**를 클릭합니다.  
  
    > [!NOTE]  
    >  몇몇 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에는 **시작 매개 변수** 탭이 없습니다. 이 탭이 없는 경우 **고급** 탭에서 **시작 매개 변수**를 두 번 클릭합니다. 매개 변수가 아주 작은 창에서 열립니다. 이전에 추가한 `;-m` 을 제거하고 **확인**을 클릭합니다.  
  
11. 서버를 마우스 오른쪽 단추로 클릭한 다음 **다시 시작**을 클릭합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 중지했다면 다시 시작한 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 단일 사용자 모드로 시작해야 합니다.
  
이제 **sysadmin** 고정 서버 역할의 멤버인 계정 중 하나에 정상적으로 연결할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  

* [서버 시작 옵션 구성](../../database-engine/configure-windows/scm-services-configure-server-startup-options.md)
* [데이터베이스 엔진 서비스 시작 옵션](../../database-engine/configure-windows/database-engine-service-startup-options.md)  
