---
title: "렌더링 확장 프로그램 배포 | Microsoft Docs"
ms.custom: 
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: extensions
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- deploying [Reporting Services], extensions
- rendering extensions [Reporting Services], deploying
ms.assetid: 9fb8c887-5cb2-476e-895a-7b0e2dd11398
caps.latest.revision: "44"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f87218d946f44beadf3f75e86816d448fe5361f2
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="deploying-a-rendering-extension"></a>렌더링 확장 프로그램 배포
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 보고서 렌더링 확장 프로그램을 작성하고 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 라이브러리에 컴파일한 후에는 보고서 서버 및 보고서 디자이너에서 이를 찾을 수 있도록 해야 합니다. 이 작업을 수행하려면 확장 프로그램을 적절한 디렉터리에 복사하고 해당하는 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 구성 파일에 항목을 추가합니다.  
  
## <a name="configuration-file-rendering-extension-element"></a>구성 파일 렌더링 확장 프로그램 요소  
 렌더링 확장 프로그램이 .DLL로 컴파일되었으면 항목을 rsreportserver.config 파일에 추가합니다. 기본적으로 이 파일은 %ProgramFiles%\Microsoft SQL Server\MSRS10_50.\<InstanceName>\Reporting Services\ReportServer에 있습니다. 부모 요소는 \<Render>입니다. Render 요소 아래에 각 렌더링 확장 프로그램에 대한 Extension 요소가 있습니다. **Extension** 요소에는 Name 및 Type의 두 가지 특성이 포함됩니다.  
  
 다음 표에서는 렌더링 확장 프로그램에 대한 **Extension** 요소의 특성을 설명합니다.  
  
|attribute|Description|  
|---------------|-----------------|  
|**이름**|확장 프로그램의 고유한 이름입니다. **Name** 특성의 최대 길이는 255자입니다. 이름은 구성 파일의 **Extensions** 요소 내 모든 항목에서 고유해야 합니다. 중복된 이름이 있을 경우 보고서 서버에서 오류를 반환합니다.|  
|**형식**|정규화된 네임스페이스와 어셈블리 이름을 포함하는 쉼표로 구분된 목록입니다.|  
|**Visible**|**false** 값은 렌더링 확장 프로그램이 사용자 인터페이스에 표시되지 않음을 나타냅니다. 이 특성이 포함되지 않을 경우 기본값은 **true**입니다.|  
|**LogAllExecutionRequests**|**false** 값은 세션의 첫 번째 보고서 실행에 대해서만 로그 항목이 기록됨을 나타냅니다. 이 특성이 포함되지 않을 경우 기본값은 **true**입니다.<br /><br /> 예를 들어 이 설정은 보고서에서 렌더링되는 첫 페이지에 대해서만 로그 항목을 기록할지( **false**인 경우) 또는 보고서에서 렌더링되는 각 페이지에 대해 로그 항목을 기록할지( **true**인 경우) 여부를 결정합니다.|  
  
 자세한 내용은 [RsReportServer.config 구성 파일](../../../reporting-services/report-server/rsreportserver-config-configuration-file.md)을 참조하세요.  
  
## <a name="deploying-the-extension-to-the-report-server"></a>보고서 서버에 확장 프로그램 배포  
 보고서 서버에서는 보고서를 다른 형식으로 내보내기 위해 렌더링 확장 프로그램을 사용합니다. 렌더링 확장 프로그램 어셈블리를 전용 어셈블리 형태로 보고서 서버에 배포해야 합니다. 또한 보고서 서버 구성 파일 rsreportserver.config에서 항목을 만들어야 합니다.  
  
### <a name="to-deploy-the-assembly"></a>어셈블리를 배포하려면  
  
1.  준비 위치에서 렌더링 확장 프로그램을 사용할 보고서 서버의 bin 디렉터리로 어셈블리를 복사합니다. 보고서 서버 Bin 디렉터리의 기본 위치는 %ProgramFiles%\Microsoft SQL Server\MSRS10_50.\<InstanceName>\Reporting Services\ReportServer\Bin입니다.  
  
2.  어셈블리 파일이 복사된 후 rsreportserver.config 파일을 엽니다. rsreportserver.config 파일도 보고서 서버 bin 디렉터리에 있습니다. 구성 파일에서 확장 프로그램 어셈블리 파일에 대한 항목을 만들어야 합니다. 이 파일은 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 또는 간단한 텍스트 편집기에서 열 수 있습니다.  
  
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
  
     **Name** 에 대한 값은 렌더링 확장 프로그램의 고유한 이름입니다. **Type**의 값은 <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension> 구현의 정규화된 네임스페이스에 대한 항목과 그 다음에 어셈블리의 이름(.dll 파일 확장명 포함 안 함)이 따라오는 형태가 포함되며 쉼표로 구분된 목록입니다. 기본적으로 렌더링 확장 프로그램은 표시됩니다. 보고서 관리자와 같은 사용자 인터페이스에 확장 프로그램이 표시되지 않도록 숨기려면 **Visible** 특성을 **Extension** 요소에 추가하고 **false**로 설정합니다.  
  
## <a name="verifying-the-deployment"></a>배포 확인  
 보고서 관리자를 열고 확장 프로그램이 보고서에 대해 사용 가능한 내보내기 유형 목록에 포함되어 있는지 확인할 수도 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [렌더링 확장 프로그램 구현](../../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md)   
 [렌더링 확장 프로그램 개요](../../../reporting-services/extensions/rendering-extension/rendering-extensions-overview.md)   
 [IRenderingExtension 인터페이스 구현](../../../reporting-services/extensions/rendering-extension/implementing-the-irenderingextension-interface.md)   
 [확장에 대한 보안 고려 사항](../../../reporting-services/extensions/security-considerations-for-extensions.md)  
  
  
