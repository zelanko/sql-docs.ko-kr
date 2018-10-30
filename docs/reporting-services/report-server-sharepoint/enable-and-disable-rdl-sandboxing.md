---
title: SharePoint 통합 모드에서 Reporting Services에 RDL 샌드박싱 설정 및 해제 | Microsoft Docs
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1cf64bf1e07a83defbc3553535251f51fa96f839
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50032122"
---
# <a name="enable-and-disable-rdl-sandboxing-for-reporting-services-in-sharepoint-integrated-mode"></a>SharePoint 통합 모드에서 Reporting Services에 RDL 샌드박싱 설정 및 해제

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

RDL(Report Definition Language) 샌드박싱 기능을 사용하면 보고서 서버의 단일 웹 팜을 여러 명이 사용하는 환경에서 각 개인에 대해 특정 형식의 리소스 사용을 검색하고 제한할 수 있습니다. 여러 명 그리고 경우에 따라 서로 다른 회사에서 사용할 수 있는 보고서 서버의 단일 웹 팜을 유지 관리하는 호스팅 서비스 시나리오를 예로 들 수 있습니다. 보고서 서버 관리자는 이 기능을 설정하여 다음과 같이 할 수 있습니다.  
  
-   외부 리소스 크기를 제한합니다. 외부 리소스에는 이미지, .xslt 파일, 지도 데이터 등이 포함됩니다.  
  
-   보고서를 게시할 때 식 텍스트에 사용되는 형식 및 멤버를 제한합니다.  
  
-   보고서를 처리할 때 식의 반환 값 크기와 텍스트 길이를 제한합니다.

> [!NOTE]
> SQL Server 2016 이후부터 SharePoint와의 Reporting Services 통합을 사용할 수 없습니다.

 RDL 샌드박싱 기능이 설정되면 다음 기능을 사용할 수 없습니다.  
  
-   보고서 정의 요소 **\<Code>** 의 사용자 지정 코드  
  
-   [!INCLUDE[ssRSversion2005](../../includes/ssrsversion2005-md.md)] 사용자 지정 보고서 항목을 위한 RDL 이전 버전 호환 모드  
  
-   식의 명명된 매개 변수  
  
 이 항목에서는 RSReportServer.Config 파일에서 \<**RDLSandboxing**> 요소의 각 요소에 대해 설명합니다. 이 파일을 수정하는 방법은 [Reporting Services 구성 파일 수정&#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)을 참조하세요. 서버 추적 로그는 RDL 샌드박싱 기능과 관련된 작업을 기록합니다. 추적 로그에 대한 자세한 내용은 [보고서 서버 서비스 추적 로그](../../reporting-services/report-server/report-server-service-trace-log.md)를 참조하세요.  
  
## <a name="example-configuration"></a>구성 예
 다음 예에서는 RSReportServer.Config 파일의 \<**RDLSandboxing**> 요소에 대한 설정 및 값 예를 보여 줍니다.  
  
```  
<RDLSandboxing>  
   <MaxExpressionLength>5000</MaxExpressionLength>  
   <MaxResourceSize>5000</MaxResourceSize>  
   <MaxStringResultLength>3000</MaxStringResultLength>  
   <MaxArrayResultLength>250</MaxArrayResultLength>  
   <Types>  
      <Allow Namespace=”System.Drawing” AllowNew=”True”>Bitmap</Allow>  
      <Allow Namespace=”TypeConverters.Custom” AllowNew=”True”>*</Allow>  
   </Types>  
   <Members>  
      <Deny>Format</Deny>  
      <Deny>StrDup</Deny>  
   </Members>  
</RDLSandboxing>  
```

## <a name="configuration-settings"></a>구성 설정

 다음 표에서는 구성 설정 정보를 제공합니다. 설정은 구성 파일에 나타나는 순서로 표시됩니다.  
  
|설정|설명|  
|-------------|-----------------|  
|**MaxExpressionLength**|RDL 식에 허용되는 최대 문자 수입니다.<br /><br /> 기본값: 1000|  
|**MaxResourceSize**|외부 리소스에 허용되는 최대 크기(KB)입니다.<br /><br /> 기본값: 100|  
|**MaxStringResultLength**|RDL 식의 반환 값에 허용되는 최대 문자 수입니다.<br /><br /> 기본값: 1000|  
|**MaxArrayResultLength**|RDL 식의 배열 반환 값에 허용되는 최대 항목 수입니다.<br /><br /> 기본값: 100|  
|**유형**|RDL 식 내에 허용할 멤버 목록입니다.|  
|**Allow**|RDL 식에 허용할 형식 또는 형식 집합입니다.|  
|**Namespace**|**Allow** 의 특성이며, Value에 적용되는 하나 이상의 형식이 포함된 네임스페이스입니다. 이 속성은 대/소문자를 구분하지 않습니다.|  
|**AllowNew**|**Allow**의 부울 특성이며, 새 형식 인스턴스를 RDL 식에 만들 수 있는지 아니면 RDL **\<Class>** 요소에 만들 수 있는지를 제어합니다.<br /><br /> 참고: **RDLSandboxing**을 사용하도록 설정하면 **AllowNew** 설정에 관계 없이 새 배열을 RDL 식에 만들 수 없습니다.|  
|**Value**|**Allow** 의 값이며, RDL 식에 허용할 형식의 이름입니다. **\*** 값은 네임스페이스의 모든 형식이 허용됨을 나타냅니다. 이 속성은 대/소문자를 구분하지 않습니다.|  
|**멤버**|**\<Types>** 요소에 포함된 형식 목록의 경우 RDL 식에 허용되지 않는 멤버 이름 목록입니다.|  
|**거부**|RDL 식에 허용되지 않는 멤버의 이름입니다. 이 속성은 대/소문자를 구분하지 않습니다.<br /><br /> 멤버에 **거부**가 지정되면 모든 형식에 대해 이 이름을 사용하는 멤버가 모두 허용되지 않습니다.|  
  
## <a name="working-with-expressions-when-rdl-sandboxing-is-enabled"></a>RDL 샌드박싱을 사용하는 경우 식 작업

식에 사용되는 리소스를 관리하기 위해 다음과 같은 방식으로 RDL 샌드박싱 기능을 수정할 수 있습니다.  
  
-   식에 사용되는 문자의 수를 제한합니다.  
  
-   식에서 반환되는 결과의 크기를 제한합니다.  
  
-   식에 사용할 수 있는 특정 형식 목록을 허용합니다.  
  
-   식에 사용할 수 있는 허용된 형식 목록에 대해 이름별로 멤버 목록을 제한합니다.  
  
-   RDL 샌드박싱 기능을 사용하면 승인된 형식 목록과 거부된 멤버 목록을 만들 수 있습니다. 승인된 형식 목록을 허용 목록이라고 하고 거부된 멤버 목록을 차단 목록이라고 합니다.  
  
> [!NOTE]  
>  보고서 정의에서 컴퓨터는 식 참조의 각 인스턴스에 대한 형식을 알 수 없습니다. 차단 목록에 멤버를 추가하면 허용 목록에 있는 모든 형식에 대해 해당 이름을 갖는 모든 멤버가 거부됩니다.  
  
 RDL 식 결과는 런타임에 확인됩니다. RDL 식은 보고서가 게시되면 보고서 정의에서 확인됩니다. 보고서 서버 추적 로그를 모니터링하여 위반 항목이 있는지 확인할 수 있습니다. 자세한 내용은 [Report Server Service Trace Log](../../reporting-services/report-server/report-server-service-trace-log.md)을 참조하세요.  
  
### <a name="working-with-types"></a>형식 사용

 허용 목록에 형식을 추가하면 RDL 식에 액세스하기 위해 다음 진입점을 제어하게 됩니다.  
  
-   형식의 정적 멤버  
  
-   [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] **New** 메서드  
  
-   보고서 정의의 **\<Classes>** 요소  
  
-   허용 목록의 형식에 대해 차단 목록에 추가한 멤버  
  
 허용 목록은 다음 진입점을 제어하지 않습니다.  
  
-   보고서 데이터 집합. 쿼리에서 반환된 보고서 데이터 집합 필드에는 유효한 RDL 형식이 포함되었을 수 있습니다.  
  
-   보고서 매개 변수 사용자가 제공한 매개 변수 값에는 유효한 RDL 형식이 포함되었을 수 있습니다.  
  
-   사용 가능한 형식 중에서 차단 목록에 없는 멤버. 기본적으로 허용 목록에 있는 모든 형식의 모든 멤버는 사용할 수 있도록 설정됩니다. 그러나 차단 목록에 멤버 이름을 추가하면 허용 목록에 있는 모든 형식에 대해 해당 이름을 갖는 모든 멤버가 거부됩니다.  
  
 특정 형식의 멤버를 사용하도록 설정하지만 다른 형식 중에서 같은 이름을 사용하는 멤버는 거부하려면 다음과 같이 해야 합니다.  
  
-   멤버 이름에 대해 **\<Deny>** 요소를 추가합니다.  
  
-   사용하도록 설정할 멤버에 대해 사용자 지정 어셈블리의 클래스에 이름이 다른 프록시 멤버를 만듭니다.  
  
-   새 클래스를 허용 목록에 추가합니다.  
  
 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET Framework 함수를 허용 목록에 추가하려면 Microsoft.VisualBasic 네임스페이스에서 해당하는 형식을 허용 목록에 추가합니다.  
  
 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET Framework 형식 키워드를 허용 목록에 추가하려면 해당하는 CLR 형식을 허용 목록에 추가합니다. 예를 들어 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET Framework 키워드 **Integer**를 사용하려면 다음 XML 조각을 **\<RDLSandboxing>** 요소에 추가합니다.  
  
```  
<Allow Namespace="System">Int32</Allow>  
```  
  
 일반 또는 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET Framework Null 허용 형식을 허용 목록에 추가하려면 다음과 같이 해야 합니다.  
  
-   일반 또는 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET Framework Null 허용 형식에 대한 프록시 형식을 만듭니다.  
  
-   새로 만든 프록시 형식을 허용 목록에 추가합니다.  
  
 사용자 지정 어셈블리의 형식을 허용 목록에 추가해도 암시적으로 이 어셈블리에 대해 실행 권한이 부여되는 것은 아닙니다. 코드 액세스 보안 파일을 명확하게 수정하고 어셈블리에 대한 실행 권한을 제공해야 합니다. 자세한 내용은 [Code Access Security in Reporting Services](../../reporting-services/extensions/secure-development/code-access-security-in-reporting-services.md)을 참조하세요.  
  
#### <a name="maintaining-the-deny-list-of-members"></a>멤버의 \<거부> 목록 유지 관리

 허용 목록에 새 형식을 추가하는 경우 다음 목록을 사용하여 멤버의 차단 목록을 업데이트해야 할 시기를 결정할 수 있습니다.  
  
-   새 형식을 제공하는 버전으로 사용자 지정 어셈블리를 업데이트하는 경우  
  
-   허용 목록의 형식에 멤버를 추가하는 경우  
  
-   보고서 서버에서 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 를 업데이트하는 경우  
  
-   보고서 서버를 이후 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]로 업그레이드하는 경우  
  
-   RDL 형식에 새 멤버가 추가되어 나중 RDL 스키마를 처리하기 위해 보고서 서버를 업데이트하는 경우  
  
### <a name="working-with-operators-and-new"></a>연산자 및 new 사용

 기본적으로 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] New **를 제외한**.NET Framework 언어 연산자는 항상 허용됩니다. **New** 연산자는 **\<Allow>** 요소의 **AllowNew** 특성에서 제어합니다. 기본 컬렉션 접근자 연산자 **!** 와 같은 기타 언어 연산자 및 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] CInt **와 같은**.NET Framework 캐스트 매크로는 항상 허용됩니다.  
  
 사용자 지정 연산자를 포함하여 연산자를 차단 목록에 추가하는 것은 지원되지 않습니다. 형식에 대해 연산자를 실행하려면 다음과 같이 해야 합니다.  
  
-   제외할 연산자를 구현하지 않는 프록시 형식을 만듭니다.  
  
-   새로 만든 프록시 형식을 허용 목록에 추가합니다.  
  
 RDL 식에 새 배열을 만들려면 정의하는 클래스에서 메서드에 배열을 만들고 이 클래스를 허용 목록에 추가합니다.  
  
 RDL 식에 새 배열을 만들려면 다음과 같이 해야 합니다.  
  
-   새 클래스를 정의하고 해당 클래스의 메서드에 배열을 만듭니다.  
  
-   이 클래스를 허용 목록에 추가합니다.  
  
## <a name="see-also"></a>관련 항목:

 [RsReportServer.config 구성 파일](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [보고서 서버 서비스 추적 로그](../../reporting-services/report-server/report-server-service-trace-log.md)  

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](https://go.microsoft.com/fwlink/?LinkId=620231)
