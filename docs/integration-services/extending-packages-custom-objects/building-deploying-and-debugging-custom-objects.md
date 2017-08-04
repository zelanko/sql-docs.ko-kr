---
title: "빌드, 배포 및 사용자 지정 개체를 디버깅 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom objects [Integration Services]
ms.assetid: b03685bc-5398-4c3f-901a-1219c1098fbe
caps.latest.revision: 50
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 99fdd71403b12cee8ba9f207890268cde2e1d450
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="building-deploying-and-debugging-custom-objects"></a>사용자 지정 개체 빌드, 배포 및 디버깅
  에 대 한 사용자 지정 개체에 대 한 코드를 작성 한 후 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], 어셈블리를 빌드, 배포 및에 통합 해야 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 패키지에서 사용 하기 위해 사용할 수 있도록 하 고 테스트 및 디버그 하기.  
  
##  <a name="top"></a>빌드, 배포 및 Integration Services에 대 한 사용자 지정 개체를 디버깅의 단계  
 개체의 사용자 지정 기능을 작성한 후에는 이를 테스트하고 사용자가 사용할 수 있도록 해야 합니다. 이 단계는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]용으로 만들 수 있는 모든 유형의 사용자 지정 개체에서 매우 비슷합니다.  
  
 다음은 빌드, 배포 및 테스트 하는 단계입니다.  
  
1.  [Sign](#signing) 어셈블리를 강력한 이름으로 생성 합니다.  
  
2.  [빌드](#building) 어셈블리입니다.  
  
3.  [배포](#deploying) 이동 하거나 적절 한 복사 하 여 어셈블리 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 폴더입니다.  
  
4.  [설치](#installing) 전역 어셈블리 캐시 (GAC)에 어셈블리입니다.  
  
     이 개체는 도구 상자에 자동으로 추가됩니다.  
  
5.  [문제를 해결](#troubleshooting) 배포에 필요한 경우.  
  
6.  [테스트](#testing) 고 코드를 디버그 합니다.  
  
 이제 사용할 수 있습니다 SSIS 디자이너 SQL Server Data Tools (SSDT)의 서로 다른 버전을 대상으로 하는 패키지를 만들기, 유지 관리 및 실행 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 사용자 지정 확장 프로그램을 개선 한이 엔진이이의 영향에 대 한 자세한 내용은 참조 하세요. [SQL Server 2016 용 SSDT 2015 년의 다중 버전 지원에서 지원 하도록 사용자 지정 SSIS 확장 가져오기](https://blogs.msdn.microsoft.com/ssis/2016/04/19/getting-your-ssis-custom-extensions-to-be-supported-by-the-multi-version-support-of-ssdt-2015-for-sql-server-2016/)  
  
##  <a name="signing"></a>어셈블리에 서명  
 공유하려는 어셈블리는 전역 어셈블리 캐시에 설치해야 합니다. 전역 어셈블리 캐시에 추가된 어셈블리는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]와 같은 응용 프로그램에서 사용할 수 있습니다. 전역 어셈블리 캐시에 어셈블리를 추가하려면 어셈블리를 강력한 이름으로 서명하여 해당 어셈블리가 전역적으로 고유함을 보장해야 합니다. 강력한 이름의 어셈블리에는 어셈블리의 이름, culture, 공개 키 및 버전 번호를 포함하는 정규화된 이름이 있습니다. 런타임에서는 이 정보를 사용하여 어셈블리를 찾고 같은 이름의 다른 어셈블리와 구별합니다.  
  
 강력한 이름으로 어셈블리를 서명하려면 먼저 공개/개인 키 쌍이 있어야 하며 이 키 쌍이 없으면 만들어야 합니다. 이 암호화 키 쌍은 빌드할 때 강력한 이름의 어셈블리를 만드는 데 사용합니다.  
  
 강력한 이름과 어셈블리를 서명할 때 따라야 하는 단계에 대한 자세한 내용은 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 설명서의 다음 항목을 참조하십시오.  
  
-   강력한 이름의 어셈블리  
  
-   공개/개인 키 쌍 만들기  
  
-   방법: 강력한 이름으로 어셈블리 서명  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]에서는 빌드할 때 어셈블리를 강력한 이름으로 서명하기가 쉽습니다. 에 **프로젝트 속성** 대화 상자는 **서명** 탭 합니다. 옵션을 선택 **어셈블리에 서명** 키 (.snk) 파일의 경로 제공 합니다.  
  
##  <a name="building"></a>어셈블리 빌드  
 프로젝트를 서명한 후 빌드 또는 프로젝트 또는 솔루션에서 사용할 수 있는 명령을 사용 하 여 다시 작성 해야 합니다는 **빌드** 의 메뉴 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]합니다. 솔루션에 사용자 지정 사용자 인터페이스를 위한 별도의 프로젝트가 포함된 경우 이 프로젝트도 강력한 이름으로 서명해야 하며 이 프로젝트를 솔루션과 동시에 빌드할 수 있습니다.  
  
 어셈블리를 배포하고 전역 어셈블리 캐시에 설치하는 다음 두 단계를 수행하는 데 가장 편리한 방법은 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]에서 이러한 단계를 빌드 후 이벤트로 스크립팅하는 것입니다. 사용할 수 있는 빌드 이벤트는 **컴파일** 에 대 한 프로젝트 속성 페이지는 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 프로젝트에서는 **빌드 이벤트** C# 프로젝트에 대 한 페이지입니다. 전체 경로와 같은 명령 프롬프트 유틸리티에 대 한 필요는 **gacutil.exe**합니다. 공백이 포함된 경로와 공백이 포함된 경로로 확장되는 $(TargetPath) 등의 매크로는 모두 따옴표로 묶어야 합니다.  
  
 다음은 사용자 지정 로그 공급자에 대한 빌드 후 이벤트 명령줄의 예입니다.  
  
```  
"C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0A\bin\NETFX 4.0 Tools\gacutil.exe" -u $(TargetName)  
"C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0A\bin\NETFX 4.0 Tools\gacutil.exe" -i $(TargetFileName)  
copy $(TargetFileName) "C:\Program Files\Microsoft SQL Server\130\DTS\LogProviders "  
```  
  
##  <a name="deploying"></a>어셈블리 배포  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에 일련의 될 때 생성 되는 폴더에 있는 파일을 열거 하 여 패키지에서 사용 하기 위해 사용할 수 있는 사용자 지정 개체를 찾는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 가 설치 되어 있습니다. 때 기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 설정에 사용 되는 경우이 집합 폴더 아래에 있는 **C:\Program Files\Microsoft SQL Server\130\DTS**합니다. 그러나 사용자 지정 개체에 대 한 설치 프로그램을 만드는 경우 값을 확인 해야는 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\SSIS\Setup\DtsPath** 레지스트리 키를이 폴더의 위치를 확인 합니다.  
  
> [!NOTE]  
>  SQL Server Data Tools에서 다중 버전 지원 제대로 작동 하는 사용자 지정 구성 요소를 배포 하는 방법에 대 한 정보를 참조 하십시오. [SQL Server 2016 용 SSDT 2015 년의 다중 버전 지원에 지원을 받기 위해 SSIS 사용자 지정 확장 프로그램을 가져오는](https://blogs.msdn.microsoft.com/ssis/2016/04/19/getting-your-ssis-custom-extensions-to-be-supported-by-the-multi-version-support-of-ssdt-2015-for-sql-server-2016/)합니다.  
  
 다음과 같은 두 가지 방법으로 폴더에 어셈블리를 추가할 수 있습니다.  
  
-   빌드 후 컴파일된 어셈블리를 적절한 폴더로 이동하거나 복사합니다. 편의상 빌드 후 이벤트에 복사 명령을 포함할 수 있습니다.  
  
-   어셈블리를 적절한 폴더에 직접 빌드합니다.  
  
 다음 배포 폴더는 **C:\Program Files\Microsoft SQL Server\130\DTS** 다양 한 유형의 사용자 지정 개체에 사용 됩니다.  
  
|사용자 지정 개체|배포 폴더|  
|-------------------|-----------------------|  
|태스크|태스크|  
|ODBC 대상 편집기|연결|  
|로그 공급자|LogProviders|  
|데이터 흐름 구성 요소|PipelineComponents|  
  
> [!NOTE]  
>  이러한 폴더에 복사된 어셈블리는 사용 가능한 태스크, 연결 관리자 등의 열거형을 지원합니다. 따라서 사용자 지정 개체의 사용자 지정 사용자 인터페이스만 포함된 어셈블리는 이러한 폴더에 배포하지 않아도 됩니다.  
  
##  <a name="installing"></a>전역 어셈블리 캐시에 어셈블리 설치  
 작업 어셈블리를 전역 어셈블리 캐시 (GAC)에 설치 하려면 명령줄 도구를 사용 하 여 **gacutil.exe**, 하거나 어셈블리를 끌어는 `%system%\assembly` 디렉터리입니다. 편의 위해 포함할 수 있습니다에 대 한 호출 **gacutil.exe** 빌드 후 이벤트에서입니다.  
  
 다음 명령은 라는 구성 요소가 설치 *MyTask.dll* 를 사용 하 여 GAC에 **gacutil.exe**합니다.  
  
 `gacutil /iF MyTask.dll`  
  
 새 버전의 사용자 지정 개체를 설치한 후에는 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 닫았다가 다시 열어야 합니다. 전역 어셈블리 캐시에 이전 버전의 사용자 지정 개체를 설치한 경우 새 버전을 설치하려면 먼저 이전 버전을 제거해야 합니다. 어셈블리를 제거 하려면 실행 **gacutil.exe** 와 어셈블리 이름을 지정 하 고는 `/u` 옵션입니다.  
  
 전역 어셈블리 캐시에 대한 자세한 내용은 "[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 도구"의 "전역 어셈블리 캐시 도구(Gactutil.exe)"를 참조하십시오.  
  
##  <a name="troubleshooting"></a>배포 문제 해결  
 사용자 지정 개체에 표시 되 면는 **도구 상자** 또는 패키지에 추가 하 고 다음 있지만 사용 가능한 개체 목록이 없는 경우:  
  
1.  전역 어셈블리 캐시에 여러 버전의 구성 요소가 있는지 확인합니다. 전역 어셈블리 캐시에 여러 버전의 구성 요소가 있는 경우 디자이너에서 구성 요소를 로드하지 못할 수 있습니다. 전역 어셈블리 캐시에서 어셈블리의 모든 인스턴스를 삭제하고 어셈블리를 다시 추가합니다.  
  
2.  배포 폴더에 어셈블리의 단일 인스턴스만 있는지 확인합니다.  
  
3.  도구 상자를 새로 고칩니다.  
  
4.  연결 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 를 **devenv.exe** 예외가 발생 하지 않는지 되도록 초기화 코드를 단계별로 실행 되도록 중단점을 설정 합니다.  
  
##  <a name="testing"></a>테스트 및 코드 디버깅  
 시작 하는 사용자 지정 개체의 런타임 메서드를 디버깅 하는 가장 간단한 방법입니다 **dtexec.exe** 에서 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 후 사용자 지정 개체를 작성 및 구성 요소를 사용 하는 패키지를 실행 합니다.  
  
 와 같은 구성 요소의 디자인 타임 메서드를 디버깅 하려는 경우는 **유효성 검사** 메서드를 두 번째 인스턴스의 구성 요소를 사용 하는 패키지를 열고 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]에 연결 하 고 해당 **devenv.exe** 프로세스입니다.  
  
 패키지를 열고에서 실행 되는 구성 요소의 런타임 메서드를 디버깅 하려는 경우 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너, 강제 해야 패키지의 실행을 일시 중지 한도 연결할 수 있도록는 **DtsDebugHost.exe** 프로세스입니다.  
  
#### <a name="to-debug-an-objects-run-time-methods-by-attaching-to-dtexecexe"></a>dtexec.exe에 연결하여 개체의 런타임 메서드를 디버깅하려면  
  
1.  이 항목에 설명된 대로 디버그 구성 요소에서 프로젝트를 서명 및 빌드하고 배포한 다음 전역 어셈블리 캐시에 설치합니다.  
  
2.  에 **디버그** 탭 **프로젝트 속성**선택, **시작 외부 프로그램** 으로 **시작 작업**, 찾습니다 **dtexec.exe**, C:\Program Files\Microsoft SQL Server\130\DTS\Binn에서 기본적으로 설치 된 합니다.  
  
3.  에 **명령줄 옵션** 텍스트 상자의 **시작 옵션**, 구성 요소를 사용 하는 패키지를 실행 하는 데 필요한 명령줄 인수를 입력 합니다. 명령줄 인수는 /F[ILE] 스위치와 그 다음에 나오는 .dtsx 파일의 경로 및 파일 이름으로 구성되는 경우가 많습니다. 자세한 내용은 [dtexec Utility](../../integration-services/packages/dtexec-utility.md)을 참조하세요.  
  
4.  원본 코드에서 구성 요소의 런타임 메서드 중 적절한 위치에 중단점을 설정합니다.  
  
5.  프로젝트를 실행합니다.  
  
#### <a name="to-debug-a-custom-objects-design-time-methods-by-attaching-to-sql-server-data-tools"></a>SQL Server Data Tools에 연결하여 사용자 지정 개체의 디자인 타임 메서드를 디버깅하려면  
  
1.  이 항목에 설명된 대로 디버그 구성 요소에서 프로젝트를 서명 및 빌드하고 배포한 다음 전역 어셈블리 캐시에 설치합니다.  
  
2.  원본 코드에서 사용자 지정 개체의 디자인 타임 메서드 중 적절한 위치에 중단점을 설정합니다.  
  
3.  [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]의 두 번째 인스턴스를 열고 해당 사용자 지정 개체를 사용하는 패키지가 포함된 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 로드합니다.  
  
4.  첫 번째 인스턴스에서 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]의 두 번째 인스턴스에 연결 하 **devenv.exe** 에서 선택 하 여 패키지가 로드 되는 **프로세스에 연결** 에서 **디버그** 첫 번째 인스턴스 메뉴.  
  
5.  [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]의 두 번째 인스턴스에서 패키지를 실행합니다.  
  
#### <a name="to-debug-a-custom-objects-run-time-methods-by-attaching-to-sql-server-data-tools"></a>SQL Server Data Tools에 연결하여 사용자 지정 개체의 런타임 메서드를 디버깅하려면  
  
1.  이전 절차에 나열 된 단계를 완료 한 후 패키지의 실행을 일시 중지를 연결할 수 있도록 강제로 **DtsDebugHost.exe**합니다. 중단점을 추가 하 여 강제로 일시이 중지할 수 있습니다는 **OnPreExecute** 이벤트를 하거나 프로젝트에 스크립트 태스크를 추가 하 고 모달 메시지 상자를 표시 하는 스크립트를 입력 합니다.  
  
2.  패키지를 실행합니다. 인스턴스를 일시 중지 되어 있는 경우 전환 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 코드 프로젝트 열기 및 선택 이라는 **프로세스에 연결** 에서 **디버그** 메뉴. 인스턴스에 연결 해야 **DtsDebugHost.exe** 로 나열 **Managed, x86** 에 **형식** 열으로 나열 되지 인스턴스에 **x86** 만 합니다.  
  
3.  일시 중지 된 패키지로 돌아가서 중단점을 지 나 계속 진행 하거나 클릭 **확인** 하 패키지 실행 및 디버깅을 계속 하 고 스크립트 태스크에 의해 발생 하 여 메시지 상자를 닫습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services에 대 한 사용자 지정 개체 개발](../../integration-services/extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)   
 [사용자 지정 개체 지속](../../integration-services/extending-packages-custom-objects/persisting-custom-objects.md)   
 [패키지 배포 문제 해결 도구](../../integration-services/troubleshooting/troubleshooting-tools-for-package-development.md)  
  
  
