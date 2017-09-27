---
title: "dtexec 유틸리티 | Microsoft Docs"
ms.custom: 
ms.date: 08/26/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7b6867fa-1039-49b3-90fb-85b84678a612
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: f76aa1cfbcad38e383abca8a79005b3851767e2a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/21/2017

---
# <a name="dtexec-utility"></a>dtexec 유틸리티
  **dtexec** 명령 프롬프트 유틸리티는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 구성 및 실행하는 데 사용합니다. **dtexec** 유틸리티에서는 매개 변수, 연결, 속성, 변수, 로깅, 진행률 표시기 등의 모든 패키지 구성 및 실행 기능에 액세스할 수 있습니다. **dtexec** 유틸리를 사용하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버, .ispac 프로젝트 파일, [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스, [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 저장소, 파일 시스템의 원본에서 패키지를 로드할 수 있습니다.  
  
> **참고:** 최신 버전의 **dtexec** 유틸리티를 사용하여 이전 버전의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]로 만든 패키지를 실행하면 유틸리티가 패키지를 최신 패키지 형식으로 일시적으로 업그레이드합니다. 그러나 **dtexec** 유틸리티를 사용하여 업그레이드된 패키지를 저장할 수는 없습니다. 패키지를 영구적으로 최신 버전으로 업그레이드하는 방법은 [Upgrade Integration Services Packages](../../integration-services/install-windows/upgrade-integration-services-packages.md)를 참조하십시오.  
  
 이 항목은 다음과 같은 섹션으로 구성됩니다.  
  
-   [Integration Services 서버 및 프로젝트 파일](#server)  
  
-   [64비트 컴퓨터에서의 설치 고려 사항](#bit)  
  
-   [병렬 설치 컴퓨터에 대한 고려 사항](#side)  
  
-   [실행 단계](#phases)  
  
-   [반환된 종료 코드](#exit)  
  
-   [구문 규칙](#syntaxRules)  
  
-   [xp_cmdshell에서 dtexec 사용](#cmdshell)  
  
-   [구문](#syntax)  
  
-   [매개 변수](#parameter)  
  
-   [주의](#remark)  
  
-   [예](#example)  
  
##  <a name="server"></a> Integration Services 서버 및 프로젝트 파일  
 **dtexec**를 사용하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에서 패키지를 실행하는 경우 **dtexec**는 [catalog.create_execution&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md), [catalog.set_execution_parameter_value&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md) and [catalog.start_execution&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md) 저장 프로시저를 호출하여 실행을 만들고, 매개 변수 값을 설정하고, 실행을 시작합니다. 실행 로그는 관련 뷰의 서버에서 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 사용 가능한 표준 보고서를 사용하여 볼 수 있습니다. 보고서에 대한 자세한 내용은 [Integration Services 서버를 위한 보고서](../../integration-services/performance/monitor-running-packages-and-other-operations.md#reports)를 참조하세요.  
  
 다음은 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에서의 패키지 실행 예입니다.  
  
```  
DTExec /ISSERVER "\SSISDB\folderB\Integration Services Project17\Package.dtsx" /SERVER "." /Envreference 2 /Par "$Project::ProjectParameter(Int32)";1 /Par "Parameter(Int32)";21 /Par "CM.sqlcldb2.SSIS_repro.InitialCatalog";ssisdb /Par "$ServerOption::SYNCHRONIZED(Boolean)";True  
```  
  
 **dtexec** 를 사용하여 .ispac 프로젝트 파일에서 패키지를 실행할 경우 이와 관련하여 프로젝트 경로와 프로젝트 스트림 이름을 지정하는 데 사용하는 /Proj[ect] 및 /Pack[age] 옵션이 있습니다. **에서** Integration Services 프로젝트 변환 마법사 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 실행하여 프로젝트를 프로젝트 배포 모델로 변환할 경우 마법사가 .ispac 프로젝트 파일을 생성합니다. 자세한 내용은 참조 [배포할 Integration Services (SSIS) 프로젝트 및 패키지](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)합니다.  
  
 타사 일정 도구와 함께 **dtexec** 를 사용하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포되는 패키지를 예약할 수 있습니다.  
  
##  <a name="bit"></a> 64비트 컴퓨터에서의 설치 고려 사항  
 64비트 컴퓨터의 경우 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 는 64비트 버전의 **dtexec** 유틸리티(dtexec.exe)를 설치합니다. 특정 패키지를 32비트 모드로 실행해야 하는 경우 **dtexec** 유틸리티의 32비트 버전을 설치해야 합니다. 32비트 버전의 **dtexec** 유틸리티를 설치하려면 설치 도중 클라이언트 도구 또는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 를 선택해야 합니다.  
  
 기본적으로 64비트 및 32비트 버전의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 명령 프롬프트 유틸리티가 모두 설치되어 있는 64비트 컴퓨터는 명령 프롬프트에서 32비트 버전을 실행합니다. 64비트 버전에 대한 디렉터리 경로 앞에 32비트 버전에 대한 디렉터리 경로가 PATH 환경 변수에 나타나기 때문에 32비트 버전이 실행됩니다. (일반적으로 32 비트 디렉터리 경로 * \<드라이브 >*: 파일 (x86) server\110\dts\binn 이며 64 비트 디렉터리 경로 \Program * \<드라이브 >*: files\microsoft SQL Server\110\DTS\Binn입니다.)  
  
> **참고:** SQL Server 에이전트를 사용하여 유틸리티를 실행하는 경우 SQL Server 에이전트는 64비트 버전의 유틸리티를 자동으로 사용합니다. SQL Server 에이전트는 PATH 환경 변수가 아닌 레지스트리를 사용하여 유틸리티에 대한 올바른 실행 파일을 찾습니다.  
  
 명령 프롬프트에서 64비트 버전의 유틸리티를 실행하기 위해 다음 동작 중 하나를 수행할 수 있습니다.  
  
-   명령 프롬프트 창을 열고 64 비트 버전의 유틸리티가 포함 되어 있는 디렉터리로 변경 합니다 (*\<드라이브 >*: files\microsoft SQL Server\110\DTS\Binn)를 다음 해당 위치에서 유틸리티를 실행 합니다.  
  
-   전체 경로 입력 하 여 명령 프롬프트 유틸리티를 실행 (*\<드라이브 >*: files\microsoft SQL Server\110\DTS\Binn)를 64 비트 버전의 유틸리티가 있습니다.  
  
-   64 비트 경로 배치 하 여 PATH 환경 변수에서의 경로 순서를 영구적으로 변경 (*\<드라이브 >*: files\microsoft SQL Server\110\DTS\Binn) 앞의 32 비트 경로 (*\<드라이브 >*: \ \ 프로그램 파일 (x86) \Microsoft SQL Server\110\DTS\Binn) 변수에 합니다.  
  
##  <a name="side"></a> 병렬 설치 컴퓨터에 대한 고려 사항  
 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 또는 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] 가 설치된 컴퓨터에 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 를 설치하면 여러 버전의 **dtexec** 유틸리티가 설치됩니다.  
  
 명령 프롬프트 유틸리티의 전체 경로 입력 하 여 실행에 올바른 버전의 유틸리티를 실행 하려면 (*\<드라이브 >*: files\microsoft SQL Server\\< 버전\>\DTS\Binn).  
  
##  <a name="phases"></a> 실행 단계  
 이 유틸리티를 실행하면 다음 4단계가 수행됩니다.  
  
1.  명령을 읽어들이는 단계: 명령 프롬프트는 지정된 옵션 및 인수 목록을 읽습니다. **/?** 또는 **/HELP** 옵션이 있으면 이후의 모든 단계를 건너뜁니다.  
  
2.  패키지 로드 단계: **/SQL**, **/FILE**또는 **/DTS** 옵션으로 지정된 패키지가 로드됩니다.  
  
3.  구성 단계: 옵션은 다음 순서로 처리됩니다.  
  
    -   패키지 플래그, 변수 및 속성을 설정하는 옵션  
  
    -   패키지 버전 및 빌드를 확인하는 옵션  
  
    -   보고와 같은 유틸리티의 런타임 동작을 구성하는 옵션  
  
4.  유효성 검사 및 실행 단계: 패키지가 실행됩니다. **/VALIDATE** 옵션을 지정한 경우에는 실행되지 않고 유효성이 검사됩니다.  
  
##  <a name="exit"></a> 반환된 종료 코드  
 **dtexec 유틸리티에서 반환된 종료 코드**  
  
 패키지를 실행하면 **dtexec** 에서 종료 코드를 반환할 수 있습니다. 종료 코드는 ERRORLEVEL 변수를 채우는 데 사용되며 이 변수의 값은 배치 파일 내의 분기 논리 또는 조건문에서 테스트될 수 있습니다. 다음 표에서는 **dtexec** 종료 시 유틸리티에서 설정할 수 있는 값을 나열합니다.  
  
|Value|설명|  
|-----------|-----------------|  
|0|패키지가 성공적으로 실행되었습니다.|  
|1.|패키지가 실패했습니다.|  
|3|사용자가 패키지를 취소했습니다.|  
|4|유틸리티에서 요청된 패키지를 찾을 수 없습니다. 패키지를 찾을 수 없습니다.|  
|5|유틸리티에서 요청된 패키지를 로드할 수 없습니다. 패키지를 로드할 수 없습니다.|  
|6|유틸리티의 명령줄에서 내부 구문 오류 또는 의미 체계 오류가 발생했습니다.|  
  
##  <a name="syntaxRules"></a> 구문 규칙  
 **유틸리티 구문 규칙**  
  
 모든 옵션은 슬래시(/) 또는 빼기 기호(-)로 시작해야 합니다. 여기에 표시된 옵션은 슬래시(/)로 시작하지만 빼기 기호(-)를 대신 사용할 수 있습니다.  
  
 인수에 공백이 있는 경우 따옴표로 묶어야 합니다. 인수를 따옴표로 묶지 않으면 인수에 공백을 사용할 수 없습니다.  
  
 따옴표로 묶인 문자열 안의 큰따옴표는 이스케이프된 작은따옴표를 나타냅니다.  
  
 암호를 제외한 옵션 및 인수는 대/소문자를 구분하지 않습니다.  
  
##  <a name="cmdshell"></a> xp_cmdshell에서 dtexec 사용  
 **xp_cmdshell에서 dtexec 사용**  
  
 **xp_cmdshell** 프롬프트에서 dtexec를 실행할 수 있습니다. 다음 예에서는 UpsertData.dtsx라는 패키지를 실행하고 반환 코드를 무시하는 방법을 보여 줍니다.  
  
```  
EXEC xp_cmdshell 'dtexec /f "C:\UpsertData.dtsx"'  
```  
  
 다음 예에서는 동일한 패키지를 실행하고 반환 코드를 캡처하는 방법을 보여 줍니다.  
  
```  
DECLARE @returncode int  
EXEC @returncode = xp_cmdshell 'dtexec /f "C:\UpsertData.dtsx"'  
```  
  
> **중요!!** [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 기본적으로 새 설치에 대해 **xp_cmdshell** 옵션을 사용할 수 없습니다. 이 옵션은 **sp_configure** 시스템 저장 프로시저를 실행하여 사용할 수 있습니다. 자세한 내용은 [xp_cmdshell 서버 구성 옵션](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md)을 참조하세요.  
  
##  <a name="syntax"></a> 구문  
  
```  
dtexec /option [value] [/option [value]]...  
```  
  
##  <a name="parameter"></a> 매개 변수  
  
-   **/?** [*option_name*]: (옵션). 지정된 *option_name* 에 대한 명령 프롬프트 옵션 또는 도움말을 표시하고 유틸리티를 닫습니다.  
  
     *option_name* 인수를 지정하면 **dtexec** 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서를 시작하고 dtexec 유틸리티 항목을 표시합니다.  
  
-   **/Ca[llerInfo]**: (옵션). 패키지 실행에 대한 추가 정보를 지정합니다. SQL Server 에이전트를 사용하여 패키지를 실행할 때 에이전트는 패키지 실행이 SQL Server 에이전트로 호출되었음을 나타내도록 이 인수를 설정합니다. **dtexec** 유틸리티를 명령줄에서 실행할 경우에는 이 매개 변수가 무시됩니다.  
  
-   **/CheckF[ile]** *filespec*: (옵션). 패키지의 **CheckpointFileName** 속성을 *filespec*에 지정된 경로와 파일로 설정합니다. 이 파일은 패키지를 다시 시작할 때 사용됩니다. 이 옵션을 지정하고 파일 이름 값을 제공하지 않으면 패키지의 **CheckpointFileName** 이 빈 문자열로 설정됩니다. 이 옵션을 지정하지 않으면 패키지의 값이 유지됩니다.  
  
-   **/CheckP[ointing]** *{on\off}* : (옵션). 패키지 실행 중 패키지에서 검사점을 사용하는지 여부를 결정하는 값을 설정합니다. **on** 값에서는 실패한 패키지를 다시 실행합니다. 실패한 패키지가 다시 실행되면 런타임 엔진에서 검사점 파일을 사용하여 실패한 지점에서 패키지를 다시 시작합니다.  
  
     값을 지정하지 않고 이 옵션을 선언할 경우 기본값은 on입니다. 값을 on으로 설정한 경우 검사점 파일을 찾을 수 없으면 패키지를 실행할 수 없습니다. 이 옵션을 지정하지 않으면 패키지에 설정된 값이 유지됩니다. 자세한 내용은 [Restart Packages by Using Checkpoints](../../integration-services/packages/restart-packages-by-using-checkpoints.md)을 참조하세요.  
  
     dtexec의 **/CheckPointing on** 옵션은 패키지의 **SaveCheckpoints** 속성을 True로 설정하고 **CheckpointUsage** 속성을 Always로 설정하는 것과 같습니다.  
  
-   **/Com[mandFile]** *filespec*: (옵션). **dtexec**와 함께 실행되는 명령 옵션을 지정합니다. *filespec* 에 지정된 파일을 열고 이 파일에서 EOF가 검색될 때까지 옵션을 읽습니다. *filespec* 는 텍스트 파일입니다. *filespec* 인수는 패키지 실행과 연관시킬 명령 파일의 이름과 경로를 지정합니다.  
  
-   **/Conf[igFile]** *filespec*: (옵션). 값을 추출할 구성 파일을 지정합니다. 이 옵션을 사용하면 패키지의 디자인 타임에 지정한 구성과 다르게 런타임 구성을 설정할 수 있습니다. 다른 구성 설정을 XML 구성 파일에 저장한 다음 패키지를 실행하기 전에 **ConfigFile** 옵션을 사용하여 이 설정을 로드할 수 있습니다.  
  
     **/ConfigFile** 옵션을 사용하면 디자인 타임에 지정하지 않은 추가 구성을 런타임에 로드할 수 있습니다. 그러나 디자인 타임에도 지정한 구성 값을 **/ConfigFile** 옵션을 사용하여 바꿀 수는 없습니다. 패키지 구성이 적용되는 방법을 이해하려면 [Package Configurations](../../integration-services/packages/package-configurations.md)을 참조하십시오.  
  
-   **/Conn[ection]** *id_or_name;connection_string [[;id_or_name;connection_string]…]*: (옵션). 이름 또는 GUID가 지정된 연결 관리자가 패키지에 있음을 지정하고 연결 문자열을 지정합니다.  
  
     이 옵션을 사용하려면 두 매개 변수 모두를 지정해야 합니다. 즉, *id_or_name* 인수에 연결 관리자 이름 또는 GUID를 제공하고 *connection_string* 인수에 올바른 연결 문자열을 지정해야 합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 연결](../../integration-services/connection-manager/integration-services-ssis-connections.md)을 참조하세요.  
  
     런타임에 **/Connection** 옵션을 사용하면 디자인 타임에 지정한 위치와 다른 위치에서 패키지 구성을 로드할 수 있습니다. 그러면 원래 지정된 값이 이러한 구성 값으로 바뀝니다. 그러나 연결 관리자를 사용하는 **구성과 같은 구성에만** /Connection [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 옵션을 사용할 수 있습니다. 패키지 구성이 적용되는 방법을 이해하려면 [패키지 구성](../../integration-services/packages/package-configurations.md) 및 [SQL Server 2016 Integration Services 기능의 동작 변경](http://msdn.microsoft.com/library/611d22fa-5ac7-485e-9a40-7131e852f794)을 참조하세요.  
  
-   **/Cons[oleLog]** [[*displayoptions*];[*list_options*;*src_name_or_guid*]...]: (옵션). 패키지 실행 중 지정된 로그 항목을 콘솔에 표시합니다. 이 옵션을 생략하면 콘솔에 로그 항목이 표시되지 않습니다. 표시를 제한하는 매개 변수 없이 이 옵션을 지정하면 모든 로그 항목이 표시됩니다. 콘솔에 표시되는 항목을 제한하려면 *displayoptions* 매개 변수를 사용하여 표시할 열을 지정하고 *list_options* 매개 변수를 사용하여 로그 항목 유형을 제한합니다.  
  
    > **참고:** [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에서 **/ISSERVER** 매개 변수를 사용하여 패키지를 실행할 경우 콘솔 출력이 제한되며 대부분의 **/Cons[oleLog]** 옵션이 적용되지 않습니다. 실행 로그는 관련 뷰의 서버에서 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 사용 가능한 표준 보고서를 사용하여 볼 수 있습니다. 보고서에 대한 자세한 내용은 [Integration Services 서버를 위한 보고서](../../integration-services/performance/monitor-running-packages-and-other-operations.md#reports)를 참조하세요.  
  
     *displayoptions* 값은 다음과 같습니다.  
  
    -   N(이름)  
  
    -   C(컴퓨터)  
  
    -   O(운영자)  
  
    -   S(원본 이름)  
  
    -   G(원본 GUID)  
  
    -   X(실행 GUID)  
  
    -   M(메시지)  
  
    -   T(시간 시작 및 종료 시간)  
  
     *list_options* 값은 다음과 같습니다.  
  
    -   *I* - 포함 목록을 지정합니다. 지정된 원본 이름 또는 GUID만 로깅됩니다.  
  
    -   *E* - 제외 목록을 지정합니다. 지정된 원본 이름 또는 GUID가 로깅되지 않습니다.  
  
    -   포함 또는 제외하도록 지정된 *src_name_or_guid* 매개 변수는 이벤트 이름, 원본 이름 또는 원본 GUID입니다.  
  
     같은 명령 프롬프트에 여러 **/ConsoleLog** 옵션을 사용하면 다음과 같이 작동합니다.  
  
    -   시각적인 순서에는 영향을 주지 않습니다.  
  
    -   명령줄에 포함 목록이 없으면 모든 유형의 로그 항목에 제외 목록이 적용됩니다.  
  
    -   명령줄에 포함 목록이 있으면 모든 포함 목록의 집합에 제외 목록이 적용됩니다.  
  
     **/ConsoleLog** 옵션에 관한 여러 가지 예는 **주의** 섹션을 참조하세요.  
  
-   **/D[ts](/sql-docs/docs/integration-services/packages/deploy-integration-services-ssis-projects-and-packages)합니다.  
  
     *package_path* 인수는 SSIS 패키지 저장소의 루트에서 시작하여 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지의 상대 경로를 지정하고 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지의 이름을 포함합니다. *package_path* 인수에 지정된 경로나 파일 이름에 공백이 있는 경우 *package_path* 인수를 따옴표로 묶어야 합니다.  
  
     **/DTS** 옵션은 **/File** 또는 **/SQL** 옵션과 함께 사용할 수 없습니다. 여러 개의 옵션을 지정하는 경우 **dtexec** 는 실패합니다.  
  
-   **/De[crypt]**  *password*: (옵션). 암호가 암호화된 패키지를 로드할 때 사용할 해독 암호를 설정합니다.  
  
-   선택 사항입니다. 패키지가 실행되는 동안 하나 이상의 지정된 이벤트가 발생할 때 디버그 덤프 파일(.mdmp 및 .tmp)을 만듭니다. *error code* 인수는 시스템에서 디버그 덤프 파일을 만들도록 트리거할 이벤트 코드 유형(오류, 경고 또는 정보)을 지정합니다. 여러 이벤트 코드를 지정하려면 각 *error code* 인수를 세미콜론(;)으로 구분합니다. 이때 *error code* 인수를 따옴표로 묶으면 안 됩니다.  
  
     다음 예에서는 DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER 오류가 발생할 때 디버그 덤프 파일을 생성합니다.  
  
    ```  
    /Dump 0xC020801C  
    ```  
  
     **/Dump** *오류 코드*: 기본적으로 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 폴더에서 디버그 덤프 파일을 저장 * \<드라이브 >*: files\microsoft SQL Server\110\Shared\ErrorDumps 합니다.  
  
    > **참고:** 디버그 덤프 파일에는 중요한 정보가 들어 있을 수 있습니다. ACL(액세스 제어 목록)을 사용하여 파일에 대한 액세스를 제한하거나 파일을 액세스가 제한된 폴더에 복사합니다. 예를 들어 디버그 파일을 Microsoft 지원 서비스에 보내기 전에 중요한 정보나 기밀 정보를 제거하는 것이 좋습니다.  
  
     **dtexec** 유틸리티가 실행하는 모든 패키지에 이 옵션을 적용하려면 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\SSIS\Setup\DtsPath 레지스트리 키에 **DumpOnCodes** REG_SZ 값을 추가합니다. **DumpOnCodes** 의 데이터 값은 시스템에서 디버그 덤프 파일을 만들도록 트리거할 오류 코드를 지정합니다. 여러 오류 코드를 지정하려면 세미콜론(;)으로 구분해야 합니다.  
  
     레지스트리 키에 **DumpOnCodes** 값을 추가하고 **/Dump** 옵션을 사용하는 경우 시스템에서 두 설정을 기반으로 디버그 덤프 파일을 만듭니다.  
  
     디버그 덤프 파일에 대한 자세한 내용은 [Generating Dump Files for Package Execution](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)을 참조하십시오.  
  
-   **/DumpOnError**: (옵션) 패키지가 실행되는 동안 오류가 발생할 때 디버그 덤프 파일(.mdmp 및 .tmp)을 만듭니다.  
  
     기본적으로 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 폴더에서 디버그 덤프 파일을 저장 * \<드라이브 >*: files\microsoft SQL Server\110\Shared\ErrorDumps 폴더입니다.  
  
    > **참고:** 디버그 덤프 파일에는 중요한 정보가 들어 있을 수 있습니다. ACL(액세스 제어 목록)을 사용하여 파일에 대한 액세스를 제한하거나 파일을 액세스가 제한된 폴더에 복사합니다. 예를 들어 디버그 파일을 Microsoft 지원 서비스에 보내기 전에 중요한 정보나 기밀 정보를 제거하는 것이 좋습니다.  
  
     **dtexec** 유틸리티가 실행하는 모든 패키지에 이 옵션을 적용하려면 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\SSIS\Setup\DtsPath 레지스트리 키에 **DumpOnError** REG_DWORD 값을 추가합니다. **DumpOnError** REG_DWORD 값은 **dtexec** 유틸리티에 **/DumpOnError** 옵션을 사용해야 하는지 여부를 결정합니다.  
  
    -   0이 아닌 데이터 값은 **dtexec** 유틸리티에 **/DumpOnError** 옵션을 사용하는지 여부와 관계없이 오류가 발생할 때 시스템에서 디버그 덤프 파일을 만듦을 나타냅니다.  
  
    -   0 데이터 값은 **dtexec** 유틸리티에 **/DumpOnError** 옵션을 사용하지 않는 한 시스템에서 디버그 덤프 파일을 만들지 않음을 나타냅니다.  
  
     디버그 덤프 파일에 대한 자세한 내용은 [Generating Dump Files for Package Execution](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)을 참조하십시오.  
  
-   **/Env[Reference]** *environment reference ID*: (옵션). [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포된 패키지에 대해 패키지 실행에서 사용되는 환경 참조(ID)를 지정합니다. 변수에 바인딩하도록 구성된 매개 변수는 환경에 포함된 변수 값을 사용합니다.  
  
     **/Env[Reference]** 옵션은 **/ISServer** 및 **/Server** 옵션과 함께 사용합니다.  
  
     이 매개 변수는 SQL Server 에이전트에서 사용됩니다.  
  
-   * * /F[ile](/sql-docs/docs/integration-services/packages/deploy-integration-services-ssis-projects-and-packages)  
  
     *filespec* 인수는 패키지의 경로와 파일 이름을 지정합니다. 경로는 UNC(Universal Naming Convention) 경로나 로컬 경로로 지정할 수 있습니다. *filespec* 인수에 지정된 경로나 파일 이름에 공백이 있는 경우 *filespec* 인수를 따옴표로 묶어야 합니다.  
  
     **/File** 옵션은 **/DTS** 또는 **/SQL** 옵션과 함께 사용할 수 없습니다. 여러 개의 옵션을 지정하는 경우 **dtexec** 는 실패합니다.  
  
-   **/H[elp]** [*option_name*]: (옵션). 옵션에 대한 도움말 또는 지정된 *option_name* 에 대한 도움말을 표시하고 유틸리티를 닫습니다.  
  
     *option_name* 인수를 지정하면 **dtexec** 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서를 시작하고 dtexec 유틸리티 항목을 표시합니다.  
  
-   **/ISServer** *packagepath*: (옵션). [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포된 패키지를 실행합니다. *PackagePath* 인수는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포된 패키지의 전체 경로 및 파일 이름을 지정합니다. *PackagePath* 인수에 지정된 경로나 파일 이름에 공백이 있는 경우 *PackagePath* 인수를 따옴표로 묶어야 합니다.  
  
     패키지 형식은 다음과 같습니다.  
  
    ```  
    \<catalog name>\<folder name>\<project name>\package file name  
    ```  
  
     **/Server** 옵션은 **/ISSERVER** 옵션과 함께 사용합니다. Windows 인증만 SSIS 서버에서 패키지를 실행할 수 있습니다. 현재 Windows 사용자는 패키지에 액세스하는 데 사용됩니다. /Server 옵션을 생략할 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 기본 로컬 인스턴스가 사용됩니다.  
  
     **/ISSERVER** 옵션은 **/DTS**, **/SQL** 또는 **/File** 옵션과 함께 사용할 수 없습니다. 여러 개의 옵션을 지정하는 경우 dtexec는 실패합니다.  
  
     이 매개 변수는 SQL Server 에이전트에서 사용됩니다.  
  
-   **/L[ogger]** *classid_orprogid;configstring*: (옵션). [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 실행에 하나 이상의 로그 공급자를 연결합니다. *classid_orprogid* 매개 변수는 로그 공급자를 지정하며 클래스 GUID로 지정될 수 있습니다. *configstring* 은 로그 공급자를 구성하는 데 사용되는 문자열입니다.  
  
     다음 목록에서는 사용 가능한 로그 공급자를 보여 줍니다.  
  
    -   텍스트 파일:  
  
        -   ProgID: DTS.LogProviderTextFile.1  
  
        -   ClassID: {59B2C6A5-663F-4C20-8863-C83F9B72E2EB}  
  
    -   [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]:  
  
        -   ProgID: DTS.LogProviderSQLProfiler.1  
  
        -   ClassID: {5C0B8D21-E9AA-462E-BA34-30FF5F7A42A1}  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
        -   ProgID: DTS.LogProviderSQLServer.1  
  
        -   ClassID: {6AA833A1-E4B2-4431-831B-DE695049DC61}  
  
    -   Windows 이벤트 로그:  
  
        -   ProgID: DTS.LogProviderEventLog.1  
  
        -   ClassID: {97634F75-1DC7-4F1F-8A4C-DAF0E13AAA22}  
  
    -   XML 파일:  
  
        -   ProgID: DTS.LogProviderXMLFile.1  
  
        -   ClassID: {AFED6884-619C-484F-9A09-F42D56E1A7EA}  
  
-   **/M[axConcurrent]** *concurrent_executables*: (옵션). 패키지에서 동시에 실행할 수 있는 실행 파일 수를 지정합니다. 값은 음수가 아닌 정수 또는 -1로 지정해야 합니다. -1 값은 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 에서 패키지를 실행하는 컴퓨터의 총 프로세서 수에 2를 더한 값과 같은 동시에 실행 가능한 최대 실행 파일 수를 허용함을 의미합니다.  
  
-   **/Pack[age]** *PackageName*: (옵션). 실행되는 패키지를 지정합니다. 이 매개 변수는 주로 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]에서 패키지를 실행할 때 사용됩니다.  
  
-   **/P[assword]** *password*: (옵션). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증으로 보호되는 패키지를 검색할 수 있도록 합니다. 이 옵션은 **/User** 옵션과 함께 사용합니다. **/Password** 옵션을 생략하고 **/User** 옵션을 사용하면 빈 암호가 사용됩니다. *password* 값은 따옴표로 묶을 수 있습니다.  
  
    > **중요!!** [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
-   **/Par[ameter]** [$Package:: | $Project:: | $ServerOption::] *parameter_name* [(data_type)]; *literal_value*: (옵션). 매개 변수 값을 지정합니다. 여러 **/Parameter** 옵션을 지정할 수 있습니다. 데이터 형식은 문자열인 CLR TypeCodes입니다. 문자열이 아닌 매개 변수의 경우 데이터 형식은 매개 변수 이름 다음에 괄호로 지정됩니다.  
  
     **/Parameter** 옵션은 **/ISServer** 옵션과 함께 사용해야 합니다.  
  
     $Package, $Project 및 $ServerOption 접두사는 각각 패키지 매개 변수, 프로젝트 매개 변수 및 서버 옵션 매개 변수를 나타내기 위해 사용합니다. 기본 매개 변수 유형은 패키지입니다.  
  
     다음은 패키지를 실행하고 프로젝트 매개 변수(myparam)에 대해 myvalue를 제공하고 패키지 매개 변수(anotherparam)에 대해 정수 값 12를 제공하는 예입니다.  
  
     `Dtexec /isserver “SSISDB\MyFolder\MyProject\MyPackage.dtsx” /server “.” /parameter $Project::myparam;myvalue /parameter anotherparam(int32);12`  
  
     매개 변수를 사용하여 연결 관리자 속성을 설정할 수도 있습니다. CM 접두사를 사용하여 연결 관리자 매개 변수를 나타냅니다.  
  
     다음 예에서 SourceServer 연결 관리자의 InitialCatalog 속성은 `ssisdb`로 설정됩니다.  
  
    ```  
    /parameter CM.SourceServer.InitialCatalog;ssisdb  
    ```  
  
     다음 예에서는 SourceServer 연결 관리자의 ServerName 속성을 마침표(.)로 설정하여 로컬 서버를 지정합니다.  
  
    ```  
    /parameter CM.SourceServer.ServerName;.  
    ```  
  
-   **/Proj[ect]** *ProjectFile*: (옵션). 실행되는 패키지를 검색할 프로젝트를 지정합니다. *ProjectFile* 인수는 .ispac 파일 이름을 지정합니다. 이 매개 변수는 주로 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]에서 패키지를 실행할 때 사용됩니다.  
  
-   **/Rem** *comment*: (옵션). 명령 프롬프트 또는 명령 파일에 설명을 포함합니다. 이 인수는 선택 사항입니다. *comment* 값은 따옴표로 묶여 있거나 공백이 없는 문자열이어야 합니다. 인수를 지정하지 않으면 빈 줄이 삽입됩니다. *comment* 값은 명령을 읽어 들이는 단계를 수행하는 동안 삭제됩니다.  
  
-   **/Rep[orting]** *level* [*;event_guid_or_name*[*;event_guid_or_name*[...]]: (옵션). 보고할 메시지의 유형을 지정합니다. *level* 에 대해 사용할 수 있는 보고 옵션은 다음과 같습니다.  
  
     **N** - 보고하지 않습니다.  
  
     **E** - 오류를 보고합니다.  
  
     **W** - 경고를 보고합니다.  
  
     **I** - 정보 메시지를 보고합니다.  
  
     **C** - 사용자 지정 이벤트를 보고합니다.  
  
     **D** - 데이터 흐름 태스크 이벤트를 보고합니다.  
  
     **P** - 진행률을 보고합니다.  
  
     **V** - 자세한 사항을 보고합니다.  
  
     V 및 N 인수는 다른 인수와 함께 사용할 수 없으므로 단독으로 지정해야 합니다. **/Reporting** 옵션을 지정하지 않을 경우 기본 수준은 **E** (오류), **W** (경고) 및 **P** (진행 상황)입니다.  
  
     모든 이벤트 앞에는 "YY/MM/DD HH:MM:SS" 형식의 타임스탬프가 있으며 GUID 또는 이름이 옵니다(사용 가능한 경우).  
  
     선택적 매개 변수 *event_guid_or_name* 은 로그 공급자에 대한 예외 목록입니다. 예외는 정상적인 상황에서는 기록되어야 하지만 기록되지 않는 이벤트를 지정합니다.  
  
     기본적으로 기록되지 않는 경우에는 이벤트를 제외시킬 필요가 없습니다.  
  
-   **/Res[tart]** {*deny | force | ifPossible*}: (옵션). 패키지에서 <xref:Microsoft.SqlServer.Dts.Runtime.Package.CheckpointUsage%2A> 속성의 새 값을 지정합니다. 매개 변수의 의미는 다음과 같습니다.  
  
     *거부* 집합 <xref:Microsoft.SqlServer.Dts.Runtime.Package.CheckpointUsage%2A> 속성을 <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSCheckpointUsage.DTSCU_NEVER>합니다.  
  
     *Force* 집합 <xref:Microsoft.SqlServer.Dts.Runtime.Package.CheckpointUsage%2A> 속성을 <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSCheckpointUsage.DTSCU_ALWAYS>합니다.  
  
     *ifPossible* 집합 <xref:Microsoft.SqlServer.Dts.Runtime.Package.CheckpointUsage%2A> 속성을 <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSCheckpointUsage.DTSCU_IFEXISTS>합니다.  
  
     값을 지정하지 않으면 기본값인 **force** 가 사용됩니다.  
  
-   **/Set** [$Sensitive::]*propertyPath;value*: (옵션). 패키지에서 매개 변수, 변수, 속성, 컨테이너, 로그 공급자, Foreach 열거자 또는 연결의 구성을 재지정합니다. 이 옵션을 사용하면 **/Set** 는 *propertyPath* 인수를 지정된 값으로 변경합니다. 여러 **/Set** 옵션을 지정할 수 있습니다.  
  
     **/Set** 옵션을 **/F[ile]** 옵션과 함께 사용하는 것 외에도 **/Set** 옵션을 **/ISServer** 옵션 또는 **/Project** 옵션과 함께 사용할 수 있습니다. **/Set** 를 **/Project**와 함께 사용할 경우 **/Set** 는 매개 변수 값을 설정합니다. **/Set** 를 **/ISServer**와 함께 사용할 경우에는 **/Set** 가 속성 재정의를 설정합니다. 또한 **/Set** 를 **/ISServer**와 함께 사용하는 경우 선택적인 $Sensitive 접두사를 사용하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에서 이 속성을 중요한 속성으로 처리하도록 표시할 수 있습니다.  
  
     패키지 구성 마법사를 실행하여 *propertyPath* 의 값을 확인할 수 있습니다. 선택한 항목의 경로는 마지막 **마법사 완료** 페이지에 표시되며 복사하여 붙여넣을 수 있습니다. 이러한 용도로만 마법사를 사용하는 경우에는 경로를 복사한 다음 마법사를 취소할 수 있습니다.  
  
     다음은 파일 시스템에 저장된 패키지를 실행하고 변수에 새 값을 제공하는 예입니다.  
  
     `dtexec /f mypackage.dtsx /set \package.variables[myvariable].Value;myvalue`  
  
     다음은 .ispac 프로젝트 파일에서 패키지를 실행하고 패키지 및 프로젝트 매개 변수를 설정하는 예입니다.  
  
     `/Project c:\project.ispac /Package Package1.dtsx /SET \Package.Variables[$Package::Parameter];1 /SET \Package.Variables[$Project::Parameter];1`  
  
     **/Set** 옵션을 사용하면 패키지 구성이 로드되는 위치를 변경할 수 있습니다. 그러나 디자인 타임에 구성으로 지정한 값은 **/Set** 옵션을 사용하여 재정의할 수 없습니다. 패키지 구성이 적용되는 방법을 이해하려면 [패키지 구성](../../integration-services/packages/package-configurations.md) 및 [SQL Server 2016 Integration Services 기능의 동작 변경](http://msdn.microsoft.com/library/611d22fa-5ac7-485e-9a40-7131e852f794)을 참조하세요.  
  
-   **/Ser[ver]** *server*: (옵션). **/SQL** 또는 **/DTS** 옵션을 지정한 경우 이 옵션은 패키지를 검색할 서버의 이름을 지정합니다. **/Server** 옵션을 생략하고 **/SQL** 또는 **/DTS** 옵션을 지정하면 로컬 서버에 대해 패키지가 실행됩니다. *server_instance* 값은 따옴표로 묶을 수 있습니다.  
  
     **/ISServer** 옵션이 지정된 경우 **/Ser[ver]** 옵션이 필요합니다.  
  
-   * * /SQ[L](/sql-docs/docs/integration-services/packages/deploy-integration-services-ssis-projects-and-packages)합니다.  
  
     *package_path* 인수는 검색할 패키지의 이름을 지정합니다. 경로에 폴더가 포함된 경우 백슬래시("\\")로 끝납니다. *package_path* 값은 따옴표로 묶을 수 있습니다. *package_path* 인수에 지정된 경로나 파일 이름에 공백이 있는 경우 *package_path* 인수를 따옴표로 묶어야 합니다.  
  
     **/SQL**옵션과 함께 **/User**, **/Password** , **/Server** 옵션을 사용할 수 있습니다.  
  
     **/User** 옵션을 생략하면 패키지에 액세스하는 데 Windows 인증이 사용됩니다. **/User** 옵션을 사용하면 지정된 **/User** 로그인 이름이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증과 연결됩니다.  
  
     **/Password** 옵션은 **/User** 옵션과 함께 사용해야 합니다. **/Password** 옵션을 사용할 경우 패키지는 제공된 사용자 이름 및 암호 정보로 액세스합니다. **/Password** 옵션을 생략하면 빈 암호가 사용됩니다.  
  
    > **중요!!** [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
     **/Server** 옵션을 생략할 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 기본 로컬 인스턴스가 사용됩니다.  
  
     **/SQL** 옵션은 **/DTS** 또는 **/File** 옵션과 함께 사용할 수 없습니다. 여러 개의 옵션을 지정하는 경우 **dtexec** 는 실패합니다.  
  
-   **/Su[m]**: (옵션). 다음 구성 요소에서 받을 행 수를 포함하는 증분 카운터를 표시합니다.  
  
-   **/U[ser]** *user_name*: (옵션). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증으로 보호되는 패키지를 검색할 수 있도록 합니다. 이 옵션은 **/SQL** 옵션을 지정한 경우에만 사용합니다. *user_name* 값은 따옴표로 묶을 수 있습니다.  
  
    > **중요!!**  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
-   **/Va[lidate]**: (옵션). 유효성 검사 단계 후에 실제로 패키지를 실행하지 않고 패키지 실행을 중지합니다. **/WarnAsError** 옵션을 사용하면 유효성 검사 중 **dtexec** 에서 경고를 오류로 간주하므로 유효성 검사 중 경고가 발생하면 패키지가 실패합니다.  
  
-   **/VerifyB[uild]** *major*[*;minor*[*;build*]]: (옵션). 확인 단계 동안 *major*, *minor*및 *build* 인수에 지정된 빌드 번호에 대해 패키지의 빌드 번호를 확인합니다. 일치하지 않을 경우 패키지가 실행되지 않습니다.  
  
     값은 정수(Long)입니다. 인수의 형식으로 3가지 중 하나를 사용할 수 있으며 *major* 값은 항상 필요합니다.  
  
    -   *major*  
  
    -   *major*;*minor*  
  
    -   *major*; *minor*; *build*  
  
-   **/VerifyP[ackageID]** *packageID*: (옵션). 실행할 패키지의 GUID를 *package_id* 인수에 지정된 값과 비교하여 확인합니다.  
  
-   **/VerifyS[igned]**: (옵션). [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 가 패키지의 디지털 서명을 확인하도록 합니다. 패키지가 서명되지 않았거나 서명이 잘못된 경우 패키지가 실패합니다. 자세한 내용은 [디지털 서명을 사용하여 패키지 원본 확인](../../integration-services/security/identify-the-source-of-packages-with-digital-signatures.md)을 참조하세요.  
  
    > **중요!!** 패키지의 서명을 확인하도록 구성된 경우 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 는 디지털 서명이 있는지, 유효한지, 그리고 신뢰할 수 있는 원본에서 제공된 것인지만 확인합니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 는 패키지가 변경되었는지 여부는 확인하지 않습니다.  
  
    > **참고:** 선택적 **BlockedSignatureStates** 레지스트리 값은 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 또는 **dtexec** 명령줄에서 설정한 디지털 서명 옵션보다 더 제한적인 설정을 지정할 수 있습니다. 이 경우 더 제한적인 설정이 다른 설정보다 우선합니다.  
  
-   **/VerifyV[ersionID]** *versionID*: (옵션). 패키지 유효성 검사 단계 동안 실행할 패키지의 버전 GUID를 *version_id* 인수에 지정된 값과 비교하여 확인합니다.  
  
-   **/VLog** *[Filespec]*: (옵션). 패키지를 디자인할 때 사용하도록 설정한 로그 공급자에 모든 Integration Services 패키지 이벤트를 기록합니다. Integration Services가 텍스트 파일용 로그 공급자를 사용하고 지정된 텍스트 파일에 로그 이벤트를 기록하도록 만들려면 경로 및 파일 이름을 *Filespec* 매개 변수로 포함합니다.  
  
     *Filespec* 매개 변수를 포함하지 않으면 Integration Services가 텍스트 파일용 로그 공급자를 사용하지 않습니다. Integration Services는 패키지를 디자인할 때 사용하도록 설정한 로그 공급자에만 로그 이벤트를 기록합니다.  
  
-   **/W[arnAsError]**: (옵션). 패키지에서 경고를 오류로 간주하도록 하므로 유효성 검사 동안 경고가 발생하면 패키지가 실패합니다. 유효성 검사 동안 경고가 발생하지 않았고 **/Validate** 옵션을 지정하지 않은 경우 패키지가 실행됩니다.  
  
-   **/X86**: (옵션). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 64비트 컴퓨터에서 32비트 모드로 패키지를 실행하도록 합니다. 이 옵션은 다음 조건이 충족되는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 설정됩니다.  
  
    -   작업 단계 유형이 **SQL Server Integration Services 패키지**입니다.  
  
    -   **새 작업 단계** 대화 상자의 **실행 옵션** 탭에서 **32비트 런타임 사용** 옵션이 선택되어 있습니다.  
  
     또한 저장 프로시저나 SMO(SQL Server 관리 개체)를 사용하여 프로그래밍 방식으로 작업을 만들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 단계에 대해 이 옵션을 설정할 수도 있습니다.  
  
     이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서만 사용됩니다. 명령 프롬프트에서 **dtexec** 유틸리티를 실행하는 경우에는 이 옵션이 무시됩니다.  
  
##  <a name="remark"></a> 주의  
 명령 옵션을 지정하는 순서에 따라 패키지 실행 방법이 달라질 수 있습니다.  
  
-   명령줄에 나타나는 순서대로 옵션이 처리됩니다. 명령줄에 명령 파일이 있으면 명령 파일을 읽습니다. 명령 파일의 명령도 나타나는 순서대로 처리됩니다.  
  
-   같은 명령줄 문에 같은 옵션, 매개 변수 또는 변수가 두 번 이상 나타나는 경우 마지막 옵션이 우선 순위를 갖습니다.  
  
-   **/Set** 및 **/ConfigFile** 옵션은 나타나는 순서대로 처리됩니다.  
  
##  <a name="example"></a> 예  
 다음 예에서는 **dtexec** 명령 프롬프트 유틸리티를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 구성 및 실행하는 방법을 보여 줍니다.  
  
 **패키지 실행**  
  
 Windows 인증을 사용하여 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 에 저장된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 패키지를 실행하려면 다음 코드를 사용합니다.  
  
```  
dtexec /sq pkgOne /ser productionServer  
```  
  
 SSIS 패키지 저장소의 파일 시스템 폴더에 저장된 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지를 실행하려면 다음 코드를 사용합니다.  
  
```  
dtexec /dts "\File System\MyPackage"  
```  
  
 Windows 인증을 사용하며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 저장된 패키지를 실행하지 않고 유효성을 검사하려면 다음 코드를 사용합니다.  
  
```  
dtexec /sq pkgOne /ser productionServer /va  
```  
  
 파일 시스템에 저장된 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지를 실행하려면 다음 코드를 사용합니다.  
  
```  
dtexec /f "c:\pkgOne.dtsx"   
```  
  
 파일 시스템에 저장된 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지를 실행하고 로깅 옵션을 지정하려면 다음 코드를 사용합니다.  
  
```  
dtexec /f "c:\pkgOne.dtsx" /l "DTS.LogProviderTextFile;c:\log.txt"  
```  
  
 Windows 인증을 사용하며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 기본 로컬 인스턴스에 저장된 패키지를 실행하려면 실행하기 전에 버전을 확인하고 다음 코드를 사용합니다.  
  
```  
dtexec /sq pkgOne /verifyv {c200e360-38c5-11c5-11ce-ae62-08002b2b79ef}  
```  
  
 파일 시스템에 저장되고 외부적으로 구성된 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지를 실행하려면 다음 코드를 사용합니다.  
  
```  
dtexec /f "c:\pkgOne.dtsx" /conf "c:\pkgOneConfig.cfg"  
```  
  
> **참고:** 경로나 파일 이름에 공백이 있는 경우 /SQL, /DTS 또는 /FILE 옵션의 *package_path* 또는 *filespec* 인수를 따옴표로 묶어야 합니다. 인수를 따옴표로 묶지 않으면 인수에 공백을 사용할 수 없습니다.  
  
 **로깅 옵션**  
  
 A, B, C라는 3개의 로그 항목 유형이 있는 경우 매개 변수가 없는 다음 **ConsoleLog** 옵션은 모든 필드와 함께 3개의 로그 유형을 모두 표시합니다.  
  
```  
/CONSOLELOG  
```  
  
 다음 옵션은 모든 로그 유형을 표시하지만 이름 및 메시지 열만 표시합니다.  
  
```  
/CONSOLELOG NM  
```  
  
 다음 옵션은 모든 열을 표시하지만 로그 항목 유형 A에 대해서만 표시합니다.  
  
```  
/CONSOLELOG I;LogEntryTypeA  
```  
  
 다음 옵션은 이름 및 메시지 열과 함께 로그 항목 유형 A만 표시합니다.  
  
```  
/CONSOLELOG NM;I;LogEntryTypeA  
```  
  
 다음 옵션은 로그 항목 유형 A와 B에 대한 로그 항목을 표시합니다.  
  
```  
/CONSOLELOG I;LogEntryTypeA;LogEntryTypeB  
```  
  
 여러 **ConsoleLog** 옵션을 사용하여 같은 결과를 얻을 수 있습니다.  
  
```  
/CONSOLELOG I;LogEntryTypeA /CONSOLELOG I;LogEntryTypeB  
```  
  
 **ConsoleLog** 옵션을 매개 변수 없이 사용하면 모든 필드가 표시됩니다. *list_options* 매개 변수를 포함하면 다음은 모든 필드와 함께 로그 항목 유형 A만 표시합니다.  
  
```  
/CONSOLELOG NM;I;LogEntryTypeA /CONSOLELOG  
```  
  
 다음 옵션은 로그 항목 유형 A를 제외한 모든 로그 항목(로그 항목 유형 B 및 C)을 표시합니다.  
  
```  
/CONSOLELOG E;LogEntryTypeA  
```  
  
 다음 예에서는 여러 **ConsoleLog** 옵션을 사용하고 하나를 제외하여 같은 결과를 얻습니다.  
  
```  
/CONSOLELOG E;LogEntryTypeA /CONSOLELOG  
/CONSOLELOG E;LogEntryTypeA /CONSOLELOG E;LogEntryTypeA  
/CONSOLELOG E;LogEntryTypeA;LogEntryTypeA  
```  
  
 로그 파일 종류가 포함 목록과 제외 목록 모두에 있는 경우 제외되므로 다음 예에서는 로그 메시지를 표시하지 않습니다.  
  
```  
/CONSOLELOG E;LogEntryTypeA /CONSOLELOG I;LogEntryTypeA  
```  
  
 **SET 옵션**  
  
 다음 예제에서는 명령줄에서 패키지를 시작하는 경우 모든 패키지의 속성 또는 변수 값을 변경할 수 있는 **/SET** 옵션을 사용하는 방법을 보여 줍니다.  
  
```  
/SET \package\DataFlowTask.Variables[User::MyVariable].Value;newValue  
```  
  
 **프로젝트 옵션**  
  
 다음 예제에서는 **/Project** 및 **/Package** 옵션을 사용하는 방법을 보여 줍니다.  
  
```  
/Project c:\project.ispac /Package Package1.dtsx  
```  
  
 다음 예제에서는 **/Project** 및 **/Package** 옵션을 사용하고 패키지 및 프로젝트 매개 변수를 설정하는 방법을 보여 줍니다.  
  
```  
/Project c:\project.ispac /Package Package1.dtsx /SET \Package.Variables[$Package::Parameter];1 /SET \Package.Variables[$Project::Parameter];1  
  
```  
  
 **ISServer 옵션**  
  
 다음 예제에서는 **/ISServer** 옵션을 사용하는 방법을 보여 줍니다.  
  
```  
dtexec /isserver "\SSISDB\MyFolder\MyProject\MyPackage.dtsx" /server "."  
```  
  
 다음 예제에서는 **/ISServer** 옵션을 사용하여 프로젝트 및 연결 관리자 매개 변수를 설정하는 방법을 보여 줍니다.  
  
```  
/Server localhost /ISServer “\SSISDB\MyFolder\Integration Services Project1\Package.dtsx” /Par "$Project::ProjectParameter(Int32)";1 /Par "CM.SourceServer.InitialCatalog";SourceDB  
  
```  
  
## <a name="related-content"></a>관련 내용  
 www.mattmasson.com의 [종료 코드, DTEXEC 및 SSIS 카탈로그](http://www.mattmasson.com/2012/02/exit-codes-dtexec-and-ssis-catalog/)블로그 항목  
  
  

