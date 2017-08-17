---
title: "시스템 관리자가 잠겨 있을 때 SQL Server에 연결 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- sa account
- connecting when locked out [SQL Server]
- locked out [SQL Server]
ms.assetid: c0c0082e-b867-480f-a54b-79f2a94ceb67
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7f14625038501a21d4321f45471a4391d29efec9
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="connect-to-sql-server-when-system-administrators-are-locked-out"></a>시스템 관리자가 잠겨 있는 경우 SQL Server에 연결
  이 항목에서는 시스템 관리자로서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 에 대한 액세스 권한을 다시 얻을 수 있는 방법에 대해 설명합니다. 시스템 관리자는 다음 중 한 가지 이유로 인해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 액세스 권한을 상실할 수 있습니다.  
  
-   sysadmin 고정 서버 역할의 멤버인 모든 로그인이 실수로 제거되었습니다.  
  
-   sysadmin 고정 서버 역할의 멤버인 모든 Windows 그룹이 실수로 제거되었습니다.  
  
-   sysadmin 고정 서버 역할의 멤버인 로그인이 회사를 그만두었거나 소재가 불명확한 개인에게 할당되어 있습니다.  
  
-   sa 계정이 비활성화되어 있거나 이 계정의 암호를 아는 사람이 없습니다.  
  
 액세스 권한을 다시 얻을 수 있는 한 가지 방법은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 다시 설치하고 모든 데이터베이스를 새 인스턴스에 연결하는 것입니다. 이 방법에 따라 문제를 해결하는 데는 많은 시간이 소요됩니다. 또한 로그인을 복구하려면 백업에서 master 데이터베이스를 복원해야 할 수도 있습니다. master 데이터베이스의 백업이 최신 백업이 아닌 경우 이 백업에 모든 정보가 포함되지 않을 수도 있습니다. master 데이터베이스의 백업이 최신 백업인 경우에는 이 백업에 이전 인스턴스와 동일한 로그인이 포함되어 있으므로 관리자는 여전히 잠겨 있게 됩니다.  
  
## <a name="resolution"></a>해결 방법  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -m **또는** -f **옵션을 사용하여** 인스턴스를 단일 사용자 모드로 시작합니다. 그러면 컴퓨터에서 로컬 Administrators 그룹의 모든 멤버가 sysadmin 고정 서버 역할의 멤버로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 단일 사용자 모드로 시작할 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스를 먼저 중지하십시오. 그렇지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 먼저 연결되므로 두 번째 사용자로 연결하지 못합니다.  
  
 **sqlcmd** 와 함께 **-m** 옵션을 사용하거나 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]을 사용할 경우 지정한 클라이언트 응용 프로그램에 대한 연결 수를 제한할 수 있습니다. 예를 들어 **-m"sqlcmd"** 는 연결 수를 단일 연결로 제한하며 이 경우 연결은 자신을 **sqlcmd** 클라이언트 프로그램으로 인식해야 합니다. 단일 사용자 모드에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 시작하며 알 수 없는 클라이언트 응용 프로그램에서 사용 가능한 유일한 연결을 사용할 경우 이 옵션을 사용합니다. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 쿼리 편집기를 통해 연결하려면 **-m"Microsoft SQL Server Management Studio - 쿼리"**를 사용합니다.  
  
> [!IMPORTANT]  
>  이 옵션을 보안 용도로는 사용하지 마십시오. 클라이언트 응용 프로그램에서 클라이언트 응용 프로그램 이름을 제공하므로 연결 문자열의 일부로 잘못된 이름을 제공할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 단일 사용자 모드로 시작하는 방법에 대한 단계별 지침은 [서버 시작 옵션 구성&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/scm-services-configure-server-startup-options.md)을 참조하세요.  
  
## <a name="step-by-step-instructions"></a>단계별 지침  
 다음 지침에서는 Windows 8 이상에서 실행 중인 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에 연결하는 과정을 설명합니다. 이전 버전의 SQL Server 또는 Windows의 경우 지침이 조금 조정되어 제공됩니다. 로컬 관리자 그룹의 멤버로 Windows에 로그인한 상태에서 이들 지침을 수행해야 하며 컴퓨터에 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 가 설치되어 있어야 합니다.  
  
1.  시작 페이지에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 시작합니다. **보기** 메뉴에서 **등록된 서버**를 선택합니다. 서버가 이미 등록되어 있지 않으면 **로컬 서버 그룹**을 마우스 오른쪽 단추로 클릭하고 **태스크**를 가리킨 다음 **로컬 서버 등록**을 클릭합니다.  
  
2.  등록된 서버 영역에서 서버를 마우스 오른쪽 단추로 클릭하고 **SQL Server 구성 관리자**를 클릭합니다. 관리자 권한으로 실행할지 묻고 구성 관리자 프로그램이 열립니다.  
  
3.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]를 닫습니다.  
  
4.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자의 왼쪽 창에서 **SQL Server 서비스**를 선택합니다. 오른쪽 창에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 찾습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 기본 인스턴스에는 컴퓨터 이름 뒤에 **(MSSQLSERVER)**가 있습니다. 명명된 인스턴스는 등록된 서버에서와 같은 이름(대문자)으로 나타납니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
5.  **시작 매개 변수** 탭의 **시작 매개 변수 지정** 상자에 `-m`를 입력하고 **추가**를 클릭합니다. 클릭합니다.  
  
    > [!NOTE]  
    >  몇몇 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에는 **시작 매개 변수** 탭이 없습니다. 이 탭이 없는 경우 **고급** 탭에서 **시작 매개 변수**를 두 번 클릭합니다. 매개 변수가 아주 작은 창에서 열립니다. 기존 매개 변수를 변경하지 않도록 주의하십시오. 맨 끝에 새 매개 변수 `;-m` (대시와 소문자 m)을 입력하고 **확인**를 클릭합니다.  
  
6.  **확인**을 클릭하고 다시 시작 메시지가 나타나면 서버 이름을 마우스 오른쪽 단추로 클릭한 다음 **다시 시작**을 클릭합니다.  
  
7.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이 다시 시작한 후에 서버는 단일 사용자 모드가 됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 실행 중이지 않는지 확인합니다. 시작된 경우 사용자의 유일한 연결을 사용합니다.  
  
8.  Windows 8 시작 화면에서 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]아이콘을 마우스 오른쪽 단추로 클릭합니다. 화면 아래쪽에서 **관리자 권한으로 실행**을 선택합니다. SSMS에 관리자 자격 증명이 전달됩니다.  
  
    > [!NOTE]  
    >  이전 버전의 Windows에서는 **관리자 권한으로 실행** 옵션이 하위 메뉴로 나타납니다.  
  
     일부 구성에서는 SSMS가 여러 연결을 시도합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 단일 사용자 모드이기 때문에 여러 연결이 실패합니다. 다음 작업 중 하나를 수행하도록 선택할 수 있습니다. 다음 중 하나를 수행합니다.  
  
    1.  관리자 자격 증명을 포함하는 Windows 인증을 사용하여 개체 탐색기에 연결합니다. **보안**과 **로그인**을 차례로 확장하고 로그인을 두 번 클릭합니다. **서버 역할** 페이지에서 **sysadmin**을 선택하고 **확인**을 클릭합니다.  
  
    2.  관리자 자격 증명을 포함하는 Windows 인증을 사용하여 개체 탐색기 대신 쿼리 창에 연결합니다. 개체 탐색기에 연결할 수 없는 경우에만 이 방식으로 연결할 수 있습니다. 다음과 같은 코드를 실행하여 **sysadmin** 고정 서버 역할의 구성원인 새 Windows 인증 로그인을 추가합니다. 다음 예제에서는 `CONTOSO\PatK`이라는 도메인 사용자를 추가합니다.  
  
        ```  
        CREATE LOGIN [CONTOSO\PatK] FROM WINDOWS;  
        ALTER SERVER ROLE sysadmin ADD MEMBER [CONTOSO\PatK];  
        ```  
  
    3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 혼합 인증 모드에서 실행 중인 경우 관리자 자격 증명을 포함하는 Windows 인증을 사용하여 쿼리 창에 연결합니다. 다음과 같은 코드를 실행하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sysadmin **고정 서버 역할의 구성원인 새** 인증 로그인을 만듭니다.  
  
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
  
9. 다음 단계에서는 이제 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 다중 사용자 모드로 다시 변경합니다. SSMS를 닫습니다.  
  
10. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자의 왼쪽 창에서 **SQL Server 서비스**를 선택합니다. 오른쪽 창에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
11. **시작 매개 변수** 탭의 **기존 매개 변수** 상자에서 `-m` 을 선택하고 **제거**를 클릭합니다.  
  
    > [!NOTE]  
    >  몇몇 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에는 **시작 매개 변수** 탭이 없습니다. 이 탭이 없는 경우 **고급** 탭에서 **시작 매개 변수**를 두 번 클릭합니다. 매개 변수가 아주 작은 창에서 열립니다. 이전에 추가한 `;-m` 을 제거하고 **확인**을 클릭합니다.  
  
12. 서버를 마우스 오른쪽 단추로 클릭한 다음 **다시 시작**을 클릭합니다.  
  
 이제 **sysadmin** 고정 서버 역할의 멤버인 계정 중 하나에 정상적으로 연결할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [단일 사용자 모드로 SQL Server 시작](../../database-engine/configure-windows/start-sql-server-in-single-user-mode.md)   
 [데이터베이스 엔진 서비스 시작 옵션](../../database-engine/configure-windows/database-engine-service-startup-options.md)  
  
  
