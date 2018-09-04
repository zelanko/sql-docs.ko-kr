---
title: RS.exe 유틸리티(SSRS) | Microsoft Docs
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: tools
ms.suite: pro-bi
ms.topic: conceptual
helpviewer_keywords:
- automatic report server tasks
- rs utility
- command prompt utilities [Reporting Services]
- report servers [Reporting Services], automating tasks
- command prompt utilities [SQL Server], rs
- scripts [Reporting Services], command prompt
- deploying reports [Reporting Services]
ms.assetid: bd6f958f-cce6-4e79-8a0f-9475da2919ce
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b9990f797ab83f3ced5009b179944227107350ce
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43282081"
---
# <a name="rsexe-utility-ssrs"></a>RS.exe 유틸리티(SSRS)
  RS.exe 유틸리티에서는 입력 파일에 제공된 스크립트를 처리합니다. 이 유틸리티를 사용하여 보고서 서버 배포 및 관리 태스크를 자동화할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]부터는 **rs** 유틸리티가 SharePoint 통합 모드용으로 구성된 보고서 서버와 기본 모드에서 구성된 서버에 대해 모두 지원됩니다. 이전 버전에서는 기본 모드 구성만 지원되었습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
rs {-?}  
{-i input_file=}  
{-s serverURL}  
{-u username}  
{-p password}  
{-e endpoint}  
{-l time_out}  
{-b batchmode}  
{-v globalvars=}  
{-t trace}  
```  
  
##  <a name="bkmk_filelocation"></a> 파일 위치  
 **RS.exe** 는 **\Program Files\Microsoft SQL Server\110\Tools\Binn**에 있습니다. 파일 시스템의 모든 폴더에서 유틸리티를 실행할 수 있습니다.  
  
##  <a name="bkmk_arguments"></a> 인수  
 **-?**  
 (옵션) **rs** 인수의 구문을 표시합니다.  
  
 **-i** *input_file*  
 실행할 .rss 파일을 지정합니다(필수). 이 값은 .rss 파일의 상대 경로 또는 정규화된 경로여야 합니다.  
  
 **-s** *serverURL*  
 파일을 실행할 웹 서버 이름 및 보고서 서버 가상 디렉터리를 지정합니다(필수). 보고서 서버 URL의 예는 `http://examplewebserver/reportserver`입니다. 서버 이름의 시작 부분에 붙는 접두사 http:// 또는 https://는 옵션입니다. 이를 생략하면 보고서 서버 스크립트 호스트에서 https를 먼저 사용해 본 다음 작동하지 않는 경우 http를 사용합니다.  
  
 **-u** [*domain*\\]*username*  
 보고서 서버에 연결하는 데 사용되는 사용자 계정을 지정합니다(옵션). **-u** 와 **-p** 를 생략하면 현재 Windows 사용자 계정이 사용됩니다.  
  
 **-p** *password*  
 **-u** 인수에 사용할 암호를 지정합니다( **-u** 를 지정한 경우 필수). 이 값은 대/소문자를 구분합니다.  
  
 **-e**  
 스크립트가 실행되어야 하는 대상 SOAP 엔드포인트를 지정합니다(옵션). 유효한 값은 다음과 같습니다.  
  
-   Mgmt2010  
  
-   Mgmt2006  
  
-   Mgmt2005  
  
-   Exec2005  
  
 값이 지정되지 않은 경우 Mgmt2005가 엔드포인트로 사용됩니다. SOAP 엔드포인트에 대한 자세한 내용은 [Report Server Web Service Endpoints](../../reporting-services/report-server-web-service/methods/report-server-web-service-endpoints.md)을 참조하세요.  
  
 **-l** *time_out*  
 서버에 대한 연결 제한 시간이 초과하기 전까지의 시간(초)을 지정합니다(옵션). 기본값은 60초입니다. 시간 제한 값을 지정하지 않으면 이 기본값이 사용됩니다. 값을 **0** 으로 지정하면 연결 시간 제한이 없습니다.  
  
 **-b**  
 스크립트 파일의 명령이 일괄적으로 실행되도록 지정합니다(옵션). 실패하는 명령이 있으면 이 일괄 처리가 롤백됩니다. 일부 명령은 일괄 처리 방식이 아닌 일반적인 방식으로 실행됩니다. 스크립트 내에서 발생되며 처리되지 않는 예외만 롤백됩니다. 스크립트가 예외를 처리하고 **Main**에서 정상적으로 반환되는 경우 일괄 처리가 커밋됩니다. 이 매개 변수를 생략하면 명령이 일괄 처리를 만들지 않고 실행됩니다. 자세한 내용은 [Batching Methods](../../reporting-services/report-server-web-service-net-framework-soap-headers/batching-methods.md)을 참조하세요.  
  
 **-v** *globalvar*  
 스크립트에서 사용되는 전역 변수를 지정합니다(옵션). 스크립트에서 전역 변수가 사용되는 경우에는 이 인수를 지정해야 합니다. 지정하는 값은 .rss 파일에 정의되는 전역 변수에 대해 유효해야 합니다. 각 **–v** 인수에 대해 하나의 전역 변수를 지정해야 합니다.  
  
 **-v** 인수는 명령줄에서 지정되며 런타임에 스크립트에 정의된 전역 변수의 값을 설정하는 데 사용됩니다. 예를 들어 스크립트에 *parentFolder*라는 변수가 포함되어 있다면 다음과 같이 명령줄에서 해당 폴더에 대한 이름을 지정할 수 있습니다.  
  
 `rs.exe -i myScriptFile.rss -s http://myServer/reportserver -v parentFolder="Financial Reports"`  
  
 전역 변수가 지정한 이름으로 생성된 다음 제공된 값으로 설정됩니다. 예를 들어 **-v a=**"**1**" **-v b=**"**2**"를 지정하면 **a** 수에는 "**1**" 값이 지정되고 **b** 변수에는 "**2**" 값이 지정됩니다.  
  
 전역 변수는 스크립트의 모든 함수에서 사용할 수 있습니다. 백슬래시와 인용 부호(**\\"**)는 큰따옴표로 해석됩니다. 인용 부호는 문자열에 공백이 포함되어 있는 경우에만 필요합니다. 변수 이름은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]에 유효해야 하며 알파벳 문자 또는 밑줄로 시작하고 알파벳 문자, 숫자 또는 밑줄이 포함되어야 합니다. 예약어는 변수 이름으로 사용할 수 없습니다. 전역 변수 사용에 대한 자세한 내용은 [식의 기본 제공 컬렉션&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md)을 참조하세요.  
  
 **-t**  
 추적 로그에 오류 메시지를 출력합니다(옵션). 이 인수는 값을 가지지 않습니다. 자세한 내용은 [Report Server Service Trace Log](../../reporting-services/report-server/report-server-service-trace-log.md)을 참조하세요.  
  
##  <a name="bkmk_permissions"></a> 사용 권한  
 이 도구를 사용하려면 스크립트를 실행하는 보고서 서버 인스턴스에 연결할 수 있는 사용 권한이 필요합니다. 스크립트를 실행하여 로컬 컴퓨터나 원격 컴퓨터를 변경할 수 있습니다. 원격 컴퓨터에 설치된 보고서 서버를 변경하려면 **-s** 인수에 원격 컴퓨터를 지정합니다.  
  
##  <a name="bkmk_examples"></a> 예  
 다음 예에서는 실행할 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET 스크립트 및 웹 서비스 메서드가 포함된 스크립트 파일을 지정하는 방법을 보여 줍니다.  
  
```  
rs –i c:\scriptfiles\script_copycontent.rss -s http://localhost/reportserver  
```  
  
 자세한 예제는 [보고서 서버 간 콘텐츠 복사를 위한 예제 Reporting Services rs.exe 스크립트](../../reporting-services/tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md)를 참조하세요.  
  
 추가 예제는 [Reporting Services 스크립트 파일 실행](../../reporting-services/tools/run-a-reporting-services-script-file.md)을 참조하세요.  
  
## <a name="remarks"></a>Remarks  
 시스템 속성을 설정하고 보고서를 게시하는 등의 스크립트를 정의할 수 있습니다. 생성된 스크립트에는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] API의 모든 메서드가 포함될 수 있습니다. 사용할 수 있는 메서드 및 속성에 대한 자세한 내용은 [Report Server Web Service](../../reporting-services/report-server-web-service/report-server-web-service.md)를 참조하세요.  
  
 이 스크립트는 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET 코드로 작성하여 파일 이름 확장명이 .rss인 유니코드 또는 UTF-8 텍스트 파일로 저장해야 합니다. **rs** 유틸리티를 사용하여 스크립트를 디버깅할 수 없습니다. 스크립트를 디버깅하려면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]에서 코드를 실행하세요.  
  
> [!TIP]  
>  자세한 예제는 [보고서 서버 간 콘텐츠 복사를 위한 예제 Reporting Services rs.exe 스크립트](../../reporting-services/tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
- [Reporting Services 스크립트 파일 실행](../../reporting-services/tools/run-a-reporting-services-script-file.md)   
- [배포 및 관리 태스크 스크립팅](../../reporting-services/tools/script-deployment-and-administrative-tasks.md)   
- [rs.exe 유틸리티 및 웹 서비스를 사용한 스크립팅](../../reporting-services/tools/script-with-the-rs-exe-utility-and-the-web-service.md)   
- [보고서 서버 명령 프롬프트 유틸리티&#40;SSRS&#41;](../../reporting-services/tools/report-server-command-prompt-utilities-ssrs.md)  
  
  
