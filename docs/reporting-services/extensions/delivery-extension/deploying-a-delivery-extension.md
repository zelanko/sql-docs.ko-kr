---
title: 배달 확장 프로그램 배포 | Microsoft Docs
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.suite: pro-bi
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- delivery extensions [Reporting Services], deploying
- Extension element
- deploying [Reporting Services], extensions
ms.assetid: 4436ce48-397d-42c7-9b5d-2a267e2a1b2c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 356f29e4f92c4949e311993ee1444bb57ad61aa9
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43270003"
---
# <a name="deploying-a-delivery-extension"></a>배달 확장 프로그램 배포
  배달 확장 프로그램은 XML 구성 파일 형식으로 구성 정보를 제공합니다. XML 파일은 배달 확장 프로그램에 대해 정의된 XML 스키마를 따릅니다. 배달 확장 프로그램은 구성 파일을 설정하고 수정하기 위한 인프라를 제공합니다.  
  
 배달 확장 프로그램이 교체되거나 업그레이드되어도 배달 확장 프로그램을 참조하는 모든 구독은 유효합니다.  
  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 배달 확장 프로그램을 작성하고 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 라이브러리에 컴파일한 후 확장 프로그램을 적절한 디렉터리에 복사하고 해당하는 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 구성 파일에 항목을 추가하여 보고서 서버에서 찾을 수 있도록 해야 합니다.  
  
## <a name="configuration-file-extension-element"></a>구성 파일 확장 프로그램 요소  
 보고서 서버에 배포하는 배달 확장 프로그램은 구성 파일에서 **Extension** 요소로 입력되어야 합니다. 보고서 서버에 대한 구성 파일은 RSReportServer.config입니다.  
  
 다음 표는 배달 확장 프로그램에 대한 **Extension** 요소의 특성을 설명합니다.  
  
|attribute|설명|  
|---------------|-----------------|  
|**이름**|확장 프로그램에 대한 고유한 이름으로서 예를 들면 전자 메일 배달 확장 프로그램의 경우 "Report Server E-Mail", 파일 공유 배달 확장 프로그램의 경우 "Report Server FileShare" 등입니다. **Name** 특성의 최대 길이는 255자입니다. 이름은 구성 파일의 **Extension** 요소에 있는 모든 항목 중에서 고유해야 합니다. 중복된 이름이 있을 경우 보고서 서버에서 오류를 반환합니다.|  
|**형식**|정규화된 네임스페이스와 어셈블리 이름을 포함하는 쉼표로 구분된 목록입니다.|  
|**Visible**|**false** 값은 배달 확장 프로그램이 사용자 인터페이스에 표시되지 않음을 나타냅니다. 이 특성이 포함되지 않을 경우 기본값은 **true**입니다.|  
  
 RSReportServer.config 파일에 대한 자세한 내용은 [Reporting Services 구성 파일](../../../reporting-services/report-server/reporting-services-configuration-files.md)을 참조하세요.  
  
## <a name="deploying-the-extension-to-the-report-server"></a>보고서 서버에 확장 프로그램 배포  
 보고서 서버에서는 알림이나 보고서의 처리 및 배달을 위해 배달 확장 프로그램을 사용합니다. 배달 확장 프로그램 어셈블리를 전용 어셈블리 형태로 보고서 서버에 배포해야 합니다. 또한 보고서 서버 구성 파일 RSReportServer.config에서 항목을 만들어야 합니다.  
  
#### <a name="to-deploy-a-deliver-extension-assembly-to-a-report-server"></a>보고서 서버에 배달 확장 프로그램 어셈블리를 배포하려면  
  
1.  준비 위치에서 배달 확장 프로그램을 사용할 보고서 서버의 bin 디렉터리로 어셈블리를 복사합니다. 보고서 서버 Bin 디렉터리의 기본 위치는 %ProgramFiles%\Microsoft SQL Server\MSRS13.\<InstanceName>\Reporting Services\ReportServer\bin입니다.  
  
    > [!IMPORTANT]  
    >  기존 배달 확장 프로그램 어셈블리를 덮어쓰려는 경우 업데이트된 어셈블리를 복사하기 전에 먼저 보고서 서버 서비스를 중지해야 합니다. 어셈블리 복사가 완료된 후 서비스를 다시 시작합니다.  
  
2.  어셈블리 파일이 복사된 후 RSReportServer.config 파일을 엽니다. RSReportServer.config 파일은 %ProgramFiles%\Microsoft SQL Server\MSRS13.\<InstanceName>\Reporting Services\ReportServer 디렉터리에 있습니다. 구성 파일에서 배달 확장 프로그램 어셈블리 파일에 대한 항목을 만들어야 합니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 또는 메모장과 같은 간단한 텍스트 편집기를 사용하여 구성 파일을 열 수 있습니다.  
  
3.  RSReportServer.config 파일에서 **Delivery** 요소를 찾습니다. 새로 만든 배달 확장 프로그램에 대한 항목이 다음 위치에 있어야 합니다.  
  
    ```  
    <Extensions>  
       <Delivery>  
          <Your extension configuration information goes here>  
       </Delivery>  
    </Extensions>  
    ```  
  
4.  배달 확장 프로그램에 대한 항목을 추가합니다. 항목에 **Name** 및 **Type**에 대한 값이 있는 **Extension** 요소가 포함되어야 하며 다음과 같습니다.  
  
    ```  
    <Extension Name="My Delivery Extension Name" Type="CompanyName.ExtensionName.MyDeliveryExtensionClass, AssemblyName" />  
    ```  
  
     **Name**에 대한 값은 배달 확장 프로그램의 고유한 이름입니다. **Type**의 값은 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> 인터페이스를 구현하는 클래스의 정규화된 네임스페이스에 대한 항목과 그 다음에 어셈블리의 이름(.dll 파일 확장명 포함 안 함)이 따라오는 형태가 포함되며 쉼표로 구분된 목록입니다. 기본적으로 배달 확장 프로그램은 표시됩니다. 웹 포털과 같은 사용자 인터페이스에 확장 프로그램이 표시되지 않도록 숨기려면 **Visible** 특성을 **Extension** 요소에 추가하고 **false**로 설정합니다.  
  
5.  마지막으로 배달 확장 프로그램에 대해 **FullTrust** 권한을 부여하는 사용자 지정 어셈블리에 대한 코드 그룹을 추가합니다. 기본적으로 %ProgramFiles%\Microsoft SQL Server\MSRS13.\<InstanceName>\Reporting Services\ReportServer에 있는 rssrvpolicy.config 파일에 코드 그룹을 추가하여 이 작업을 수행할 수 있습니다. 코드 그룹은 다음과 같습니다.  
  
    ```  
    <CodeGroup class="UnionCodeGroup"  
       version="1"  
       PermissionSetName="FullTrust"  
       Name="MyExtensionCodeGroup"  
       Description="Code group for my delivery extension">  
          <IMembershipCondition class="UrlMembershipCondition"  
             version="1"  
             Url="C:\Program Files\Microsoft SQL Server\MSRS13.<InstanceName>\Reporting Services\ReportServer\bin\MyExtensionAssembly.dll"  
           />  
    </CodeGroup>  
    ```  
  
     URL 멤버 자격은 배달 확장 프로그램에 대해 선택할 수 있는 많은 멤버 자격 조건 중 하나일 뿐입니다. [!INCLUDE[ssRS](../../../includes/ssrs.md)]의 코드 액세스 보안에 대한 자세한 내용은 [보안 개발&#40;Reporting Services&#41;](../../../reporting-services/extensions/secure-development/secure-development-reporting-services.md)을 참조하세요.  
   
## <a name="verifying-the-deployment"></a>배포 확인  
 웹 서비스 <xref:ReportService2010.ReportingService2010.ListExtensions%2A> 메서드를 사용하여 배달 확장 프로그램이 보고서 서버에 성공적으로 배포되었는지 여부를 확인할 수 있습니다. 웹 포털을 열고 확장 프로그램이 구독에 대해 사용 가능한 배달 확장 프로그램 목록에 포함되어 있는지 확인할 수도 있습니다. 웹 포털 및 구독에 대한 자세한 내용은 [구독 및 배달&#40;Reporting Services&#41;](../../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [배달 확장 프로그램 구현](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 확장 라이브러리](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
