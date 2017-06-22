---
title: "렌더링 확장 프로그램 배포 | Microsoft Docs"
ms.custom: 
ms.date: 03/20/2017
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
- deploying [Reporting Services], extensions
- rendering extensions [Reporting Services], deploying
ms.assetid: 9fb8c887-5cb2-476e-895a-7b0e2dd11398
caps.latest.revision: 44
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 260e104d2686ab9111c9b38c2ecf6c5da2fbdb91
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="deploying-a-rendering-extension"></a>렌더링 확장 프로그램 배포
  작성 하 고 컴파일된 후 프로그램 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 보고서 렌더링 확장 프로그램에는 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 라이브러리, 보고서 디자이너 및 보고서 서버에서 검색할 수 있도록 해야 합니다. 이 작업을 수행하려면 확장 프로그램을 적절한 디렉터리에 복사하고 해당하는 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 구성 파일에 항목을 추가합니다.  
  
## <a name="configuration-file-rendering-extension-element"></a>구성 파일 렌더링 확장 프로그램 요소  
 렌더링 확장 프로그램이 .DLL로 컴파일되었으면 항목을 rsreportserver.config 파일에 추가합니다. 기본적으로 위치는 %ProgramFiles%\Microsoft SQL Server\MSRS10_50입니다. \<InstanceName > services\reportserver입니다. 부모 요소가 \<렌더링 > 합니다. Render 요소 아래에 각 렌더링 확장 프로그램에 대한 Extension 요소가 있습니다. **Extension** 요소에는 Name 및 Type의 두 가지 특성이 포함됩니다.  
  
 다음 표에서는 렌더링 확장 프로그램에 대한 **Extension** 요소의 특성을 설명합니다.  
  
|Attribute|Description|  
|---------------|-----------------|  
|**이름**|확장 프로그램의 고유한 이름입니다. **Name** 특성의 최대 길이는 255자입니다. 이름은 구성 파일의 **Extensions** 요소 내 모든 항목에서 고유해야 합니다. 중복된 이름이 있을 경우 보고서 서버에서 오류를 반환합니다.|  
|**형식**|정규화된 네임스페이스와 어셈블리 이름을 포함하는 쉼표로 구분된 목록입니다.|  
|**Visible**|**false** 값은 렌더링 확장 프로그램이 사용자 인터페이스에 표시되지 않음을 나타냅니다. 이 특성이 포함되지 않을 경우 기본값은 **true**입니다.|  
|**LogAllExecutionRequests**|**false** 값은 세션의 첫 번째 보고서 실행에 대해서만 로그 항목이 기록됨을 나타냅니다. 이 특성이 포함되지 않을 경우 기본값은 **true**입니다.<br /><br /> 예를 들어 이 설정은 보고서에서 렌더링되는 첫 페이지에 대해서만 로그 항목을 기록할지( **false**인 경우) 또는 보고서에서 렌더링되는 각 페이지에 대해 로그 항목을 기록할지( **true**인 경우) 여부를 결정합니다.|  
  
 자세한 내용은 [RsReportServer.config 구성 파일](../../../reporting-services/report-server/rsreportserver-config-configuration-file.md)을 참조하세요.  
  
## <a name="deploying-the-extension-to-the-report-server"></a>보고서 서버에 확장 프로그램 배포  
 보고서 서버에서는 보고서를 다른 형식으로 내보내기 위해 렌더링 확장 프로그램을 사용합니다. 렌더링 확장 프로그램 어셈블리를 전용 어셈블리 형태로 보고서 서버에 배포해야 합니다. 또한 보고서 서버 구성 파일 rsreportserver.config에서 항목을 만들어야 합니다.  
  
### <a name="to-deploy-the-assembly"></a>어셈블리를 배포하려면  
  
1.  준비 위치에서 렌더링 확장 프로그램을 사용할 보고서 서버의 bin 디렉터리로 어셈블리를 복사합니다. 보고서 서버 Bin 디렉터리의 기본 위치는 %ProgramFiles%\Microsoft SQL Server\MSRS10_50입니다. \<InstanceName > services\reportserver\bin입니다.  
  
2.  어셈블리 파일이 복사된 후 rsreportserver.config 파일을 엽니다. rsreportserver.config 파일도 보고서 서버 bin 디렉터리에 있습니다. 구성 파일에서 확장 프로그램 어셈블리 파일에 대한 항목을 만들어야 합니다. 사용 하 여 파일을 열 수 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 또는 간단한 텍스트 편집기입니다.  
  
     자세한 내용은 [RsReportServer.config 구성 파일](../../../reporting-services/report-server/rsreportserver-config-configuration-file.md)을 참조하세요.  
  
3.  Rsreportserver.config 파일에서 **Render** 요소를 찾습니다. 새로 만든 확장 프로그램에 대한 항목이 다음 위치에 있어야 합니다.  
  
    ```  
    <Extensions>  
       <Render>  
          <extension configuration>  
       </Render>  
    </Extensions>  
    ```  
  
4.  렌더링 확장 프로그램에 대한 항목을 추가합니다. 항목에 **Name** 및 **Type**에 대한 값이 있는 요소가 포함되어야 하며 다음과 같습니다.  
  
    ```  
    <Extension Name="My Rendering Extension Name" Type="CompanyName.ExtensionName.MyRenderingProvider, AssemblyName" />  
    ```  
  
     **Name** 에 대한 값은 렌더링 확장 프로그램의 고유한 이름입니다. 에 대 한 값 **형식** 의 정규화 된 네임 스페이스에 대 한 항목을 포함 하는 쉼표로 구분 된 목록에 <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension> 구현에서 사용자 어셈블리 (.dll 파일 확장명 제외)의 이름이 차례로 나옵니다. 기본적으로 렌더링 확장 프로그램은 표시됩니다. 보고서 관리자와 같은 사용자 인터페이스에 확장 프로그램이 표시되지 않도록 숨기려면 **Visible** 특성을 **Extension** 요소에 추가하고 **false**로 설정합니다.  
  
## <a name="verifying-the-deployment"></a>배포 확인  
 보고서 관리자를 열고 확장 프로그램이 보고서에 대해 사용 가능한 내보내기 유형 목록에 포함되어 있는지 확인할 수도 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [렌더링 확장 프로그램 구현](../../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md)   
 [렌더링 확장 프로그램 개요](../../../reporting-services/extensions/rendering-extension/rendering-extensions-overview.md)   
 [IRenderingExtension 인터페이스 구현](../../../reporting-services/extensions/rendering-extension/implementing-the-irenderingextension-interface.md)   
 [확장에 대 한 보안 고려 사항](../../../reporting-services/extensions/security-considerations-for-extensions.md)  
  
  
