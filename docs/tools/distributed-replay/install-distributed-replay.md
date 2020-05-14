---
title: Distributed Replay 설치
titleSuffix: SQL Server Distributed Replay
description: 이 문서에서는 설치 마법사, 명령 프롬프트 창 또는 구성 파일을 사용하여 Distributed Replay를 설치하는 방법에 대해 설명합니다.
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: ea1171da-f50e-4f16-bedc-5e468a46477f
author: MikeRayMSFT
ms.author: mikeray
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: 08e69ce63d3bd3524614f014a2c193cad1634389
ms.sourcegitcommit: 4b5919e3ae5e252f8d6422e8e6fddac1319075a1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2020
ms.locfileid: "82999393"
---
# <a name="install-distributed-replay"></a>Distributed Replay 설치

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Distributed Replay는 다음 세 가지 방법 중 하나로 설치할 수 있습니다.  
  
-   [설치 마법사에서 Distributed Replay 설치](#bkmk_wizard)  
  
-   [명령 프롬프트에서 Distributed Replay 설치](#bkmk_command_prompt)  
  
-   [구성 파일을 사용하여 Distributed Replay 설치](#bkmk_configuration_file)  
  
##  <a name="install-distributed-replay-from-the-installation-wizard"></a><a name="bkmk_wizard"></a> 설치 마법사에서 Distributed Replay 설치  
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
  
-   사용하려는 컴퓨터가 [Distributed Replay Requirements](../../tools/distributed-replay/distributed-replay-requirements.md)항목에 설명된 요구 사항을 충족하는지 확인하십시오.  
  
-   이 절차를 시작하기 전에 컨트롤러와 클라이언트 서비스를 실행할 도메인 사용자 계정을 만듭니다. Windows Administrators 그룹의 멤버가 아닌 계정을 만드는 것이 좋습니다. 자세한 내용은 [Distributed Replay Security](../../tools/distributed-replay/distributed-replay-security.md) 항목에서 사용자 및 서비스 계정 섹션을 참조하십시오.  
  
    > [!NOTE]  
    >  관리 도구, 컨트롤러 서비스 및 클라이언트 서비스를 같은 컴퓨터에서 실행하는 경우에는 로컬 사용자 계정을 사용할 수 있습니다.  
  
 **설치 위치:**  
  
 기본 파일 위치 및 표준 설치를 사용한다고 가정할 때 기본 디렉터리는 C:\Program Files\Microsoft SQL Server입니다. 이진 파일과 어셈블리는 이 디렉터리 내의 다음 위치에 설치됩니다.  
  
-   32비트 시스템:  
  
     [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]Tools  
  
     \- 또는 -  
  
     \<공유 기능 디렉터리>\Tools\\(사용자가 입력한 대체 공유 기능 디렉터리)  
  
-   64비트 시스템:  
  
     C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (x86)\130\Tools  
  
     \- 또는 -  
  
     \<공유 기능 디렉터리 (x86)>\Tools\\(사용자가 입력한 공유 기능 대체(x86) 디렉터리)  
  
#### <a name="to-install-distributed-replay-features"></a>Distributed Replay 기능을 설치하려면  
  
1.  Distributed Replay 기능 설치를 시작하려면 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 설치 마법사를 시작합니다.  
  
2.  **설치 지원 규칙** 페이지에는 SQL Server 설치 지원 파일을 설치할 때 발생할 수 있는 문제가 표시됩니다. 설치를 계속하려면 모든 설치 지원 오류를 수정해야 합니다.  
  
3.  **제품 키** 페이지에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]무료 버전을 설치할지 아니면 PID 키가 있는 제품의 프로덕션 버전을 설치할지를 나타내는 옵션 단추를 선택합니다. 자세한 내용은 [SQL Server 2016 버전 및 구성 요소](../../sql-server/editions-and-components-of-sql-server-2016.md)를 참조하세요.  
  
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
  
### <a name="net-framework-security"></a>.NET Framework 보안  
 Distributed Replay 기능을 설치하려면 관리 권한이 있어야 합니다. sysadmin 권한을 가진 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인만 테스트 서버의 sysadmin 서버 역할에 클라이언트 서비스 계정을 추가할 수 있습니다. Distributed Replay 보안 고려 사항에 대한 자세한 내용은 [Distributed Replay Security](../../tools/distributed-replay/distributed-replay-security.md)을 참조하십시오.  
  
##  <a name="install-distributed-replay-from-the-command-prompt"></a><a name="bkmk_command_prompt"></a> 명령 프롬프트에서 Distributed Replay 설치  
 명령 프롬프트에서 Distributed Replay의 새 인스턴스를 설치할 경우 어떤 기능을 설치할지 지정하고 그 기능을 어떻게 구성할지 지정할 수 있습니다. 명령 프롬프트에서 설치하면 Distributed Replay 구성 요소를 설치, 복원, 업그레이드 및 제거할 수 있습니다. 명령 프롬프트에서 설치할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 /Q 매개 변수를 사용하는 완전 자동 모드를 지원합니다.  
  
> [!NOTE]  
>  로컬 설치의 경우 관리자로 설치 프로그램을 실행해야 합니다. 원격 공유로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하는 경우 원격 공유에 대한 읽기 및 실행 권한이 있는 도메인 계정을 사용해야 합니다.  
  
### <a name="installation-parameters"></a>설치 매개 변수  
 최상위 기능 목록에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]및 도구가 포함됩니다. 도구 기능은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리 도구, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서, [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]및 기타 공유 구성 요소를 설치합니다. Distributed Replay 구성 요소를 설치하려면 다음 매개 변수를 지정합니다.  
  
|구성 요소|매개 변수|  
|---------------|---------------|  
|Distributed Replay Controller|**DREPLAY_CTLR**|  
|Distributed Replay Client|**DREPLAY_CLT**|  
|관리 도구|**Tools**|  
  
> [!IMPORTANT]  
>  Distributed Replay를 설치한 후에는 컨트롤러 및 클라이언트 컴퓨터에서 방화벽 규칙을 만들고 각 클라이언트 컴퓨터에 대상 서버에 대한 권한을 부여해야 합니다. 자세한 내용은 [설치 후 단계 완료](../../tools/distributed-replay/complete-the-post-installation-steps.md)를 참조하세요.  
  
 다음 표에 나와 있는 매개 변수를 사용하여 설치 명령줄 스크립트를 개발할 수 있습니다.  
  
|매개 변수|Description|지원되는 값|  
|---------------|-----------------|----------------------|  
|/CTLRSVCACCOUNT<br /><br /> **선택 사항**|Distributed Replay Controller 서비스의 서비스 계정|계정 및 암호 확인|  
|/CTLRSVCPASSWORD<br /><br /> **선택 사항**|Distributed Replay Controller 서비스 계정의 암호|계정 및 암호 확인|  
|/CTLRSTARTUPTYPE<br /><br /> **선택 사항**|Distributed Replay Controller 서비스의 시작 유형|자동<br /><br /> 사용 안 함<br /><br /> 설명서|  
|/CTLRUSERS<br /><br /> **선택 사항**|Distributed Replay Controller 서비스에 대한 사용 권한을 가지는 사용자를 지정합니다.|구분 기호로 공백(“ ”)을 사용하는 일련의 사용자 계정 문자열<br /><br /> **중요**: Distributed Replay Controller 서비스를 구성할 때 Distributed Replay Client 서비스를 실행하는 데 사용할 사용자 계정을 하나 이상 지정할 수 있습니다. 다음은 지원되는 계정 목록입니다.<br /><br /> 도메인 사용자 계정<br /><br /> 사용자가 만든 로컬 사용자 계정<br /><br /> 관리자<br /><br /> 관리자<br /><br /> 가상 계정 및 MSA(관리 서비스 계정)<br /><br /> Network Services, 로컬 서비스 및 시스템<br /><br /> <br /><br /> 참고: 그룹 계정(로컬 또는 도메인) 및 다른 기본 제공 계정(예: Everyone)은 사용할 수 없습니다.|  
|/CLTSVCACCOUNT<br /><br /> **선택 사항**|Distributed Replay Client 서비스의 서비스 계정|계정 및 암호 확인|  
|/CLTSVCPASSWORD<br /><br /> **선택 사항**|Distributed Replay Client 서비스 계정의 암호|계정 및 암호 확인|  
|/CLTSTARTUPTYPE<br /><br /> **선택 사항**|Distributed Replay Client 서비스의 시작 유형|자동<br /><br /> 사용 안 함<br /><br /> 설명서|  
|/CLTCTLRNAME<br /><br /> **선택 사항**|클라이언트에서 Distributed Replay Controller 서비스를 위해 통신하는 컴퓨터 이름||  
|/CLTWORKINGDIR<br /><br /> **선택 사항**|Distributed Replay Client 서비스의 작업 디렉터리|올바른 경로|  
|/CLTRESULTDIR<br /><br /> **선택 사항**|Distributed Replay Client 서비스의 결과 디렉터리|올바른 경로|  
  
### <a name="sample-syntax"></a>예제 구문:  
 **Distributed Replay Controller 구성 요소를 설치하려면**  
  
```  
setup /q /ACTION=Install /FEATURES=DREPLAY_CTLR /IAcceptSQLServerLicenseTerms /CTLRUSERS="domain\user1" "domain\user2" /CTLRSVCACCOUNT="domain\svcuser" /CTLRSVCPASSWORD="password" /CTLRSTARTUPTYPE=Automatic  
```  
  
 **Distributed Replay Client 구성 요소를 설치하려면**  
  
```  
setup /q /ACTION=Install /FEATURES=DREPLAY_CLT /IAcceptSQLServerLicenseTerms /CLTSVCACCOUNT="domain\svcuser" /CLTSVCPASSWORD="password" /CLTSTARTUPTYPE=Automatic /CLTCTLRNAME=ControllerMachineName /CLTWORKINGDIR="C:\WorkingDir" /CLTRESULTDIR="C:\ResultDir  
```  
  
##  <a name="install-distributed-replay-using-a-configuration-file"></a><a name="bkmk_configuration_file"></a> 구성 파일을 사용하여 Distributed Replay 설치  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 시 사용자 입력 및 시스템 기본값을 기반으로 구성 파일을 생성할 수 있습니다. 관리 도구를 설치하도록 지정한 경우 이 구성 파일을 사용하여 세 가지 Distributed Replay 구성 요소(관리 도구, Distributed Replay Controller 및 Distributed Replay Client)를 배포할 수 있습니다. 구성 파일을 사용하면 Distributed Replay 구성 요소를 설치, 복구 및 다시 설치할 수 있습니다.  
  
 구성 파일은 명령줄에서 설치할 경우에만 사용할 수 있습니다. 구성 파일을 사용할 때 매개 변수의 처리 순서는 다음과 같습니다.  
  
-   구성 파일이 패키지의 기본값을 덮어씁니다.  
  
-   명령줄 값이 구성 파일의 값을 덮어씁니다.  
  
 구성 파일을 사용하는 방법에 대한 자세한 내용은 [구성 파일을 사용하여 SQL Server 2016 설치](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md)를 참조하세요.  
  
> [!IMPORTANT]  
>  Distributed Replay를 설치한 후에는 컨트롤러 및 클라이언트 컴퓨터에서 방화벽 규칙을 만들고 각 클라이언트 컴퓨터에 대상 서버에 대한 권한을 부여해야 합니다. 자세한 내용은 [설치 후 단계 완료](../../tools/distributed-replay/complete-the-post-installation-steps.md)를 참조하세요.  
  
#### <a name="to-generate-a-configuration-file"></a>구성 파일을 생성하려면  
  
1.  설치 마법사의 안내에 따르면 **설치 준비 완료** 페이지가 표시됩니다. 구성 파일의 경로는 **설치 준비 완료** 페이지의 구성 파일 경로 섹션에 지정됩니다.  
  
2.  설치를 실제로 완료하지는 않고 INI 파일을 생성하기 위해 설치를 취소합니다.  
  
#### <a name="to-install-distributed-replay-using-the-configuration-file"></a>구성 파일을 사용하여 Distributed Replay를 설치하려면  
  
-   명령 프롬프트에서 설치를 실행하고 ConfigurationFile 매개 변수를 사용하여 ConfigurationFile.ini를 입력합니다.  
  
 **예제 구문**  
  
 다음 예에서는 명령 프롬프트에서 구성 파일을 지정하는 방법을 보여 줍니다.  
  
```
Setup.exe /CTLRSVCPASSWORD="ctlrsvcpswd" /CLTSVCPASSWORD="cltsvcpswd" / ConfigurationFile=ConfigurationFile.INI\  
```

> [!NOTE]
> 구성 파일에서는 암호를 구성할 수 없으므로 명령줄에서 두 암호를 모두 지정해야 합니다.  

## <a name="see-also"></a>참고 항목

- [SQL Server 2016 버전에서 지원되는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)
- [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)
- [Distributed Replay 요구 사항](../../tools/distributed-replay/distributed-replay-requirements.md)
- [관리 도구 명령줄 옵션&#40;Distributed Replay Utility&#41;](../../tools/distributed-replay/administration-tool-command-line-options-distributed-replay-utility.md)
- [Distributed Replay 구성](../../tools/distributed-replay/configure-distributed-replay.md)