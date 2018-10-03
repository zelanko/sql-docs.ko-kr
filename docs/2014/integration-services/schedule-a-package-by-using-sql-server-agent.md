---
title: SQL Server 에이전트를 사용 하 여 패키지 예약 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 3d389cce-05af-4e1d-b684-7bbff413c806
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b0d955078772767804b625e1fb560e8cd0d15683
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48201981"
---
# <a name="schedule-a-package-by-using-sql-server-agent"></a>SQL Server 에이전트를 사용하여 패키지 예약
  다음 절차에서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에이전트 작업 단계를 통해 패키지 실행을 자동화하여 패키지를 실행하는 단계를 제공합니다.  
  
### <a name="to-automate-package-execution-by-using-sql-server-agent"></a>SQL Server 에이전트를 사용하여 패키지 실행을 자동화하려면  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 작업을 만들려는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스 또는 단계를 추가하려는 작업을 포함하는 인스턴스에 연결합니다.  
  
2.  개체 탐색기에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에이전트 노드를 확장하고 다음 태스크 중 하나를 수행합니다.  
  
    -   새 작업을 추가하려면 **작업** 을 마우스 오른쪽 단추로 클릭한 다음 **새 작업**을 클릭합니다.  
  
    -   기존 작업에 단계를 추가하려면 **작업**을 확장하고 해당 작업을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  새 작업을 만드는 경우 **일반** 페이지에서 작업 이름을 지정하고 소유자 및 작업 범주를 선택한 다음 필요에 따라 작업 설명을 지정합니다.  
  
4.  작업을 예약할 수 있게 설정하려면 **사용**을 선택합니다.  
  
5.  예약하려는 패키지에 대한 작업 단계를 만들려면 **단계**를 클릭한 다음 **새로 만들기**를 클릭합니다.  
  
6.  작업 단계 유형에 대한 **Integration Services 패키지** 를 선택합니다.  
  
7.  **다음 계정으로 실행** 목록에서 **SQL Server 에이전트 서비스 계정** 을 선택하거나 작업 단계에 사용될 자격 증명이 있는 프록시 계정을 선택합니다. 프록시 계정을 만드는 방법은 [Create a SQL Server Agent Proxy](../ssms/agent/create-a-sql-server-agent-proxy.md)를 참조하십시오.  
  
     **SQL Server 에이전트 서비스 계정** 대신 프록시 계정을 사용하면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에이전트를 사용하여 패키지를 실행할 때 발생할 수 있는 일반적인 문제를 해결할 수 있습니다. 이들 문제에 대한 자세한 정보는 [!INCLUDE[msCoName](../includes/msconame-md.md)] 기술 자료 문서 [SQL Server 에이전트 작업 단계에서 SSIS 패키지를 호출할 때 SSIS 패키지가 실행되지 않는다](http://support.microsoft.com/kb/918760)를 참고하십시오.  
  
    > [!NOTE]  
    >  프록시 계정에 사용하는 자격 증명의 암호가 변경되면 자격 증명 암호를 업데이트해야 합니다. 그렇지 않으면 작업 단계가 실패합니다.  
  
     SQL Server 에이전트 서비스 계정을 구성하는 방법에 대한 자세한 내용은 [SQL Server 에이전트의 서비스 시작 계정 설정&#40;SQL Server 구성 관리자&#41;](../relational-databases/sql-server-configuration-manager.md)을 참조하세요.  
  
8.  **패키지 원본** 목록 상자에서 패키지의 원본을 클릭하고 작업 단계의 옵션을 구성합니다.  
  
     **다음 표에서는 패키지 원본에 대해 설명합니다.**  
  
    |패키지 원본|Description|  
    |--------------------|-----------------|  
    |**SSIS 카탈로그**|SSISDB 데이터베이스에 저장된 패키지입니다. 패키지는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서버에 배포되는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트에 포함됩니다.|  
    |**SQL Server**|MSDB 데이터베이스에 저장된 패키지입니다. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스를 사용하여 패키지를 관리합니다.|  
    |**SSIS 패키지 저장소**|컴퓨터의 기본 폴더에 저장된 패키지입니다. 기본 폴더는 *\<drive>*:\Program Files\Microsoft SQL Server\110\DTS\Packages입니다. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스를 사용하여 패키지를 관리합니다.<br /><br /> 참고: [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 의 구성 파일을 수정하여 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]서비스에서 관리할 파일 시스템에 추가로 폴더를 지정하거나 다른 폴더를 지정할 수 있습니다. 자세한 내용은 [Integration Services 서비스 구성&#40;SSIS 서비스&#41;](service/integration-services-service-ssis-service.md)을 참조하세요.|  
    |**파일 시스템**|컴퓨터의 임의 폴더에 저장된 패키지입니다.|  
  
     **다음 표에서는 선택한 패키지 원본에 따라 작업 단계에 사용할 수 있는 구성 옵션을 설명합니다.**  
  
    > [!IMPORTANT]  
    >  패키지가 암호로 보호된 경우 **새 작업 단계** 대화 상자의 **일반** 페이지에 있는 ( **패키지** 탭을 제외한) 탭을 클릭하면 표시되는 **패키지 암호** 대화 상자에 암호를 입력해야 합니다. 그렇지 않으면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에이전트 작업은 패키지 실행에 실패합니다.  
  
     **패키지 원본**: SSIS 카탈로그  
  
    |탭|변수|  
    |---------|-------------|  
    |**패키지**|**Server**<br /><br /> SSISDB 카탈로그를 호스팅하는 데이터베이스 서버 인스턴스의 이름을 입력하거나 선택합니다.<br /><br /> **SSIS 카탈로그** 가 패키지 원본이면 Microsoft Windows 사용자 계정을 사용하여 서버에 로그온할 수 있습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증을 사용할 수 없습니다.|  
    ||**패키지**<br /><br /> 줄임표 단추를 클릭하고 패키지를 선택합니다.<br /><br /> **개체 탐색기** 에서 **Integration Services 카탈로그**노드의 하위 폴더에 있는 패키지를 선택합니다.|  
    |**매개 변수**<br /><br /> **구성** 탭에 위치합니다.|패키지에 포함된 매개 변수의 새 값을 입력합니다. 리터럴 값을 입력하거나 이미 매개 변수에 매핑한 서버 환경 변수에 포함된 값을 사용할 수 있습니다.  **\*\* 중요 \* \***  여러 환경에 포함 된 변수에 여러 매개 변수 및/또는 연결 관리자 속성 매핑한 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에이전트 오류 메시지를 표시 합니다. 지정된 실행의 경우 패키지는 단일 서버 환경에 포함된 값만으로 실행할 수 있습니다.<br /><br /> 리터럴 값을 입력하려면 매개 변수 옆에 있는 줄임표 단추를 클릭합니다. **실행할 리터럴 값 편집** 대화 상자가 나타납니다.<br /><br /> 환경 변수를 사용하려면 **환경** 을 클릭한 다음 사용하려는 변수를 포함하는 환경을 선택합니다.<br /><br /> <br /><br /> **매개 변수** 탭은 패키지를 디자인할 때 추가한 매개 변수를 표시합니다. 이때 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]를 사용하는 것도 방법이 될 수 있습니다. 탭은 패키지 배포 모델에서 프로젝트 배포 모델로 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 변환할 때 패키지에 추가된 매개 변수도 표시합니다. **Integration Services 프로젝트 변환 마법사** 를 사용하면 매개 변수로 패키지 구성을 바꿀 수 있습니다.<br /><br /> 서버 환경을 만들고 매개 변수에 변수를 매핑하는 방법에 대한 자세한 내용은 [서버 환경 만들기 및 매핑](../../2014/integration-services/create-and-map-a-server-environment.md)를 참조하세요.|  
    |**연결 관리자**<br /><br /> **구성** 탭에 위치합니다.|연결 관리자 속성의 값을 변경합니다. 예를 들어 서버 이름을 변경할 수 있습니다.<br /><br /> 연결 관리자 속성에 대한 매개 변수가 SSIS 서버에 자동으로 생성됩니다.<br /><br /> 속성 값을 변경하려면 리터럴 값을 입력하거나 이미 연결 관리자 속성에 매핑한 서버 환경 변수에 포함된 값을 사용할 수 있습니다. **\*\* 중요 \* \***  여러 환경에 포함 된 변수에 여러 매개 변수 및/또는 연결 관리자 속성 매핑한 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에이전트 오류 메시지를 표시 합니다. 지정된 실행의 경우 패키지는 단일 서버 환경에 포함된 값만으로 실행할 수 있습니다.<br /><br /> 리터럴 값을 입력하려면 매개 변수 옆에 있는 줄임표 단추를 클릭합니다. **실행할 리터럴 값 편집** 대화 상자가 나타납니다.<br /><br /> 환경 변수를 사용하려면 **환경** 을 클릭한 다음 사용하려는 변수를 포함하는 환경을 선택합니다.<br /><br /> <br /><br /> 서버 환경을 만들고 연결 관리자 속성에 변수를 매핑하는 방법에 대한 자세한 내용은 [서버 환경 만들기 및 매핑](../../2014/integration-services/create-and-map-a-server-environment.md)를 참조하세요.|  
    |**고급**<br /><br /> **구성** 탭에 위치합니다.|패키지 실행에 대해 다음과 같은 추가 설정을 구성합니다.<br /><br /> <br /><br /> **속성 재정의**: 클릭 **추가** 패키지 속성에 대 한 새 값을 입력 하 여 속성 경로 지정 하 고 속성 값을 중요 한지 여부를 나타냅니다. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서버는 중요한 데이터를 암호화합니다. 속성에 대한 설정을 편집하거나 제거하려면 **속성** 재정의 상자의 행을 클릭한 다음 **편집** 이나 **제거**를 클릭합니다. 합니다 **속성을 재정의** 옵션은의 이전 릴리스에서 업그레이드 된 구성 사용 하 여 패키지를 위한 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]합니다. [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] 를 사용하여 만들고 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서버에 배포한 패키지는 구성 대신 매개 변수를 사용합니다. 다음 중 하나를 수행하여 속성 경로를 찾을 수 있습니다.<br /><br /> XML 구성 파일에서 속성 경로 복사 (\*.dtsconfig) 파일입니다. 경로는 파일의 구성 섹션에 경로 속성의 값으로 나열됩니다. 다음은 MaximumErrorCount 속성에 대한 경로의 예입니다.<br /><br /> \Package.Properties[MaximumErrorCount]<br /><br /> **패키지 구성 마법사** 를 실행하고 마지막 **마법사 완료** 페이지에서 속성 경로를 복사합니다. 그런 다음 마법사를 취소할 수 있습니다.|  
    ||**로깅 수준**: 선택한 로깅 수준은 SSISDB 보기에 보고서에 표시 되는 정보를 결정 합니다 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서버. **성능** 또는 **자세한 정보** 로깅 수준을 선택하면 패키지 실행 성능에 영향을 줄 수 있습니다. 패키지 실행의 로깅 수준을 다음 중 하나를 선택 합니다.<br /><br /> **None**: 로깅이 해제 됩니다. 패키지 실행 상태에만 기록됩니다.<br /><br /> **기본**: 사용자 지정 및 진단 이벤트 외의 모든 이벤트가 기록 됩니다. 로깅 수준의 기본값입니다.<br /><br /> **성능**: 성능 통계와 OnError 및 OnWarning 이벤트만 기록 됩니다.<br /><br /> **Verbose**: 사용자 지정 및 진단 이벤트를 비롯 한 모든 이벤트가 기록 됩니다.<br /><br /> 자세한 내용은 [SSIS 서버에서 패키지 실행에 대한 로깅 설정](../../2014/integration-services/enable-logging-for-package-execution-on-the-ssis-server.md)을 참조하세요.|  
    ||**오류 덤프**: 패키지의 실행 하는 동안 오류가 발생할 때 디버그 덤프 파일 생성 되는지 여부를 지정 합니다.<br /><br /> 이 파일은 문제를 해결하는 데 도움이 될 수 있는 패키지 실행에 대한 정보를 제공합니다.<br /><br /> 이 옵션을 선택하고 실행 중에 오류가 발생하면 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]는 .mdmp 파일(이진 파일) 및 .tmp 파일(텍스트 파일)을 만듭니다. 기본적으로 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]는 *\<drive>:* \Program Files\Microsoft SQL Server\110\Shared\ErrorDumps 폴더에 파일을 저장합니다.|  
    ||**32 비트 런타임을** 64 비트 버전의 64 비트 컴퓨터에서 32 비트 버전의 dtexec 유틸리티를 사용 하 여 패키지 실행 여부를 나타냅니다 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에이전트를 설치 합니다.<br /><br /> 예를 들어 64비트 버전에서 사용할 수 없는 네이티브 OLE DB 공급자를 패키지에서 사용하는 경우 32비트 버전의 dtexec를 사용하여 패키지를 실행해야 합니다. 자세한 내용은 [Integration Services에 대한 64비트 고려 사항](http://msdn.microsoft.com/library/ms141766\(SQL.105\).aspx)을 참조하십시오.<br /><br /> 기본적으로 **SQL Server Integration Services 패키지** 작업 단계 유형을 선택하면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에이전트는 시스템에서 자동으로 호출된 dtexec 유틸리티 버전을 사용하여 패키지를 실행합니다. 시스템은 컴퓨터 프로세서와 컴퓨터에서 실행 중인 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에이전트 버전에 따라 32비트 또는 64비트 버전 유틸리티를 호출합니다.|  
  
     **패키지 원본**:  SQL서버, SSIS 패키지 저장소 또는 파일 시스템  
  
     에 대 한 명령줄 옵션에 해당 하는 SQL Server, SSIS 패키지 저장소 또는 파일 시스템에 저장 된 패키지에 대해 설정할 수 있는 옵션의 대다수는 `dtexec` 명령 프롬프트 유틸리티입니다. 유틸리티와 명령줄 옵션에 대한 자세한 내용은 [dtexec Utility](packages/dtexec-utility.md)를 참조하십시오.  
  
    |탭|변수|  
    |---------|-------------|  
    |**패키지**<br /><br /> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssIS](../includes/ssis-md.md)] 패키지 저장소에 저장된 패키지의 탭 옵션입니다.|**Server**<br /><br /> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스에 대해 데이터베이스 서버 인스턴스의 이름을 입력하거나 선택합니다.|  
    ||**Windows 인증 사용**<br /><br /> Microsoft Windows 사용자 계정으로 서버에 로그온하려면 이 옵션을 선택합니다.|  
    ||**SQL Server 인증 사용**<br /><br /> 사용자가 지정한 로그인 이름과 암호를 사용하여 트러스트되지 않은 연결로부터 연결하면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 로그인 계정이 설정되었는지 및 지정한 암호가 전에 기록한 암호와 일치하는지를 확인하여 인증을 수행합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서 로그인 계정을 찾을 수 없으면 인증이 실패하고 오류 메시지가 나타납니다.|  
    ||**사용자 이름**|  
    ||**암호**|  
    ||**패키지**<br /><br /> 줄임표 단추를 클릭하고 패키지를 선택합니다.<br /><br /> **개체 탐색기** 에서 **저장된 패키지**노드의 하위 폴더에 있는 패키지를 선택합니다.|  
    |**패키지**<br /><br /> 파일 시스템에 저장된 패키지의 탭 옵션입니다.|**패키지**<br /><br /> 패키지 파일의 전체 경로를 입력하거나 줄임표 단추를 클릭한 다음 패키지를 선택합니다.|  
    |**구성**|특정 구성으로 패키지를 실행할 XML 구성 파일을 추가합니다. 패키지 구성을 사용하여 런타임 시 패키지 속성 값을 업데이트합니다.<br /><br /> 이 옵션에 해당 하는 **/ConfigFile** 에 대 한 옵션 `dtexec`합니다.<br /><br /> 패키지 구성이 적용되는 방법을 이해하려면 [Package Configurations](../../2014/integration-services/package-configurations.md)을 참조하십시오. 패키지 구성을 만드는 방법은 [Create Package Configurations](../../2014/integration-services/create-package-configurations.md)를 참조하십시오.|  
    |**명령 파일**|사용 하 여 실행 하려는 추가 옵션을 지정 `dtexec`, 별도 파일에 있습니다.<br /><br /> 예를 들어 패키지를 실행하는 동안 하나 이상의 지정된 이벤트가 발생하는 경우 디버그 덤프 파일을 생성하려면 /Dump *errorcode* 옵션을 포함하는 파일을 포함할 수 있습니다.<br /><br /> **명령 파일** 옵션을 사용하면 여러 파일을 만들어서 적절한 파일을 지정하는 방법으로 한 패키지에 대해 다른 옵션 집합을 실행할 수 있습니다.<br /><br /> **명령 파일** 옵션에 해당 합니다 `/CommandFile` 에 대 한 옵션 `dtexec`합니다.|  
    |**데이터 원본**|패키지에 포함된 연결 관리자를 봅니다. 연결 문자열을 수정하려면 연결 관리자를 클릭하고 연결 문자열을 클릭합니다.<br /><br /> 이 옵션에 해당 하는 `/Connection` 에 대 한 옵션 `dtexec`합니다.|  
    |**실행 옵션**|**유효성 검사 경고 발생 시 패키지 실패**<br /> 경고 메시지가 오류로 간주되는지 여부를 나타냅니다. 이 옵션을 선택하고 유효성 검사 중 경고가 발생하면 패키지는 유효성 검사 중 실패합니다. 이 옵션에 해당 하는 `/WarnAsError` 에 대 한 옵션 `dtexec`합니다.<br /><br /> **패키지를 실행하지 않고 유효성 검사**<br /> 유효성 검사 단계 후에 실제로 패키지를 실행하지 않고 패키지 실행을 중지할지 여부를 나타냅니다. 이 옵션에 해당 하는 `/Validate` 에 대 한 옵션 `dtexec`합니다.<br /><br /> **MacConcurrentExecutables 속성 무시**<br /> 패키지에서 동시에 실행할 수 있는 실행 파일 수를 지정합니다. -1 값은 패키지가 실행할 수 있는 최대 파일 수가 패키지를 실행하는 컴퓨터의 프로세서 총 수에 2를 더한 값과 같음을 의미합니다. 이 옵션에 해당 하는 `/MaxConcurrent` 에 대 한 옵션 `dtexec`합니다.<br /><br /> **패키지 검사점 사용**<br /> 패키지 실행 중 검사점 사용 여부를 나타냅니다. 자세한 내용은 [검사점을 사용하여 패키지 다시 시작](packages/restart-packages-by-using-checkpoints.md)을 참조하세요.<br /><br /> 이 옵션은 `/CheckPointing`의 `dtexec` 옵션에 해당합니다.<br /><br /> **다시 시작 옵션 무시**<br /> 에 대 한 새 값이 설정 되었는지를 나타냅니다는 `CheckpointUsage` 패키지의 속성입니다. **다시 시작 옵션** 목록 상자에서 값을 선택합니다.<br /><br /> 이 옵션에 해당 하는 `/Restart` 에 대 한 옵션 `dtexec`합니다.<br /><br /> **32비트 런타임 사용**<br /> 64비트 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에이전트가 설치된 64비트 컴퓨터에서 32비트 버전의 dtexec 유틸리티를 사용하는 패키지의 실행 여부를 나타냅니다.<br /><br /> 예를 들어 64비트 버전에서 사용할 수 없는 네이티브 OLE DB 공급자를 패키지에서 사용하는 경우 32비트 버전의 dtexec를 사용하여 패키지를 실행해야 합니다. 자세한 내용은 [Integration Services에 대한 64비트 고려 사항](http://msdn.microsoft.com/library/ms141766\(SQL.105\).aspx)을 참조하십시오.<br /><br /> 기본적으로 **SQL Server Integration Services 패키지** 작업 단계 유형을 선택하면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에이전트는 시스템에서 자동으로 호출된 dtexec 유틸리티 버전을 사용하여 패키지를 실행합니다. 시스템은 컴퓨터 프로세서와 컴퓨터에서 실행 중인 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에이전트 버전에 따라 32비트 또는 64비트 버전 유틸리티를 호출합니다.|  
    |**로깅**|로그 공급자를 패키지 실행과 연결합니다.<br /><br /> **텍스트 파일용 SSIS 로그 공급자**<br /> ASCII 텍스트 파일에 로그 항목을 기록합니다.<br /><br /> **SQL Server용 SSIS 로그 공급자**<br /> MSDB 데이터베이스의 sysssislog 테이블에 로그 항목을 기록합니다.<br /><br /> **SQL Server Profiler용 SSIS 로그 공급자**<br /> SQL Server 프로파일러를 사용하여 볼 수 있는 추적 정보를 기록합니다.<br /><br /> **Windows 이벤트 로그용 SSIS 로그 공급자**<br /> Windows 이벤트 로그의 응용 프로그램 로그에 로그 항목을 기록합니다.<br /><br /> **XML 파일용 SSIS 로그 공급자**<br /> XML 파일에 로그 파일을 기록합니다.<br /><br /> 텍스트 파일, XML 파일 및 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 프로파일러 로그 공급자의 경우 패키지에 포함된 파일 연결 관리자를 선택합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 로그 공급자의 경우 패키지에 포함된 OLE DB 연결 관리자를 선택합니다.<br /><br /> 이 옵션에 해당 하는 `/Logger` 에 대 한 옵션 `dtexec`합니다.|  
    |**값 설정**|패키지 속성 설정을 재정의합니다. **속성** 상자에서 **속성 경로** 및 **값** 열에 값을 입력합니다. 속성 하나에 대한 값을 입력하면, **속성** 상자에 빈 행이 나타나고 다른 속성에 대한 값을 입력할 수 있게 됩니다.<br /><br /> 속성 상자에서 속성을 제거하려면 행을 클릭한 다음 **제거**를 클릭합니다.<br /><br /> 다음 중 하나를 수행하여 속성 경로를 찾을 수 있습니다.<br /><br /> XML 구성 파일에서 속성 경로 복사 (\*.dtsconfig) 파일입니다. 경로는 파일의 구성 섹션에 경로 속성의 값으로 나열됩니다. 다음은 MaximumErrorCount 속성에 대한 경로의 예입니다.<br /><br /> \Package.Properties[MaximumErrorCount]<br /><br /> **패키지 구성 마법사** 를 실행하고 마지막 **마법사 완료** 페이지에서 속성 경로를 복사합니다. 그런 다음 마법사를 취소할 수 있습니다.|  
    |**확인**|**서명된 패키지만 실행**<br /> 패키지 서명 확인 여부를 나타냅니다. 패키지가 서명되지 않았거나 서명이 잘못된 경우 패키지가 실패합니다. 이 옵션에 해당 하는 `/VerifySigned` 에 대 한 옵션 `dtexec`합니다.<br /><br /> **패키지 빌드 확인**<br /> 패키지의 빌드 번호가 이 옵션 옆에 있는 **빌드** 상자에 입력된 빌드 번호와 비교하여 검증되었는지를 나타냅니다. 일치하지 않을 경우 패키지가 실행되지 않습니다. 이 옵션에 해당 하는 `/VerifyBuild` 에 대 한 옵션 `dtexec`합니다.<br /><br /> **패키지 ID 확인**<br /> 패키지의 GUID가 이 옵션 옆에 있는 **패키지 ID** 상자에 입력된 package ID와 비교하여 검증되었는지를 나타냅니다. 이 옵션에 해당 하는 `/VerifyPackageID` 에 대 한 옵션 `dtexec`합니다.<br /><br /> **버전 ID 확인**<br /> 패키지의 버전 GUID가 이 옵션 옆에 있는 **버전 ID** 상자에 입력된 버전 ID와 비교하여 검증되었는지를 나타냅니다. 이 옵션에 해당 하는 `/VerifyVersionID` 에 대 한 옵션 `dtexec`합니다.|  
    |**명령줄**|dtexec의 명령줄 옵션을 수정합니다. 옵션에 대한 자세한 내용은 [dtexec Utility](packages/dtexec-utility.md)를 참조하십시오.<br /><br /> 팁: 명령 프롬프트 창에 명령줄을 복사를 수 추가 `dtexec`, 명령줄에서 패키지를 실행 합니다. 이렇게 하면 명령줄 텍스트를 쉽게 만들 수 있습니다.<br /><br /> **원래 옵션 복원**<br /> **작업 단계 속성**대화 상자의 **패키지**, **구성**, **명령 파일**, **데이터 원본**, **실행 옵션**, **로깅**, **값 설정** , **확인** 탭에 설정한 명령줄 옵션을 사용합니다.<br /><br /> **수동으로 명령 편집**<br /> **명령줄** 상자에 명령줄 옵션을 추가로 입력합니다.<br /><br /> 작업 단계에 변경한 내용을 저장하기 위해 **확인** 을 클릭하기 전에 **원래 옵션 복원** 을 클릭하면 **명령줄**상자에 추가로 입력한 옵션을 모두 삭제할 수 있습니다.|  
  
9. **확인** 을 클릭하여 설정을 저장하고 **새 작업 단계** 대화 상자를 닫습니다.  
  
    > [!NOTE]  
    >  **SSIS 카탈로그**에 저장된 패키지의 경우 해결되지 않은 매개 변수 또는 연결 관리자 속성 설정이 있으면 **확인** 단추가 비활성화됩니다. 해결되지 않은 설정은 서버 환경 변수에 포함된 값을 사용하여 매개 변수나 속성을 설정하는 경우 다음 조건 중 하나를 충족하면 발생합니다.  
    >   
    >  -   **구성** 탭의 **환경** 확인란이 선택되어 있지 않습니다.  
    > -   변수를 포함하는 서버 환경이 **구성** 탭의 목록 상자에 선택되어 있지 않습니다.  
  
10. 작업 단계 일정을 만들려면 **페이지 선택** 창에서 **일정** 을 클릭합니다. 일정 구성 방법에 대한 자세한 정보는 [Schedule a Job](../ssms/agent/schedule-a-job.md)을 참조하십시오.  
  
    > [!TIP]  
    >  일정에 이름을 지정할 때 다른 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에이전트 일정과 쉽게 구분할 수 있도록 고유하고 설명이 포함된 이름을 사용하는 것이 좋습니다.  
  
## <a name="see-also"></a>관련 항목  
 [프로젝트 및 패키지 실행](packages/run-integration-services-ssis-packages.md)  
  
  
