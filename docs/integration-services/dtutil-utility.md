---
description: Encrypt
title: dtutil 유틸리티 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- verifying packages
- checking packages
- moving packages
- packages [Integration Services], command line options
- command prompt [Integration Services]
- SQL Server Integration Services packages, command line options
- copying packages
- existence testing [Integration Services]
- Integration Services packages, command line options
- SSIS packages, command line options
- deleting packages
- dtutil utility
- removing packages
- relocating packages
ms.assetid: 6c7975ff-acec-4e6e-82e5-a641e3a98afe
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 41d40f419497ccb2917052ac477c888a9338c135
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92195265"
---
# <a name="dtutil-utility"></a>Encrypt

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


  **dtutil** 명령 프롬프트 유틸리티를 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지를 관리합니다. 이 유틸리티는 패키지를 복사, 이동, 삭제하거나 패키지가 있는지 여부를 확인할 수 있습니다. 해당 동작은 [!INCLUDE[ssIS](../includes/ssis-md.md)] [!INCLUDE[msCoName](../includes/msconame-md.md)] 데이터베이스, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 패키지 저장소 및 파일 시스템의 세 위치 중 하나에 저장된 [!INCLUDE[ssIS](../includes/ssis-md.md)] 패키지에서 수행할 수 있습니다. 유틸리티가 **msdb**에 저장된 패키지에 액세스하는 경우 명령 프롬프트에 사용자 이름과 암호를 입력해야 할 수 있습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증을 사용하면 사용자 이름과 암호를 모두 입력해야 합니다. 사용자 이름이 누락된 경우 **dtutil** 은 Windows 인증을 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에 로그온하려고 시도합니다. 패키지 스토리지 유형은 **/SQL**, **/FILE**및 **/DTS** 옵션으로 식별됩니다.  
  
 **dtutil** 명령 프롬프트 유틸리티는 명령 파일이나 리디렉션 사용을 지원하지 않습니다.  
  
 **dtutil** 명령 프롬프트 유틸리티에는 다음과 같은 기능이 있습니다.  
  
-   명령 프롬프트의 설명은 명령 프롬프트 동작을 자동으로 문서화하여 쉽게 이해할 수 있게 해줍니다.  
  
-   덮어쓰기 보호는 패키지를 복사하거나 이동할 때 기존 패키지를 덮어쓰기 전에 확인 메시지를 표시합니다.  
  
-   콘솔 도움말은 **dtutil**명령 옵션에 대한 정보를 제공합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 인스턴스에 연결된 경우에는 dtutil에서 수행하는 대부분의 작업을 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]에서도 시각적으로 수행할 수 있습니다. 자세한 내용은 [패키지 관리&#40;SSIS 서비스&#41;](../integration-services/service/package-management-ssis-service.md)를 참조하세요.  
  
 옵션은 순서에 관계없이 입력할 수 있습니다. 파이프("|") 문자는 **OR** 연산자이며 가능한 값을 표시하는 데 사용됩니다. **OR** 파이프로 구분된 옵션 중 하나를 사용해야 합니다.  
  
 모든 옵션은 슬래시(/) 또는 빼기 기호(-)로 시작해야 합니다. 단, 슬래시 또는 빼기 기호와 옵션 텍스트 사이에는 공백이 없어야 합니다. 그렇지 않으면 명령이 실패합니다.  
  
 인수는 따옴표로 묶거나 공백이 없는 문자열이어야 합니다.  
  
 작은따옴표로 묶인 문자열 안의 큰따옴표는 이스케이프된 작은따옴표를 나타냅니다.  
  
 암호를 제외한 옵션 및 인수는 대/소문자를 구분하지 않습니다.  
  
 **64비트 컴퓨터에서의 설치 고려 사항**  
  
 64비트 컴퓨터의 경우 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서 64비트 버전의 **dtexec** 유틸리티(dtexec.exe) 및 **dtutil** 유틸리티(dtutil.exe)를 설치합니다. 이러한 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 도구의 32비트 버전을 설치하려면 설치 도중 클라이언트 도구 또는 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 를 선택해야 합니다.  
  
 기본적으로 64비트 및 32비트 버전의 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 명령 프롬프트 유틸리티가 모두 설치되어 있는 64비트 컴퓨터는 명령 프롬프트에서 32비트 버전을 실행합니다. 64비트 버전에 대한 디렉터리 경로 앞에 32비트 버전에 대한 디렉터리 경로가 PATH 환경 변수에 나타나기 때문에 32비트 버전이 실행됩니다. 일반적으로 32비트 디렉터리 경로는 *\<drive>* :\Program Files(x86)\Microsoft SQL Server\130\DTS\Binn이고, 64비트 디렉터리 경로는 *\<drive>* :\Program Files\Microsoft SQL Server\130\DTS\Binn입니다.  
  
> [!NOTE]  
>  SQL Server 에이전트를 사용하여 유틸리티를 실행하는 경우 SQL Server 에이전트는 64비트 버전의 유틸리티를 자동으로 사용합니다. SQL Server 에이전트는 PATH 환경 변수가 아닌 레지스트리를 사용하여 유틸리티에 대한 올바른 실행 파일을 찾습니다.  
  
 명령 프롬프트에서 64비트 버전의 유틸리티를 실행하기 위해 다음 동작 중 하나를 수행할 수 있습니다.  
  
-   명령 프롬프트 창을 열고 64비트 버전의 유틸리티가 포함되어 있는 디렉터리 *(\<drive>* :\Program Files\Microsoft SQL Server\130\DTS\Binn)로 변경한 다음, 해당 위치에서 유틸리티를 실행합니다.  
  
-   명령 프롬프트에서 64비트 버전의 유틸리티에 대한 전체 경로( *\<drive>* :\Program Files\Microsoft SQL Server\130\DTS\Binn)를 입력하여 유틸리티를 실행합니다.  
  
-   PATH 환경 변수에서 32비트 경로( *\<drive>* :\ Program Files(x86)\Microsoft SQL Server\130\DTS\Binn) 앞에 64비트 경로( *\<drive>* :\Program Files\Microsoft SQL Server\130\DTS\Binn)를 배치하여 변수에서의 경로 순서를 영구적으로 변경합니다.  
  
## <a name="syntax"></a>구문  
  
```dos
dtutil /option [value] [/option [value]]...  
```  
  
#### <a name="parameters"></a>매개 변수  
  
|옵션|Description|  
|------------|-----------------|  
|/?|명령 프롬프트 옵션을 표시합니다.|  
|/C[opy] *location;destinationPathandPackageName*|[!INCLUDE[ssIS](../includes/ssis-md.md)] 패키지에 대해 Copy 동작을 지정합니다. 이 매개 변수를 사용하려면 먼저 **/FI**, **/SQ**또는 **/DT** 옵션을 사용하여 패키지 위치를 지정해야 합니다. 그런 다음 대상 위치 및 대상 패키지 이름을 지정합니다. *destinationPathandPackageName* 인수는 [!INCLUDE[ssIS](../includes/ssis-md.md)] 패키지를 복사할 대상 위치를 지정합니다. 대상 *location* 이 **SQL**인 경우 명령에 *DestUser*, *DestPassword* 및 *DestServer* 인수도 지정해야 합니다.<br /><br /> **Copy** 동작을 수행할 때 대상 위치에 기존 패키지가 있을 경우 **dtutil** 에서 패키지를 삭제할 것인지 묻는 메시지를 표시합니다. **Y** 로 응답하면 패키지를 덮어쓰고 **N** 으로 응답하면 프로그램을 종료합니다. 명령에 *Quiet* 인수가 포함된 경우 메시지가 표시되지 않으며 기존 패키지를 덮어씁니다.|  
|/Dec[rypt] *password*|(선택 사항). 암호가 암호화된 패키지를 로드할 때 사용할 해독 암호를 설정합니다.|  
|/Del[ete]|*SQL*, *DTS* 또는 *FILE* 옵션으로 지정된 패키지를 삭제합니다. **dtutil** 에서 패키지를 삭제할 수 없을 경우 프로그램이 종료됩니다.|  
|/DestP[assword] *password*|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증을 사용하는 대상 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 연결하기 위해 SQL 옵션에 사용할 암호를 지정합니다. *DESTPASSWORD* 옵션이 포함되지 않은 명령줄에서 *DTSUSER* 를 지정하면 오류가 생성됩니다.<br /><br /> 참고: [!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)].|  
|/DestS[erver] *server_instance*|대상이 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 저장되도록 하는 모든 동작에 사용할 서버 이름을 지정합니다. [!INCLUDE[ssIS](../includes/ssis-md.md)] 패키지를 저장할 때 로컬 서버나 기본 서버가 아닌 서버를 식별하는 데 사용됩니다. *와 관련된 동작이 없는 명령줄에서* DESTSERVER [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 지정하면 오류가 발생합니다. 이 옵션과 조합하여 사용할 수 있는 적합한 명령에는 *SIGN SQL*, *COPY SQL*또는 *MOVE SQL* 옵션과 같은 동작이 있습니다.<br /><br /> 서버 이름에 백슬래시 및 인스턴스 이름을 추가하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스 이름을 지정할 수 있습니다.|  
|/DestU[ser] *username*|*인증을 사용하는*인스턴스에 연결하기 위해 *SIGN SQL*, *COPY SQL* 및 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] MOVE SQL [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 옵션에 사용할 사용자 이름을 지정합니다. *DESTUSER* , *SIGN SQL*또는 *COPY SQL*옵션이 포함되지 않은 명령줄에서 *MOVE SQL* 를 지정하면 오류가 발생합니다.|  
|/Dump *process ID*|선택 사항이며, 이 옵션을 선택할 경우 지정된 프로세스 **dtexec** 유틸리티 또는 **dtsDebugHost.exe** 프로세스가 일시 중지되고 디버그 덤프 파일 .mdmp 및 .tmp가 만들어집니다.<br /><br /> 참고: **/Dump**옵션을 사용하려면 디버그 프로그램 사용자 권한(SeDebugPrivilege)을 할당받아야 합니다.<br /><br /> 일시 중지할 프로세스의 *process ID* 를 찾으려면 Windows 작업 관리자를 사용합니다.<br /><br /> 기본적으로 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]에서는 디버그 덤프 파일을 *\<drive>* :\Program Files\Microsoft SQL Server\130\Shared\ErrorDumps 폴더에 저장합니다.<br /><br /> **dtexec** 유틸리티 **dtsDebugHost.exe** 프로세스에 대한 자세한 내용은 [dtexec Utility](../integration-services/packages/dtexec-utility.md) 및 [Building, Deploying, and Debugging Custom Objects](../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)을 참조하십시오.<br /><br /> 디버그 덤프 파일에 대한 자세한 내용은 [Generating Dump Files for Package Execution](../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)을 참조하십시오.<br /><br /> 참고: 디버그 덤프 파일에는 중요한 정보가 들어 있을 수 있습니다. ACL(액세스 제어 목록)을 사용하여 파일에 대한 액세스를 제한하거나 파일을 액세스가 제한된 폴더에 복사합니다.|  
|/DT[S] *filespec*|사용할 [!INCLUDE[ssIS](../includes/ssis-md.md)] 패키지가 [!INCLUDE[ssIS](../includes/ssis-md.md)] 패키지 저장소에 있음을 지정합니다. *filespec* 인수는 [!INCLUDE[ssIS](../includes/ssis-md.md)] 패키지 저장소의 루트에서 시작하는 폴더 경로를 포함해야 합니다. 기본적으로 구성 파일에서 루트 폴더의 이름은 "MSDB" 및 "File System"입니다. 공백이 포함된 경로는 큰따옴표를 사용하여 구분해야 합니다.<br /><br /> 다음 옵션을 지정한 것과 동일한 명령줄에서 DT[S] 옵션을 지정하면 DTEXEC_DTEXECERROR가 반환됩니다.<br /><br /> **FILE**<br /><br /> **SQL**<br /><br /> **SOURCEUSER**<br /><br /> **SOURCEPASSWORD**<br /><br /> **SOURCESERVER**|  
|/En[crypt] *{SQL &#124; FILE}; Path;ProtectionLevel[;password]*|(선택 사항). 로드된 패키지를 지정된 보호 수준과 암호를 사용하여 암호화하고 *Path*에 지정된 위치에 저장합니다. *ProtectionLevel* 은 암호가 필요한지 여부를 결정합니다.<br /><br /> *SQL* - 경로는 대상 패키지 이름입니다.<br /><br /> *FILE* - 경로는 패키지의 정규화된 경로 및 파일 이름입니다.<br /><br /> *DTS* - 현재 이 옵션은 지원되지 않습니다.<br /><br /> *ProtectionLevel* 옵션:<br /><br /> 수준 0: 중요한 정보를 따로 암호화하지 않습니다.<br /><br /> 수준 1: 로컬 사용자 자격 증명을 사용하여 중요한 정보를 암호화합니다.<br /><br /> 수준 2: 필수 암호를 사용하여 중요한 정보를 암호화합니다.<br /><br /> 수준 3: 필수 암호를 사용하여 패키지를 암호화합니다.<br /><br /> 수준 4: 로컬 사용자 자격 증명을 사용하여 패키지를 암호화합니다.<br /><br /> 수준 5: 패키지에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 스토리지 암호화를 사용합니다.|  
|/Ex[ists]|(선택 사항). 패키지가 있는지 여부를 확인하는 데 사용됩니다. **dtutil** 은 *SQL*, *DTS* 또는 *FILE* 옵션을 사용하여 지정된 패키지를 찾으려고 시도합니다. **dtutil** 에서 지정된 패키지를 찾지 못할 경우 DTEXEC_DTEXECERROR가 반환됩니다.|  
|/FC[reate] {*SQL* &#124; *DTS*};*ParentFolderPath;NewFolderName*|(선택 사항). *NewFolderName*에 지정된 이름으로 새 폴더를 만듭니다. 새 폴더의 위치는 *ParentFolderPath*로 표시됩니다.|  
|/FDe[lete] {*SQL* &#124; *DTS*}[;*ParentFolderPath;FolderName]*|(선택 사항). [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssIS](../includes/ssis-md.md)] 에서 *FolderName*에 이름이 지정된 폴더를 삭제합니다. 삭제할 폴더의 위치는 *ParentFolderPath*로 표시됩니다.|  
|/FDi[rectory] {*SQL* &#124; *DTS*};*FolderPath[;S]*|(선택 사항). [!INCLUDE[ssIS](../includes/ssis-md.md)] 또는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 폴더에 있는 폴더와 패키지 모두의 내용을 나열합니다. 선택 사항인 *FolderPath* 매개 변수는 내용을 표시할 폴더를 지정합니다. 선택 사항인 *S* 매개 변수는 *FolderPath*에 지정된 폴더의 하위 폴더 내용 목록을 표시합니다.|  
|/FE[xists ] {*SQL* &#124; *DTS*};*FolderPath*|(선택 사항). 지정된 폴더가 [!INCLUDE[ssIS](../includes/ssis-md.md)] 또는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 있는지 확인합니다. *FolderPath* 매개 변수는 확인할 폴더의 경로와 이름입니다.|  
|/Fi[le] *filespec*|이 옵션은 사용할 [!INCLUDE[ssIS](../includes/ssis-md.md)] 패키지가 파일 시스템에 있음을 지정합니다. UNC(범용 명명 규칙) 경로나 로컬 경로로 *filespec* 값을 지정할 수 있습니다.<br /><br /> 다음 옵션과 동일한 명령줄에서 *File* 옵션을 지정하면 DTEXEC_DTEXECERROR가 반환됩니다.<br /><br /> **DTS**<br /><br /> **SQL**<br /><br /> **SOURCEUSER**<br /><br /> **SOURCEPASSWORD**<br /><br /> **SOURCESERVER**|  
|/FR[ename] {*SQL* &#124; *DTS*} [;*ParentFolderPath; OldFolderName;NewFolderName]*|(선택 사항). [!INCLUDE[ssIS](../includes/ssis-md.md)] 또는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 폴더 이름을 바꿉니다. *ParentFolderPath* 는 이름을 바꿀 폴더의 위치입니다. *OldFolderName* 은 폴더의 현재 이름이며 *NewFolderName* 은 폴더에 지정할 새 이름입니다.|  
|/H[elp] *option*|광범위한 내용을 다루는 도움말을 표시합니다. 이 도움말에서는 **dtutil** 옵션을 표시하고 그 사용 방법을 설명합니다. 옵션 인수는 선택 사항입니다. 이 인수를 포함할 경우 도움말 텍스트에는 지정된 옵션에 대한 자세한 내용이 포함됩니다. 다음 예에서는 모든 옵션에 대한 도움말을 표시합니다.<br /><br /> `dtutil /H`<br /><br /> 다음 두 예에서는 */H* 옵션을 사용하여 특정 옵션에 대한 자세한 도움말을 표시하는 방법을 보여 줍니다. 이 예에서 도움말을 표시할 특정 옵션은 */Q [uiet]* 입니다.<br /><br /> `dtutil /Help Quiet`<br /><br /> `dtutil /H Q`|  
|/I[DRegenerate]|패키지를 위한 새 GUID를 만들고 패키지 ID 속성을 업데이트합니다. 패키지를 복사해도 패키지 ID는 동일하게 유지되므로 로그 파일에는 두 패키지 모두에 대해 동일한 GUID가 포함됩니다. 이 동작은 새로 복사된 패키지에 대해 새 GUID를 만들어 원본과 구별합니다.|  
|/M[ove] {*SQL* &#124; *File* &#124; *DTS*}; *pathandname*|[!INCLUDE[ssIS](../includes/ssis-md.md)] 패키지에 대해 Move 동작을 지정합니다. 이 매개 변수를 사용하려면 먼저 **/FI**, **/SQ**또는 **/DT** 옵션을 사용하여 패키지 위치를 지정합니다. 그런 다음 **Move** 동작을 지정합니다. 이 동작에는 세미콜론으로 구분되는 두 인수가 필요합니다.<br /><br /> 대상 인수는 *SQL*, *FILE*또는 *DTS*를 지정할 수 있습니다. *SQL* 대상은 *DESTUSER*, *DESTPASSWORD*및 *DESTSERVER* 옵션을 포함할 수 있습니다.<br /><br /> *pathandname* 인수는 패키지 위치를 지정합니다. *SQL* 은 패키지 경로와 패키지 이름을 사용하고 *FILE* 은 UNC 또는 로컬 경로를 사용하며 *DTS* 는 [!INCLUDE[ssIS](../includes/ssis-md.md)] 패키지 저장소의 루트에 상대적인 위치를 사용합니다. 대상이 *FILE* 또는 *DTS*인 경우 path 인수에는 파일 이름이 포함되지 않습니다. 대신 지정된 위치의 패키지 이름을 파일 이름으로 사용합니다.<br /><br /> <br /><br /> **MOVE** 동작을 수행할 때 대상에 기존 패키지가 있을 경우 **dtutil** 에서 패키지를 덮어쓸 것인지 묻는 메시지를 표시합니다. **Y** 로 응답하면 패키지를 덮어쓰고 **N** 으로 응답하면 프로그램을 종료합니다. 명령에 *QUIET* 옵션이 포함된 경우 메시지가 표시되지 않으며 기존 패키지를 덮어씁니다.|  
|/Q[uiet]|**COPY**, **MOVE**또는 **SIGN** 옵션이 포함된 명령을 실행할 때 나타날 수 있는 확인 메시지를 표시하지 않습니다. 이 메시지는 지정된 패키지와 이름이 같은 패키지가 대상 컴퓨터에 이미 있을 경우 또는 지정된 패키지에 이미 서명이 된 경우 나타납니다.|  
|/R[emark] *text*|명령줄에 주석을 추가합니다. 주석 인수는 선택 사항입니다. 주석 텍스트에 공백이 포함된 경우 텍스트를 따옴표로 묶어야 합니다. 명령줄에 여러 REM 옵션을 포함할 수 있습니다.|  
|/Si[gn] {*SQL* &#124; *File* &#124; *DTS*}; *path*; *hash*|[!INCLUDE[ssIS](../includes/ssis-md.md)] 패키지에 서명합니다. 이 동작에서는 세미콜론으로 구분되는 세 인수(대상, path, hash)를 사용합니다.<br /><br /> 대상 인수는 *SQL*, *FILE*또는 *DTS*를 지정할 수 있습니다. SQL 대상은 *DESTUSER*, *DESTPASSWORD* 및 *DESTSERVER* 옵션을 포함할 수 있습니다.<br /><br /> path 인수는 동작을 수행할 패키지의 위치를 지정합니다.<br /><br /> hash 인수는 다양한 길이의 16진수 문자열로 표현되는 인증서 식별자를 지정합니다.<br /><br /> 자세한 내용은 [디지털 서명을 사용하여 패키지 원본 확인](../integration-services/security/identify-the-source-of-packages-with-digital-signatures.md)을 참조하세요.<br /><br /> <br /><br /> **\*\* 중요 \*\*** 패키지의 서명을 확인하도록 구성된 경우 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 는 디지털 서명이 있는지, 유효한지, 그리고 신뢰할 수 있는 원본에서 제공된 것인지만 확인합니다. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 는 패키지가 변경되었는지 여부는 확인하지 *않습니다* .|  
|/SourceP[assword] *password*|*인증을 사용하는* 인스턴스의 데이터베이스에 저장된 *패키지를 검색할 수 있도록* SQL [!INCLUDE[ssIS](../includes/ssis-md.md)] 및 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] SOURCEUSER [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 옵션에 사용할 암호를 지정합니다. *SOURCEUSER* 옵션이 포함되지 않은 명령줄에서 **SOURCEPASSWORD** 를 지정하면 오류가 발생합니다.<br /><br /> 참고: [!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)]|  
|/SourceS[erver] *server_instance*|**에 저장된** 패키지를 검색할 수 있도록 [!INCLUDE[ssIS](../includes/ssis-md.md)] SQL [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]옵션에 사용할 서버 이름을 지정합니다. *SIGN SQL*, *COPY* *SQL* 또는 *MOVE* *SQL* 옵션이 포함되지 않은 명령줄에서 *SOURCESERVER*를 지정하면 오류가 발생합니다.<br /><br /> 서버 이름에 백슬래시 및 인스턴스 이름을 추가하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스 이름을 지정할 수 있습니다.|  
|/SourceU[ser] *username*|*인증을 사용하는* 에 저장된 [!INCLUDE[ssIS](../includes/ssis-md.md)] 패키지를 검색할 수 있도록 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] SOURCESERVER [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 옵션에 사용할 사용자 이름을 지정합니다. *SOURCEUSER* , *SIGN SQL*또는 *COPY SQL*옵션이 포함되지 않은 명령줄에서 *MOVE SQL* 를 지정하면 오류가 발생합니다.<br /><br /> 참고: [!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)]|  
|/SQ[L] *package_path*|[!INCLUDE[ssIS](../includes/ssis-md.md)] 패키지의 위치를 지정합니다. 이 옵션은 패키지가 **msdb** 데이터베이스에 저장되었음을 나타냅니다. *package_path* 인수는 [!INCLUDE[ssIS](../includes/ssis-md.md)] 패키지의 경로와 이름을 지정합니다. 폴더 이름은 백슬래시로 끝납니다.<br /><br /> 다음 옵션과 같은 명령줄에서 *SQL* 옵션을 지정하면 DTEXEC_DTEXECERROR가 반환됩니다.<br /><br /> *DTS*<br /><br /> *FILE*<br /><br /> *SQL* 옵션은 다음 옵션 중 하나와 함께 사용하거나 혼자 사용할 수 있습니다.<br /><br /> *SOURCEUSER*<br /><br /> *SOURCEPASSWORD*<br /><br /> *SOURCESERVER*<br /><br /> <br /><br /> *SOURCEUSERNAME* 이 포함되지 않은 경우 패키지에 액세스하기 위해 Windows 인증이 사용됩니다. *SOURCEPASSWORD* 는 *SOURCEUSER* 가 있는 경우에만 허용됩니다. *SOURCEPASSWORD* 를 포함하지 않으면 빈 암호가 사용됩니다.<br /><br /> **\*\* 중요 \*\*** [!INCLUDE[ssNoteStrongPass](../includes/ssnotestrongpass-md.md)]|  
  
## <a name="dtutil-exit-codes"></a>dtutil 종료 코드  
 **dtutil** 은 구문 오류가 있거나, 잘못된 인수가 사용되었거나, 잘못된 옵션 조합이 지정된 경우 경고를 표시하는 종료 코드를 설정합니다. 그 이외의 경우 이 유틸리티는 "작업이 완료되었습니다"라는 메시지를 표시합니다. 다음 표에는 **dtutil** 유틸리티가 종료 시 설정할 수 있는 값이 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|0|유틸리티가 성공적으로 실행되었습니다.|  
|1|유틸리티가 실패했습니다.|  
|4|유틸리티는 요청된 패키지를 찾을 수 없습니다.|  
|5|유틸리티는 요청된 패키지를 로드할 수 없습니다.|  
|6|명령줄에 구문 오류나 의미 체계 오류가 있으므로 유틸리티는 명령줄을 확인할 수 없습니다.|  
  
## <a name="remarks"></a>설명  
 **dtutil**에서는 명령줄을 사용할 수 없거나 리디렉션할 수 없습니다.  
  
 명령줄에서 옵션 순서는 중요하지 않습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 일반적인 명령줄 사용 시나리오를 보여 줍니다.  
  
### <a name="copy-examples"></a>복사 예  
 Windows 인증을 사용하는 **로컬 인스턴스의** msdb [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스에 저장된 패키지를 SSIS 패키지 저장소에 복사하려면 다음 구문을 사용합니다.  
  
```dos
dtutil /SQL srcPackage /COPY DTS;destFolder\destPackage   
```  
  
 파일 시스템의 임의 위치에서 다른 위치로 패키지를 복사하고 복사본에 다른 이름을 지정하려면 다음 구문을 사용합니다.  
  
```dos
dtutil /FILE c:\myPackages\mypackage.dtsx /COPY FILE;c:\myTestPackages\mynewpackage.dtsx  
```  
  
 로컬 파일 시스템에 있는 패키지를 다른 컴퓨터에서 호스팅되는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 복사하려면 다음 구문을 사용합니다.  
  
```dos
dtutil /FILE c:\sourcepkg.dtsx /DestServer <servername> /COPY SQL;destpkgname  
```  
  
 */DestU[ser]* 및 */DestP[assword]* 옵션을 사용하지 않았기 때문에 Windows 인증이 사용됩니다.  
  
 패키지를 복사한 다음 새 ID를 만들려면 다음 구문을 사용합니다.  
  
```dos
dtutil /I /FILE copiedpkg.dtsx   
```  
  
 특정 폴더의 모든 패키지에 대해 새 ID를 만들려면 다음 구문을 사용합니다.  
  
```dos
for %%f in (C:\test\SSISPackages\*.dtsx) do dtutil.exe /I /FILE %%f  
```  
  
 명령 프롬프트에서 명령을 입력하는 경우에는 단일 백분율 기호(%)를 사용합니다. 배치 파일 내에서 명령을 사용하는 경우에는 이중 백분율 기호(%%)를 사용합니다.  
  
### <a name="delete-examples"></a>삭제 예  
 Windows 인증을 사용하는 **인스턴스에서** msdb [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스에 저장된 패키지를 삭제하려면 다음 구문을 사용합니다.  
  
```dos
dtutil /SQL delPackage /DELETE  
```  
  
 **인증을 사용하는** 인스턴스에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] msdb [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스에 저장된 패키지를 삭제하려면 다음 구문을 사용합니다.  
  
```dos
dtutil /SQL delPackage /SOURCEUSER srcUserName /SOURCEPASSWORD #8nGs*w7F /DELETE  
```  
  
> [!NOTE]  
>  명명된 서버에서 패키지를 삭제하려면 **SOURCESERVER** 옵션 및 해당 인수를 포함합니다. *SQL* 옵션을 사용해야만 서버를 지정할 수 있습니다.  
  
 SSIS 패키지 저장소에 저장된 패키지를 삭제하려면 다음 구문을 사용합니다.  
  
```dos
dtutil /DTS delPackage.dtsx /DELETE  
```  
  
 파일 시스템에 저장된 패키지를 삭제하려면 다음 구문을 사용합니다.  
  
```dos
dtutil /FILE c:\delPackage.dtsx /DELETE  
```  
  
### <a name="exists-examples"></a>존재 확인 예  
 Windows 인증을 사용하는 **의 로컬 인스턴스에서** msdb [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스에 패키지가 있는지 여부를 확인하려면 다음 구문을 사용합니다.  
  
```dos
dtutil /SQL srcPackage /EXISTS  
```  
  
 **인증을 사용하는** 의 로컬 인스턴스에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] msdb [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스에 패키지가 있는지 여부를 확인하려면 다음 구문을 사용합니다.  
  
```dos
dtutil /SQL srcPackage /SOURCEUSER srcUserName /SOURCEPASSWORD *hY$d56b /EXISTS  
```  
  
> [!NOTE]  
>  명명된 서버에 패키지가 있는지 확인하려면 **SOURCESERVER** 옵션 및 해당 인수를 포함합니다. SQL 옵션을 사용해야만 서버를 지정할 수 있습니다.  
  
 로컬 패키지 저장소에 패키지가 있는지 확인하려면 다음 구문을 사용합니다.  
  
```dos
dtutil /DTS srcPackage.dtsx /EXISTS  
```  
  
 로컬 파일 시스템에 패키지가 있는지 확인하려면 다음 구문을 사용합니다.  
  
```dos
dtutil /FILE c:\srcPackage.dtsx /EXISTS  
```  
  
### <a name="move-examples"></a>이동 예  
 SSIS 패키지 저장소에 저장된 패키지를 Windows 인증을 사용하는 로컬 **인스턴스의** msdb [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스로 이동하려면 다음 구문을 사용합니다.  
  
```dos
dtutil /DTS srcPackage.dtsx /MOVE SQL;destPackage  
```  
  
 **인증을 사용하는 로컬** 인스턴스의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] msdb [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스에 저장된 패키지를 **인증을 사용하는 다른 로컬** 인스턴스의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] msdb [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스로 이동하려면 다음 구문을 사용합니다.  
  
```dos
dtutil /SQL srcPackage /SOURCEUSER srcUserName /SOURCEPASSWORD $Hj45jhd@X /MOVE SQL;destPackage /DESTUSER destUserName /DESTPASSWORD !38dsFH@v  
```  
  
> [!NOTE]  
>  명명된 서버 간에 패키지를 이동하려면 **SOURCES** 및 **DESTS** 옵션과 해당 인수를 포함합니다. *SQL* 옵션을 사용해야만 서버를 지정할 수 있습니다.  
  
 SSIS 패키지 저장소에 저장된 패키지를 이동하려면 다음 구문을 사용합니다.  
  
```dos
dtutil /DTS srcPackage.dtsx /MOVE DTS;destPackage.dtsx  
```  
  
 파일 시스템에 저장된 패키지를 이동하려면 다음 구문을 사용합니다.  
  
```dos
dtutil /FILE c:\srcPackage.dtsx /MOVE FILE;c:\destPackage.dtsx  
```  
  
### <a name="sign-examples"></a>서명 예  
 Windows 인증을 사용하는 로컬 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스에 저장된 패키지에 서명하려면 다음 구문을 사용합니다.  
  
```dos
dtutil /FILE srcPackage.dtsx /SIGN FILE;destpkg.dtsx;1767832648918a9d989fdac9819873a91f919  
```  
  
 인증서에 대한 정보를 찾으려면 **CertMgr**을 사용합니다. 해시 코드는 **CertMgr** 유틸리티에서 인증서를 선택한 다음 속성을 표시하는 **보기** 를 클릭하여 볼 수 있습니다. **자세히** 탭에는 인증서에 대한 자세한 정보가 제공됩니다. **Thumbprint** 속성은 공백이 제거된 다음 해시 값으로 사용됩니다.  
  
> [!NOTE]  
>  이 예에 사용된 해시는 실제 해시가 아닙니다.  
  
 자세한 내용은 [Authenticode로 코드 서명 및 확인(Signing and Checking Code with Authenticode)](/previous-versions/windows/internet-explorer/ie-developer/platform-apis/ms537364(v=vs.85))의 CertMgr 섹션을 참조하십시오.  
  
### <a name="encrypt-examples"></a>암호화 예  
 다음 예에서는 암호와 함께 전체 패키지 암호화를 사용하여 파일 기반 PackageToEncrypt.dtsx를 파일 기반 EncryptedPackage.dts로 암호화합니다. 암호화에 사용된 암호는 *EncPswd*입니다.  
  
```dos
dtutil /FILE PackageToEncrypt.dtsx /ENCRYPT file;EncryptedPackage.dtsx;3;EncPswd  
```  
  
## <a name="see-also"></a>참고 항목  
[Integration Services(SSIS) 패키지 실행](../integration-services/packages/run-integration-services-ssis-packages.md)  
  
