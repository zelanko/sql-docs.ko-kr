---
title: 설치 Distributed Replay (설치) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 64479cdc-661a-4e32-a381-8f8b5a238337
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 1e91b1b3af5c8531800f60478a4cb31d31ac3fbc
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85054744"
---
# <a name="install-distributed-replay-setup"></a>Distributed Replay 설치(설치)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 마법사를 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Distributed Replay 기능을 설치합니다. 기능 설치 위치를 계획할 때는 다음 사항을 고려하십시오.  
  
-   관리 도구는 Distributed Replay Controller와 동일한 컴퓨터 또는 다른 컴퓨터에 설치할 수 있습니다.  
  
-   각 Distributed Replay 환경에는 컨트롤러가 하나만 있을 수 있습니다.  
  
-   최대 16개 컴퓨터(실제 컴퓨터 또는 가상 컴퓨터)에 클라이언트 서비스를 설치할 수 있습니다.  
  
-   Distributed Replay 컴퓨터에는 클라이언트 서비스 인스턴스를 하나만 설치할 수 있습니다. Distributed Replay 환경에 클라이언트가 여러 개 있는 경우에는 컨트롤러와 같은 컴퓨터에 클라이언트 서비스를 설치하지 않는 것이 좋습니다. 이렇게 하면 전체적인 분산 재생 속도가 느려질 수 있습니다.  
  
-   성능 테스트 시나리오의 경우에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 대상 인스턴스에 관리 도구, Distributed Replay 컨트롤러 서비스 또는 Client 서비스를 설치하지 않는 것이 좋습니다. 애플리케이션 호환성을 위한 기능 테스트 시에만 이러한 모든 기능을 대상 서버에 설치해야 합니다.  
  
-   설치 후에는 클라이언트에서 Distributed Replay  Client 서비스를 시작하기 전에 컨트롤러 서비스인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller를 실행해야 합니다.  
  
> [!NOTE]  
>  Distributed Replay 기능을 제거하거나 변경하려면 Windows **제어판** 의 **프로그램 및 기능**창을 사용합니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 프로그램 제거 또는 변경 **창에서** 를 선택한 다음 **제거** 를 클릭하면 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 설치 마법사가 열립니다. **기능 선택** 페이지에서 제거할 Distributed Replay 기능을 선택하면 됩니다.  
  
 **사전 요구 사항:**  
  
-   사용하려는 컴퓨터가 [Distributed Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md)항목에 설명된 요구 사항을 충족하는지 확인하십시오.  
  
-   이 절차를 시작하기 전에 컨트롤러와 클라이언트 서비스를 실행할 도메인 사용자 계정을 만듭니다. Windows Administrators 그룹의 멤버가 아닌 계정을 만드는 것이 좋습니다. 자세한 내용은 [Distributed Replay Security](../../tools/distributed-replay/distributed-replay-security.md) 항목에서 사용자 및 서비스 계정 섹션을 참조하십시오.  
  
    > [!NOTE]  
    >  관리 도구, 컨트롤러 서비스 및 클라이언트 서비스를 같은 컴퓨터에서 실행하는 경우에는 로컬 사용자 계정을 사용할 수 있습니다.  
  
 **설치 위치:**  
  
 기본 파일 위치 및 표준 설치를 사용한다고 가정할 때 기본 디렉터리는 C:\Program Files\Microsoft SQL Server입니다. 이진 파일과 어셈블리는 이 디렉터리 내의 다음 위치에 설치됩니다.  
  
-   32비트 시스템:  
  
     [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]Tools  
  
     \- 또는 -  
  
     \<Share Feature Directory>\Tools \\ (사용자가 제공한 대체 공유 기능 디렉터리)  
  
-   64비트 시스템:  
  
     C:\Program files \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (x86) \120\Tools  
  
     \- 또는 -  
  
     \<Share Feature Directory (x86)>\Tools \\ (사용자가 제공한 대체 공유 기능 (x86) 디렉터리)  
  
### <a name="to-install-distributed-replay-features"></a>Distributed Replay 기능을 설치하려면  
  
1.  Distributed Replay 기능 설치를 시작하려면 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 설치 마법사를 시작합니다.  
  
2.  **설치 지원 규칙** 페이지에는 SQL Server 설치 지원 파일을 설치할 때 발생할 수 있는 문제가 표시됩니다. 설치를 계속하려면 모든 설치 지원 오류를 수정해야 합니다.  
  
3.  **제품 키** 페이지에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]무료 버전을 설치할지 아니면 PID 키가 있는 제품의 프로덕션 버전을 설치할지를 나타내는 옵션 단추를 선택합니다. 자세한 내용은 [SQL Server 2014의 버전 및 구성 요소](../editions-and-components-of-sql-server-2016.md)를 참조 하세요.  
  
4.  **사용 조건** 페이지에서 사용권 계약을 읽은 다음 사용 조건과 계약 조건에 동의하면 해당 확인란을 선택합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 개선을 돕기 위해 기능 사용 옵션을 사용하도록 설정하여 [!INCLUDE[msCoName](../../includes/msconame-md.md)]로 보고서를 보낼 수도 있습니다.  
  
5.  **설치 지원 파일** 페이지에서 **설치** 를 클릭하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 설치 지원 파일을 설치 또는 업데이트합니다.  
  
6.  **설치 역할** 페이지에서 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능 설치**를 선택하고 **다음** 을 클릭하여 **기능 선택** 페이지를 계속 진행합니다.  
  
7.  **기능 선택** 페이지에서 설치할 기능을 구성합니다.  
  
    -   관리 도구를 설치하려면 **관리 도구 - 기본**을 선택합니다.  
  
    -   컨트롤러 서비스를 설치하려면 **Distributed Replay Controller**를 선택합니다.  
  
    -   클라이언트 서비스를 설치하려면 **Distributed Replay Client**를 선택합니다.  
  
     **중요**: Distributed Replay Controller를 구성할 때 Distributed Replay Client 서비스를 실행하는 데 사용할 사용자 계정을 하나 이상 지정할 수 있습니다. 다음은 지원되는 계정 목록입니다.  
  
    -   도메인 사용자 계정  
  
    -   사용자가 만든 로컬 사용자 계정  
  
    -   관리자  
  
    -   가상 계정 및 MSA(관리 서비스 계정)  
  
    -   Network Services, 로컬 서비스 및 시스템  
  
     그룹 계정(로컬 또는 도메인) 및 다른 기본 제공 계정(예: Everyone)은 사용할 수 없습니다.  
  
8.  필요에 따라 줄임표(...) 단추를 클릭하여 공유 기능 디렉터리 경로를 변경합니다.  
  
    1.  32비트 컴퓨터의 기본 설치 경로는 **C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\**  
  
    2.  64비트 컴퓨터의 기본 설치 경로는 **C:\Program Files (x86)\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\** 입니다.  
  
9. 작업을 마쳤으면 **다음**을 클릭합니다.  
  
10. **설치 규칙** 페이지에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램이 컴퓨터 구성의 유효성을 검사합니다. 유효성 검사 프로세스가 완료되면 **다음**을 클릭합니다.  
  
11. **디스크 공간 요구 사항** 페이지에서는 지정한 기능에 필요한 디스크 공간을 계산합니다. 그런 다음 사용 가능한 디스크 공간과 필요한 디스크 공간을 비교합니다.  
  
12. **오류 보고** 페이지에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 개선에 도움이 되도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 보낼 정보를 지정할 수 있습니다. 오류 보고 옵션은 기본적으로 사용됩니다.  
  
13. **설치 구성 규칙** 페이지에서는 시스템 구성 검사기가 규칙 집합을 하나 더 실행하여 지정한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능에 대한 컴퓨터 구성의 유효성을 검사합니다.  
  
14. **프로그램 설치 준비 완료** 페이지에서 **설치**를 클릭합니다.  
  
    > [!IMPORTANT]  
    >  Distributed Replay를 설치한 후에는 컨트롤러 및 클라이언트 컴퓨터에서 방화벽 규칙을 만들고 각 클라이언트 컴퓨터에 대상 서버에 대한 권한을 부여해야 합니다. 자세한 내용은 [설치 후 단계 완료](../../tools/distributed-replay/complete-the-post-installation-steps.md)를 참조하세요.  
  
 다음의 추가 항목에 Distributed Replay를 설치하는 다른 방법이 설명되어 있습니다.  
  
-   [명령 프롬프트에서 Distributed Replay 설치](../../tools/distributed-replay/install-distributed-replay-overview.md)  
  
-   [구성 파일을 사용하여 Distributed Replay 설치](../../../2014/sql-server/install/install-distributed-replay-using-a-configuration-file.md)  
  
## <a name="net-framework-security"></a>.NET Framework 보안  
 Distributed Replay 기능을 설치하려면 관리 권한이 있어야 합니다. sysadmin 권한을 가진 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인만 테스트 서버의 sysadmin 서버 역할에 클라이언트 서비스 계정을 추가할 수 있습니다. Distributed Replay 보안 고려 사항에 대한 자세한 내용은 [Distributed Replay Security](../../tools/distributed-replay/distributed-replay-security.md)을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 2014 버전에서 지 원하는 기능](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)   
 [Distributed Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md)   
 [관리 도구 명령줄 옵션&#40;Distributed Replay Utility&#41;](../../tools/distributed-replay/administration-tool-command-line-options-distributed-replay-utility.md)   
 [Distributed Replay 구성](../../tools/distributed-replay/configure-distributed-replay.md)  
  
  
