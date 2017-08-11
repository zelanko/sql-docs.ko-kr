---
title: "배달 확장 프로그램 배포 | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- delivery extensions [Reporting Services], deploying
- Extension element
- deploying [Reporting Services], extensions
ms.assetid: 4436ce48-397d-42c7-9b5d-2a267e2a1b2c
caps.latest.revision: 45
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: d072577828375a08c133bb1a68d93e652e5cf168
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="deploying-a-delivery-extension"></a>배달 확장 프로그램 배포
  배달 확장 프로그램은 XML 구성 파일 형식으로 구성 정보를 제공합니다. XML 파일은 배달 확장 프로그램에 대해 정의된 XML 스키마를 따릅니다. 배달 확장 프로그램은 구성 파일을 설정하고 수정하기 위한 인프라를 제공합니다.  
  
 배달 확장 프로그램이 교체되거나 업그레이드되어도 배달 확장 프로그램을 참조하는 모든 구독은 유효합니다.  
  
 작성 하 고 컴파일된 후 프로그램 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 배달 확장 프로그램을는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 라이브러리 확장 적절 한 디렉터리에 복사 하 고 적절 한 항목을 추가 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 구성 파일을 보고서 서버에서 찾을 수 있도록 합니다.  
  
## <a name="configuration-file-extension-element"></a>구성 파일 확장 프로그램 요소  
 보고서 서버에 배포 하는 배달 확장 프로그램으로 입력 해야 **확장** 구성 파일에 있는 요소입니다. 보고서 서버에 대한 구성 파일은 RSReportServer.config입니다.  
  
 다음 표에서 설명에 대 한 특성은 **확장** 배달 확장 프로그램에 대 한 요소입니다.  
  
|Attribute|Description|  
|---------------|-----------------|  
|**이름**|확장 프로그램에 대한 고유한 이름으로서 예를 들면 전자 메일 배달 확장 프로그램의 경우 "Report Server E-Mail", 파일 공유 배달 확장 프로그램의 경우 "Report Server FileShare" 등입니다. **Name** 특성의 최대 길이는 255자입니다. 이름은 구성 파일의 **Extension** 요소에 있는 모든 항목 중에서 고유해야 합니다. 중복된 이름이 있을 경우 보고서 서버에서 오류를 반환합니다.|  
|**형식**|정규화된 네임스페이스와 어셈블리 이름을 포함하는 쉼표로 구분된 목록입니다.|  
|**Visible**|값이 **false** 는 배달 확장 프로그램이 표시 되지 않음을 사용자 인터페이스에 나타냅니다. 이 특성이 포함되지 않을 경우 기본값은 **true**입니다.|  
  
 RSReportServer.config 파일에 대 한 자세한 내용은 참조 [Reporting Services Configuration Files](../../../reporting-services/report-server/reporting-services-configuration-files.md)합니다.  
  
## <a name="deploying-the-extension-to-the-report-server"></a>보고서 서버에 확장 프로그램 배포  
 보고서 서버에서는 알림이나 보고서의 처리 및 배달을 위해 배달 확장 프로그램을 사용합니다. 배달 확장 프로그램 어셈블리를 전용 어셈블리 형태로 보고서 서버에 배포해야 합니다. 또한 보고서 서버 구성 파일 RSReportServer.config에서 항목을 만들어야 합니다.  
  
#### <a name="to-deploy-a-deliver-extension-assembly-to-a-report-server"></a>보고서 서버에 배달 확장 프로그램 어셈블리를 배포하려면  
  
1.  준비 위치에서 배달 확장 프로그램을 사용할 보고서 서버의 bin 디렉터리로 어셈블리를 복사합니다. 보고서 서버 bin 디렉터리의 기본 위치는 %ProgramFiles%\Microsoft SQL Server\MSRS13입니다. \<InstanceName > services\reportserver\bin입니다.  
  
    > [!IMPORTANT]  
    >  기존 배달 확장 프로그램 어셈블리를 덮어쓰려는 경우 업데이트된 어셈블리를 복사하기 전에 먼저 보고서 서버 서비스를 중지해야 합니다. 어셈블리 복사가 완료된 후 서비스를 다시 시작합니다.  
  
2.  어셈블리 파일이 복사된 후 RSReportServer.config 파일을 엽니다. RSReportServer.config 파일은 %ProgramFiles%\Microsoft SQL Server\MSRS13에에서 있습니다. \<InstanceName > services\reportserver 디렉터리입니다. 구성 파일에서 배달 확장 프로그램 어셈블리 파일에 대한 항목을 만들어야 합니다. 구성 파일을 열면 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 또는 메모장과 같은 간단한 텍스트 편집기입니다.  
  
3.  찾을 **배달** RSReportServer.config 파일의 요소입니다. 새로 만든 배달 확장 프로그램에 대한 항목이 다음 위치에 있어야 합니다.  
  
    ```  
    <Extensions>  
       <Delivery>  
          <Your extension configuration information goes here>  
       </Delivery>  
    </Extensions>  
    ```  
  
4.  배달 확장 프로그램에 대한 항목을 추가합니다. 입력 한 내용을 포함 되어야는 **확장** 에 대 한 값이 있는 요소 **이름** 및 **형식**, 하며 다음과 같습니다.  
  
    ```  
    <Extension Name="My Delivery Extension Name" Type="CompanyName.ExtensionName.MyDeliveryExtensionClass, AssemblyName" />  
    ```  
  
     에 대 한 값 **이름** 배달 확장 프로그램의 고유 이름입니다. 에 대 한 값 **형식** 구현 하는 클래스의 정규화 된 네임 스페이스에 대 한 항목을 포함 하는 쉼표로 구분 된 목록에서 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> 인터페이스를 사용자 어셈블리 (.dll 파일 확장명 제외)의 이름이 차례로 나옵니다. 기본적으로 배달 확장 프로그램은 표시됩니다. 웹 포털 등의 사용자 인터페이스에 확장 프로그램을 숨기려면 추가 **Visible** 특성을 **확장** 요소를이 속성을 설정 하 고 **false**합니다.  
  
5.  마지막으로, 권한을 부여 하는 사용자 지정 어셈블리에 대 한 코드 그룹을 추가 **FullTrust** 배달 확장 프로그램에 대 한 권한이 있습니다. 기본적으로 %ProgramFiles%\Microsoft SQL Server\MSRS13에에서 rssrvpolicy.config 파일에 코드 그룹을 추가 하 여이 작업을 수행 합니다. \<InstanceName > services\reportserver입니다. 코드 그룹은 다음과 같습니다.  
  
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
  
     URL 멤버 자격은 배달 확장 프로그램에 대해 선택할 수 있는 많은 멤버 자격 조건 중 하나일 뿐입니다. 코드 액세스 보안에 대 한 자세한 내용은 [!INCLUDE[ssRS](../../../includes/ssrs-md.md)]를 참조 하세요.[ 개발 &#40; 보안 Reporting services&#41;](../../../reporting-services/extensions/secure-development/secure-development-reporting-services.md)  
   
## <a name="verifying-the-deployment"></a>배포 확인  
 웹 서비스 <xref:ReportService2010.ReportingService2010.ListExtensions%2A> 메서드를 사용하여 배달 확장 프로그램이 보고서 서버에 성공적으로 배포되었는지 여부를 확인할 수 있습니다. 웹 포털을 열고 확장 프로그램이 구독에 대 한 사용 가능한 배달 확장 프로그램 목록에 포함 되어 있는지 확인 하십시오. 수도 있습니다. 웹 포털 및 구독에 대 한 자세한 내용은 참조 [구독 및 배달 &#40; Reporting services&#41; ](../../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md).  
  
## <a name="see-also"></a>관련 항목:  
 [배달 확장 프로그램 구현](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 확장 프로그램 라이브러리](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  

