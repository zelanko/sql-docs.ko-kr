---
title: 사용자 지정 개체 빌드, 배포 및 디버깅 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- custom objects [Integration Services]
ms.assetid: b03685bc-5398-4c3f-901a-1219c1098fbe
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a6f96e795b44e936c4088e4ded571e76c33d4863
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65724800"
---
# <a name="building-deploying-and-debugging-custom-objects"></a>사용자 지정 개체 빌드, 배포 및 디버깅

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]의 사용자 지정 개체에 대한 코드를 작성한 후에 어셈블리를 빌드하여 배포한 다음, 패키지에서 사용할 수 있도록 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에 통합하여 테스트하고 디버그해야 합니다.  
  
##  <a name="top"></a> Integration Services의 사용자 지정 개체 빌드, 배포 및 디버깅 단계  
 개체의 사용자 지정 기능을 작성한 후에는 이를 테스트하고 사용자가 사용할 수 있도록 해야 합니다. 이 단계는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]용으로 만들 수 있는 모든 유형의 사용자 지정 개체에서 매우 비슷합니다.  
  
 다음은 이를 빌드, 배포 및 테스트하는 단계입니다.  
  
1.  생성할 어셈블리를 강력한 이름으로 [서명](#signing)합니다.  
  
2.  어셈블리를 [빌드](#building)합니다.  
  
3.  어셈블리를 적절한 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 폴더로 이동하거나 복사하여 [배포](#deploying)합니다.  
  
4.  GAC(전역 어셈블리 캐시)에 어셈블리를 [설치](#installing)합니다.  
  
     이 개체는 도구 상자에 자동으로 추가됩니다.  
  
5.  필요한 경우 [배포 문제를 해결](#troubleshooting)합니다.  
  
6.  코드를 [테스트](#testing)하고 디버그합니다.  
  
 이제 SSDT(SQL Server Data Tools)에서 SSIS 디자이너를 사용하여 다른 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 대상으로 하는 패키지를 만들고, 유지 관리하고, 실행할 수 있습니다. 이러한 개선이 사용자 지정 확장에 미치는 영향에 대한 자세한 내용은 [SQL Server 2016용 SSDT 2015의 다중 버전 지원을 통해 SSIS 사용자 지정 확장 지원](https://blogs.msdn.microsoft.com/ssis/2016/04/19/getting-your-ssis-custom-extensions-to-be-supported-by-the-multi-version-support-of-ssdt-2015-for-sql-server-2016/)을 참조하세요.  
  
##  <a name="signing"></a> 어셈블리 서명  
 공유하려는 어셈블리는 전역 어셈블리 캐시에 설치해야 합니다. 전역 어셈블리 캐시에 추가된 어셈블리는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]와 같은 응용 프로그램에서 사용할 수 있습니다. 전역 어셈블리 캐시에 어셈블리를 추가하려면 어셈블리를 강력한 이름으로 서명하여 해당 어셈블리가 전역적으로 고유함을 보장해야 합니다. 강력한 이름의 어셈블리에는 어셈블리의 이름, culture, 공개 키 및 버전 번호를 포함하는 정규화된 이름이 있습니다. 런타임에서는 이 정보를 사용하여 어셈블리를 찾고 같은 이름의 다른 어셈블리와 구별합니다.  
  
 강력한 이름으로 어셈블리를 서명하려면 먼저 퍼블릭/프라이빗 키 쌍이 있어야 하며 이 키 쌍이 없으면 만들어야 합니다. 이 퍼블릭 및 프라이빗 암호화 키 쌍은 빌드할 때 강력한 이름의 어셈블리를 만드는 데 사용합니다.  
  
 강력한 이름과 어셈블리를 서명할 때 따라야 하는 단계에 대한 자세한 내용은 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 설명서의 다음 항목을 참조하십시오.  
  
-   강력한 이름의 어셈블리  
  
-   공개/개인 키 쌍 만들기  
  
-   방법: 강력한 이름으로 어셈블리 서명  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]에서는 빌드할 때 어셈블리를 강력한 이름으로 서명하기가 쉽습니다. **프로젝트 속성** 대화 상자에서 **서명** 탭을 선택하고, **어셈블리 서명** 옵션을 선택한 다음, 키 파일(.snk)의 경로를 제공합니다.  
  
##  <a name="building"></a> 어셈블리 빌드  
 프로젝트를 서명한 후에는 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]의 **빌드** 메뉴에서 사용할 수 있는 명령을 사용하여 프로젝트 또는 솔루션을 빌드하거나 다시 빌드해야 합니다. 솔루션에 사용자 지정 사용자 인터페이스를 위한 별도의 프로젝트가 포함된 경우 이 프로젝트도 강력한 이름으로 서명해야 하며 이 프로젝트를 솔루션과 동시에 빌드할 수 있습니다.  
  
 어셈블리를 배포하고 글로벌 어셈블리 캐시에 설치하는 다음 두 단계를 수행하는 데 가장 편리한 방법은 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]에서 이러한 단계를 빌드 후 이벤트로 스크립팅하는 것입니다. 빌드 이벤트는 [프로젝트 속성]의 **컴파일** 페이지([!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 프로젝트의 경우) 또는 **빌드 이벤트** 페이지(C# 프로젝트의 경우)에서 사용할 수 있습니다. **gacutil.exe**와 같은 명령 프롬프트 유틸리티에는 전체 경로가 필요합니다. 공백이 포함된 경로와 공백이 포함된 경로로 확장되는 $(TargetPath) 등의 매크로는 모두 따옴표로 묶어야 합니다.  
  
 다음은 사용자 지정 로그 공급자에 대한 빌드 후 이벤트 명령줄의 예입니다.  
  
```cmd
"C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0A\bin\NETFX 4.0 Tools\gacutil.exe" -u $(TargetName)  
"C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0A\bin\NETFX 4.0 Tools\gacutil.exe" -i $(TargetFileName)  
copy $(TargetFileName) "C:\Program Files\Microsoft SQL Server\130\DTS\LogProviders "  
```  
  
##  <a name="deploying"></a> 어셈블리 배포  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]가 설치될 때 만들어진 일련의 폴더에 있는 파일을 열거하여 패키지에서 사용할 수 있는 사용자 지정 개체를 찾습니다. 기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 설정을 사용한 경우 이러한 폴더 집합은 **C:\Program Files\Microsoft SQL Server\130\DTS** 아래에 있습니다. 그러나 사용자 지정 개체에 대한 설치 프로그램을 만드는 경우 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\SSIS\Setup\DtsPath** 레지스트리 키의 값을 검사하여 이 폴더의 위치를 확인해야 합니다.  
  
> [!NOTE]  
>  SQL Server Data Tools의 다중 버전 지원과 함께 제대로 작동하도록 사용자 지정 구성 요소를 배포하는 방법에 대한 자세한 내용은 [SQL Server 2016용 SSDT 2015의 다중 버전 지원을 통해 SSIS 사용자 지정 확장 지원](https://blogs.msdn.microsoft.com/ssis/2016/04/19/getting-your-ssis-custom-extensions-to-be-supported-by-the-multi-version-support-of-ssdt-2015-for-sql-server-2016/)을 참조하세요.  
  
 다음과 같은 두 가지 방법으로 폴더에 어셈블리를 추가할 수 있습니다.  
  
-   빌드 후 컴파일된 어셈블리를 적절한 폴더로 이동하거나 복사합니다. 편의상 빌드 후 이벤트에 복사 명령을 포함할 수 있습니다.  
  
-   어셈블리를 적절한 폴더에 직접 빌드합니다.  
  
 **C:\Program Files\Microsoft SQL Server\130\DTS**에 있는 다음 배포 폴더는 다양한 유형의 사용자 지정 개체에 사용됩니다.  
  
|사용자 지정 개체|배포 폴더|  
|-------------------|-----------------------|  
|태스크|태스크|  
|ODBC 대상 편집기|Connections|  
|로그 공급자|LogProviders|  
|데이터 흐름 구성 요소|PipelineComponents|  
  
> [!NOTE]  
>  이러한 폴더에 복사된 어셈블리는 사용 가능한 태스크, 연결 관리자 등의 열거형을 지원합니다. 따라서 사용자 지정 개체의 사용자 지정 사용자 인터페이스만 포함된 어셈블리는 이러한 폴더에 배포하지 않아도 됩니다.  
  
##  <a name="installing"></a> 전역 어셈블리 캐시에 어셈블리 설치  
 GAC(전역 어셈블리 캐시)에 태스크 어셈블리를 설치하려면 **gacutil.exe** 명령줄 도구를 사용하거나 어셈블리를 `%system%\assembly` 디렉터리에 끌어 놓습니다. 편의상 **gacutil.exe**에 대한 호출을 빌드 후 이벤트에 포함할 수도 있습니다.  
  
 다음 명령은 **gacutil.exe**를 사용하여 *MyTask.dll*이라는 구성 요소를 GAC에 설치합니다.  
  
 `gacutil /iF MyTask.dll`  
  
 새 버전의 사용자 지정 개체를 설치한 후에는 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 닫았다가 다시 열어야 합니다. 전역 어셈블리 캐시에 이전 버전의 사용자 지정 개체를 설치한 경우 새 버전을 설치하려면 먼저 이전 버전을 제거해야 합니다. 어셈블리를 제거하려면 **gacutil.exe**를 실행하고 `/u` 옵션을 사용하여 어셈블리 이름을 지정합니다.  
  
 전역 어셈블리 캐시에 대한 자세한 내용은 "[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 도구"의 "전역 어셈블리 캐시 도구(Gactutil.exe)"를 참조하십시오.  
  
##  <a name="troubleshooting"></a> 배포 문제 해결  
 사용자 지정 개체가 **도구 상자** 또는 사용 가능한 개체 목록에 표시되지만 패키지에 추가할 수 없는 경우 다음을 시도해 보세요.  
  
1.  전역 어셈블리 캐시에 여러 버전의 구성 요소가 있는지 확인합니다. 전역 어셈블리 캐시에 여러 버전의 구성 요소가 있는 경우 디자이너에서 구성 요소를 로드하지 못할 수 있습니다. 전역 어셈블리 캐시에서 어셈블리의 모든 인스턴스를 삭제하고 어셈블리를 다시 추가합니다.  
  
2.  배포 폴더에 어셈블리의 단일 인스턴스만 있는지 확인합니다.  
  
3.  도구 상자를 새로 고칩니다.  
  
4.  [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]를 **devenv.exe**에 연결하고 초기화 코드를 단계별로 실행하도록 중단점을 설정하여 예외가 발생하지 않도록 합니다.  
  
##  <a name="testing"></a> 코드 테스트 및 디버깅  
 사용자 지정 개체의 런타임 메서드를 가장 간단하게 디버그하려면 사용자 지정 개체를 빌드하고 해당 구성 요소를 사용하는 패키지를 실행한 후에 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]에서 **dtexec.exe**를 시작합니다.  
  
 **Validate** 메서드와 같은 구성 요소의 디자인 타임 메서드를 디버그하려면 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]의 두 번째 인스턴스에서 해당 구성 요소를 사용하는 패키지를 열고 **devenv.exe** 프로세스에 연결합니다.  
  
 또한 패키지가 열려 있고 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 실행 중일 때 구성 요소의 런타임 메서드를 디버그하려면 **DtsDebugHost.exe** 프로세스에도 연결할 수 있도록 패키지 실행을 강제로 일시 중지해야 합니다.  
  
#### <a name="to-debug-an-objects-run-time-methods-by-attaching-to-dtexecexe"></a>dtexec.exe에 연결하여 개체의 런타임 메서드를 디버깅하려면  
  
1.  이 항목에 설명된 대로 디버그 구성 요소에서 프로젝트를 서명 및 빌드하고 배포한 다음 전역 어셈블리 캐시에 설치합니다.  
  
2.  **프로젝트 속성**의 **디버그** 탭에서 **시작 외부 프로그램**을 **시작 동작**으로 선택하고, C:\Program Files\Microsoft SQL Server\130\DTS\Binn에 기본적으로 설치되는 **dtexec.exe**를 찾습니다.  
  
3.  **명령줄 옵션** 입력란의 **시작 옵션** 아래에서 구성 요소를 사용하는 패키지를 실행하는 데 필요한 명령줄 인수를 입력합니다. 명령줄 인수는 /F[ILE] 스위치와 그 다음에 나오는 .dtsx 파일의 경로 및 파일 이름으로 구성되는 경우가 많습니다. 자세한 내용은 [dtexec Utility](../../integration-services/packages/dtexec-utility.md)를 참조하세요.  
  
4.  원본 코드에서 구성 요소의 런타임 메서드 중 적절한 위치에 중단점을 설정합니다.  
  
5.  프로젝트를 실행합니다.  
  
#### <a name="to-debug-a-custom-objects-design-time-methods-by-attaching-to-sql-server-data-tools"></a>SQL Server Data Tools에 연결하여 사용자 지정 개체의 디자인 타임 메서드를 디버깅하려면  
  
1.  이 항목에 설명된 대로 디버그 구성 요소에서 프로젝트를 서명 및 빌드하고 배포한 다음 전역 어셈블리 캐시에 설치합니다.  
  
2.  원본 코드에서 사용자 지정 개체의 디자인 타임 메서드 중 적절한 위치에 중단점을 설정합니다.  
  
3.  [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]의 두 번째 인스턴스를 열고 해당 사용자 지정 개체를 사용하는 패키지가 포함된 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 로드합니다.  
  
4.  [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]의 첫 번째 인스턴스에서 **디버그** 메뉴의 **프로세스에 연결**을 선택하여 패키지가 로드되는 **devenv.exe**의 두 번째 인스턴스에 연결합니다.  
  
5.  [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]의 두 번째 인스턴스에서 패키지를 실행합니다.  
  
#### <a name="to-debug-a-custom-objects-run-time-methods-by-attaching-to-sql-server-data-tools"></a>SQL Server Data Tools에 연결하여 사용자 지정 개체의 런타임 메서드를 디버깅하려면  
  
1.  이전 절차에 나열된 단계를 완료한 후 **DtsDebugHost.exe**에 연결할 수 있도록 패키지 실행을 강제로 일시 중지합니다. **OnPreExecute** 이벤트에 중단점을 추가하거나, 프로젝트에 스크립트 태스크를 추가하고 모달 메시지 상자를 표시하는 스크립트를 입력하여 강제로 일시 중지할 수 있습니다.  
  
2.  패키지를 실행합니다. 일시 중지가 발생하면 코드 프로젝트가 열려 있는 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 인스턴스로 전환하고 **디버그** 메뉴에서 **프로세스에 연결**을 선택합니다. **형식** 열에 **x86** 전용으로 나열된 인스턴스가 아니라 **Managed, x86**으로 나열된 **DtsDebugHost.exe** 인스턴스에 연결해야 합니다.  
  
3.  일시 중지된 패키지로 돌아가서 중단점을 지나 계속하거나 **확인**을 클릭하여 스크립트 태스크에서 발생한 메시지 상자를 닫고 패키지 실행 및 디버깅을 계속합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 사용자 지정 개체 개발](../../integration-services/extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)   
 [사용자 지정 개체 지속](../../integration-services/extending-packages-custom-objects/persisting-custom-objects.md)   
 [패키지 배포 문제 해결 도구](../../integration-services/troubleshooting/troubleshooting-tools-for-package-development.md)  
  
  
